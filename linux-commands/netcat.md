# NetCat

NetCat能通过TCP和UDP在网络中读写数据, 他所做的就是在两台电脑之间建立链接并返回两个数据流，在这之后所能做的事就看你的想像力了。你可以通过netcat建立一个服务器，传输文件，与朋友聊天，传输流媒体等等。

NETCAT 基本功能有：

* connect somewhere: nc \[options\] \[hostname\] port \[port\]
* listen for connection: nc -l \[options\] \[port\]

```
nc -h # HELP information for nc
```

### 利用netcat 实现chat server

```
nc -l 1234  # server end open listener on port 1234
nc localhost 1234 # client end
```

假设我们通过ifconfig（linux）命令 或者 ipconfig（windows）命令获取我们本机网卡的ip为 192.168.0.3，那么client端可以直接连我们的网络IP：

```
nc 192.168.0.3 1234
```

### 利用 netcat 实现文件传输



