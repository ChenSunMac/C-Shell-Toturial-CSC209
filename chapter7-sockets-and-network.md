# Sockets, IPC & Network

通过pipe, 我们可以进行再processes之间的 **单向** communication, 实际上, 在unix系统里, 我们还可以通过很多其他的方式进行 Inter Process Communication (IPC):

- Pipe & named pipes (bi-directional)
- Message Queues
- Shared Memory
- Signals
- ...


通过这些我们已经可以完成对在同一台host机器上的process之间的通讯, 那么问题来了：
*How can two processes communicate across a network?*
## Sockets (套接字)

Socket是计算机之间进行通信的一种约定或一种方式。通过 socket 这种约定，一台计算机可以接收其他计算机的数据，也可以向其他计算机发送数据。

**Socket** is an end point of communication between two systems on a network. 

To be a bit precise, a socket is a **combination of IP address and port on one system**. 

So on each system a socket exists for a process interacting with the socket on other system over the network.

简单来说, 通过Sockets, 我们能够实现关于不同applications在同一个甚至不同host上的交流

## Internet Model and Protocals

There are two types of network communication models:
- OSI
- TCP/IP

While *OSI* is more of a theoretical model, the **TCP/IP** networking model is the most popular and widely used.

