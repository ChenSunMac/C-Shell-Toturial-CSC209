# Select() 谁有空呢

**select()** system call blocks until one or more of a set of file descriptors becomes
ready.



```c
int select(int nfds, fd_set *readfds, fd_set *writefds, fd_set *exceptfds, struct timeval *timeout);
// Returns number of ready file descriptors, 0 on timeout, or –1 on error
```