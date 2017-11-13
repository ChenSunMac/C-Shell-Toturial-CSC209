# Sockets, IPC & Network

通过pipe, 我们可以进行再processes之间的 **单向** communication, 实际上, 在unix系统里, 我们还可以通过很多其他的方式进行 Inter Process Communication \(IPC\):

* Pipe & named pipes \(bi-directional\)
* Message Queues
* Shared Memory
* Signals
* ...

通过这些我们已经可以完成对在同一台host机器上的process之间的通讯, 那么问题来了：  
_How can two processes communicate across a network?_

## Sockets \(套接字\)

Socket是计算机之间进行通信的一种约定或一种方式。通过 socket 这种约定，一台计算机可以接收其他计算机的数据，也可以向其他计算机发送数据。

**Socket** is an end point of communication between two systems on a network.

To be a bit precise, a socket is a **combination of IP address and port on one system**.

So on each system a socket exists for a process interacting with the socket on other system over the network.

简单来说, 通过Sockets, 我们能够实现关于不同applications在同一个甚至不同host上的交流

## Internet Model and Protocols

There are two types of network communication models:

* OSI
* TCP/IP

While _OSI_ is more of a theoretical model, the **TCP/IP** networking model is the most popular and widely used.

| Layer Name | Protocol | Address |
| --- | :---: | ---: |
| Application | Telnet, SSH | Hostname |
|  | E-mail | user@domain |
|  | Web Browser | URL, http:... |
| Transport  Layer | Transmission Control Protocol  or  User Datagram Protocol | Port Numbers |
| Internet Layer | Internet Protocol, routing | IP Address |
| Link Layer | Network Interface Device : FastEthernet, GigE, WiFi \(802.11a, b, g, n\) | MAC Address |

![The application on each host executes read and write operations as if the processes were directly connected to each other by some kind of data pipe. Every other detail of the communication is hidden from each process. ](/assets/IP_diagram.png)
The application on each host executes read and write operations as if the processes were directly connected to each other by some kind of data pipe. Every other detail of the communication is hidden from each process.

![Encapsulation of application data descending through the layers](/assets/data_IP.png)

Encapsulation of application data descending through the layers

我们可以看到IP协议对应于网络层，TCP协议对应于传输层，而HTTP协议对应于应用层;
然而Socket又是啥呢？

socket是对TCP/IP协议的封装和应用（程序员层面上）

socket是对TCP/IP协议的封装，Socket本身并不是协议，而是一个调用接口（API），通过Socket，我们才能使用TCP/IP协议

Socket的出现只是使得程序员更方便地使用TCP/IP协议栈而已，是对TCP/IP协议的抽象，从而形成了我们知道的一些最基本的函数接口，比如create、listen、connect、accept、send、read和write等等

网络上有一个简单的类比： 
- HTTP是轿车，提供了封装或者显示数据的具体形式；
- Socket是发动机，提供了网络通信的能力。

就好比底层的硬件实现了电脑，然而具体的操作还是需要程序员编的OS 和其他程序
