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

NEED to EDIT
-----------------

---
## bind() 你好，你插的是这儿，对就是这儿




## connect() 你好，我想插你



## listen() 听说有人想搞朕