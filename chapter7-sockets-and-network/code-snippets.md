```c
struct sockaddr_in{
    sa_family_t sin_family;
    unsigned short int sin_port;
    struct in_addr sin_addr;
    unsigned char pad[8]; /*UNUSED*/
}
```
---
### Server setups:
```c
struct sockaddr_in r;
if ((listenfd = socket(AF_INET, SOCK_STREAM, 0)) < 0) {
    perror("socket");
    exit(1);
}
memset(&r, '', sizeof r);
r.sin_family = AF_INET;
r.sin_addr.s_addr = htonl(INADDR_ANY);
r.sin_port = htons(port);
if (bind(listenfd, (struct sockaddr *)&r, sizeof r)) {
    perror("bind");
    exit(1);
}
if (listen(listenfd, 5)) {
    perror("listen");
    exit(1);
}
```

---
### Accept connection:
```c
int fd;
struct sockaddr_in r;
socklen_t socklen = sizeof r;
if ((fd = accept(listenfd, (struct sockaddr *)&r, &socklen)) < 0) {
    perror("accept");
    /* exit or do some thing else */
}
```

---
### Client Setup
```c
const char* ipaddr="...";
int soc;
char buf[256];
struct hostent *hp;
struct sockaddr_in peer;
peer.sin_family = PF_INET;
peer.sin_port = htons(PORT);
/* fill in peer address */
hp = gethostbyname(ipaddr);
if ( hp == NULL ) {
    fprintf(stderr, "%s: %s unknown host\n",
        argv[0], argv[1]);
    exit(1);
}
peer.sin_addr = *((struct in_addr *)hp->h_addr);
/* create socket */
if((soc = socket(PF_INET, SOCK_STREAM, 0)) == -1) {
    perror("socket");
}
/* request connection to server */
if (connect(soc, (struct sockaddr *)&peer, sizeof(peer)) == -1) {
    perror("client:connect"); close(soc);
    exit(1);
}
```

