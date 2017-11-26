# Socket Programming


## socket() - 你好，我是个插孔，这是我的fd，来插这儿
In a typical client-server scenario, applications communicate using sockets as follows:

* 每一个需要通讯的application都创造并拥有一个socket，这个socket是通讯的接口，就好比手机
* Server binds its socket to a well-known address\(name\) so client can locate it, 就好比你要去打110\(911\)电话

A socket is created using the socket\(\) system call, which returns a file descriptor used  
to refer to the socket:

```c
fd = socket(domain, type, protocol);
```

以上有三个Variable field, 我们逐一分析一下

### Domain
Sockets exist in a **communication domain**, which determines:

- the method of identifying a socket (i.e., the format of a socket “address”); 
- the range of communication (i.e., either between applications on the same host
or between applications on different hosts connected via a network).

| Domain | Communication Performed | Address Format | address Structure |
| :--- | :--- |:--- |:--- |
| AF_UNIX | within Kernel, same host  |pathname | *sockaddr_un*|
| AF_INET | Via IPv4 | 32-bit IPv4 address + 16-bit port number | *sockaddr_in*|
| AF_INET6 | Via IPv6 | 128-bit IPv6 address + 16-bit port number | *sockaddr_in6*|


### Socket Types
Socket types are supported in both the UNIX and the Internet domains. 
类比一下, 220V 和 110V都插座都是插座, 只是接的功率不一样, 在这里简单的把Socket Type 分为两类:
1. Stream (SOCK_STREAM)
    + reliable
    + bidirectional
2. Datagram sockets(SOCK_DGRAM)
    + data transmission not reliable

### Protocal
一般都是0 （need to add stuff）..

### Conclusion socket()

**socket()**创建了一个插孔**listener fd**专门用来执行**bind()**以及监听。


---
## bind() 你好，你插的是这儿，对就是这儿

```c
int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```
**bind()** 把**sockfd**以及给定的 *sockaddr* 绑定起来了。
也就是说这是一个把*无名socket*和**有名的地址**绑定起来的命令。

```c
struct sockaddr {
}
```

### getsockname()

---
## connect() 你好，我想插你



## listen() 听说有人想搞朕
```c
int listen(int sockfd, int backlog); 
// return 0 on success, or -1 on error
```
1. We can’t apply listen() to a connected socket—that is, a socket on which a connect() has been successfully performed or a socket returned by a call to accept(). 


2. backlog used for handling pending connection (when server is accepting other clients)

简而言之， 监听listener socket（not connected），并且用backlog去limit pending connections

---

## accept() 好的，知道了，咱俩去那儿搞
```c
int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
// return new fd on success, -1 on error
```
**accept()** create *new scoket*, and this new socket is connected to the *peer socket* that performed the **connect()**.

*addr* points to a structure taht is used to return the socket address (of peer socket).

- we can set *addr* and *addrlen* to NULL and 0 if we are not interested in the address of the peer socket

### getpeername()

Retrieve the peer's address later using the getpeername() system call



