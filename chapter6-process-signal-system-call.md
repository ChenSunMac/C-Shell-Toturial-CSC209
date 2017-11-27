## Process

a *process* is an instance of an executing program. When a program is executed, the kernel loads the code of the program into virtual memory, allocates space for program variables, and sets up kernel bookkeeping data structures to record various information (such as process ID, termination status, user IDs, and group IDs) about the process.

<br>

一个进程可以从逻辑上分为以下几个部分：
 - Text： Program Instructions, 参考MIPS Assembly 里的.text
 <br>
 - Data: static variables used by program, 参考Assembly里的.data
 <br>
 - Heap: area that program can dynamically allocate extra memory
<br>
- Stack: for function call, allocate storage for local variable and function call linkage information, 参考Assembly里recursion


![overViewOfProcess](/assets/overViewOfProcess.png)

Creating multiple processes can be a useful way of dividing up a task.