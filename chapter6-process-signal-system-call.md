## Process

a *process* is an instance of an executing program. When a program is executed, the kernel loads the code of the program into virtual memory, allocates space for program variables, and sets up kernel bookkeeping data structures to record various information (such as process ID, termination status, user IDs, and group IDs) about the process.

<br>

一个进程可以从逻辑上分为以下几个部分：
 - Text： Program Instructions, 参考MIPS Assembly 里的.text

 - Data: static variables used by program, 参考Assembly里的.data

 - Heap: area that program can dynamically allocate extra memory

- Stack: for function call, allocate storage for local variable and function call linkage information, 参考Assembly里recursion


### Process creation and program execution
A process can create a new process using the *fork()* system call. （实际上是Process用fork()对kernel进行system call，然后kernel创建了新的Process）

The process that calls fork() is referred to as the parent process, and the new process is referred to as the child process.

The **child process** goes on either to execute a different set of functions in the same code as the parent, or, frequently, to use the *execve()* system call to load and execute an entirely new program. An *execve()* call destroys the existing text, data, stack, and heap segments, replacing them with new segments based on the code of the new program.

Each process has a unique ***integer process identifier (PID)***. Each process also has a **parent process identifier (PPID)** attribute, which identifies the process that requested the kernel to create this process.


## Interprocess Communication and Synchronization

Linux and Unix provide rich set of mechanisms for ***interprocess communication (IPC)***:

- *signals*: to indicate that an event has occurred;  Think it as ***Software Interrupt***

- *Pipes*: to transfer data between processes;

- *Sockets*: to transfer data from one process to another;

- *file locking*: allows a process to lock regions of a file in order to prevent other processes from reading or updating the file contents

- *message queues*: exchange messages (packets of data) between processes;

- *semaphores*: synchronize the actions of processes

- *shared memory*: Allows 2 or more processes to share a piece of memory


![overViewOfProcess](/assets/overViewOfProcess.png)

Creating multiple processes can be a useful way of dividing up a task.