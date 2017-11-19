```c
struct sockaddr_in{
    sa_family_t sin_family;
    unsigned short int sin_port;
    struct in_addr sin_addr;
    unsigned char pad[8]; /*UNUSED*/
}
```

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