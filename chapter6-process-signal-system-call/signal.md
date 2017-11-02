# Signal Concepts
A signal is a **notification to a process** that an event has occurred. Signals are sometimes described as software interrupts. Signals are analogous to hardware interrupts in that they interrupt the normal flow of execution of a program; in most cases, it is not possible to predict exactly when a signal will arrive.

Signal may be sent to a process by the kernel, by another process, or by itself. There is a range of standard signal types, each of which has a unique number and purpose.

### kill()

One process can send a signal to another process using the *kill()* system call, which is the analog of the *kill* shell command.
```c
int kill(pid_t pid, int sig); //Returns 0 on success, or –1 on error
```