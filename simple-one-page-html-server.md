```c
/* A simple website server example
    
   $ server_html
    
   Author: Chen Sun
   */
#include <stdio.h>
#include <sys/stat.h>
#include <fcntl.h>
#include <sys/types.h> 
#include <sys/socket.h>
#include <netinet/in.h>
#include <stdlib.h>
#include <strings.h>
#include <unistd.h>
#include <sys/uio.h>

char webpage[] = 
"HTTP/1.1 200 OK\r\n"
"Content-Type: text/html; charset=UTF-8\r\n\r\n"
"<!DOCTYPE html>\r\n"
"<html><head><title> EZ4 CSC209 </title> \r\n"
"<style>body{background-color: #FFF000}</style></head>\r\n"
"<body><center><h1>Hello World</h1><br>\r\n"
"<img src=\"doctest.jpg\"></center></body></html>\r\n";

int main (int argc, char *argv[]){
	struct sockaddr_in server_addr, client_addr;
	socklen_t sin_len = sizeof(client_addr);
	int fd_server, fd_client;
	char buf[2048];
	int fdimg;

	fd_server = socket(AF_INET, SOCK_STREAM, 0);
	if (fd_server < 0){
		perror("socket wrong");
		exit(1);
	}

	memset(&server_addr, 0, sizeof (server_addr));
    server_addr.sin_family = AF_INET;
    server_addr.sin_addr.s_addr = htonl(INADDR_ANY);
    server_addr.sin_port = htons(8080);

    if (bind(fd_server, (struct sockaddr *)&server_addr, sizeof (server_addr))) {
        perror("bind");
        close(fd_server);
        exit(1);
    }

    /*LISTEN FROM PORT*/
    if (listen(fd_server, 5)) {
        perror("listen");
        close(fd_server);
        exit(1);
    }
    // ACTIONS
    while(1){
    	fd_client = accept(fd_server, (struct sockaddr *)&client_addr, &sin_len);
    	if (fd_client == -1){
    		perror("Connection Failed\n");
    		continue;
    	}
    	printf("Got Connection\n");

    	if (!fork())
    	{
    		/*Child Process*/
    		//close the listening port
    		close(fd_server);
    		// clear the buffer
    		memset(buf, 0, 2048);
    		read(fd_client, buf, 2047);

    		printf("%s\n", buf);

    		if(!strncmp(buf, "GET /favicon.ico", 16)){
    			int BUFSIZE1 = 2935162;
    			char buffer_icon[BUFSIZE1];
    			fdimg = open("favicon.ico", O_RDONLY);
    			int n = read(fdimg, buffer_icon, BUFSIZE1);
    			write(fd_client, buffer_icon, n);
    			/*sendfile is optimization (on Linux), skip if not allowed*/
    			//sendfile(fd_client,fdimg, NULL, 4000);
    			close(fdimg);
    		}
    		else if(!strncmp(buf, "GET /doctest.jpg", 16)){
    			int BUFSIZE2 = 194183;
    			char buffer_image[BUFSIZE2];
    			fdimg = open("doctest.jpg", O_RDONLY);
    			int n = read(fdimg, buffer_image, BUFSIZE2);
    			write(fd_client, buffer_image, n);
    			//sendfile(fd_client,fdimg, NULL, 6000);
    			close(fdimg);
    		}
    		//send webpage to client	
    		else {
    			write(fd_client, webpage, sizeof(webpage) - 1);
    		}
    		close(fd_client);
    		printf("closing...\n");
    		exit(0);
    	}
    	/*Paraent Process*/
    	close(fd_client);
    }




} 
```