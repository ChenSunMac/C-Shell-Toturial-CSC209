# Socket

In a typical client-server scenario, applications communicate using sockets as follows:

- 每一个需要通讯的application都创造并拥有一个socket，这个socket是通讯的接口，就好比手机
- Server binds its socket to a well-known address(name) so client can locate it, 就好比你要去打110(911)电话

A socket is created using the socket() system call, which returns a file descriptor used
to refer to the socket:
```c
fd = socket(domain, type, protocol);
```