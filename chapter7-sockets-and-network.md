# Sockets, IPC & Network

通过pipe, 我们可以进行再processes之间的 **单向** communication, 实际上, 在unix系统里, 我们还可以通过很多其他的方式进行 Inter Process Communication (IPC):

- Pipe & named pipes (bi-directional)
- Message Queues
- Shared Memory
- Signals
- ...


通过这些我们已经可以完成对在同一台host机器上的process之间的通讯, 那么问题来了：
*How can two processes communicate across a network?*

