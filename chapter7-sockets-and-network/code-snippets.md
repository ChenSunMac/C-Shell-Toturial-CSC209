```c
struct sockaddr_in{
    sa_family_t sin_family;
    unsigned short int sin_port;
    struct in_addr sin_addr;
    unsigned char pad[8]; /*UNUSED*/
}
```