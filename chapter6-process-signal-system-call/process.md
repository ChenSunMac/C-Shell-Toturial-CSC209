# Process
A **process** is an instance of an executing program. Many processes may be running the same program.
如果把CPU(承担所有的计算任务)当做一个它就像一座工厂，时刻在运行。

假定工厂的电力有限，一次只能供给一个车间使用。也就是说，一个车间开工的时候，其他车间都必须停工。背后的含义就是，单个CPU(one kernel)一次只能运行一个任务。

Process就是工厂的车间，它代表CPU所能处理的单个任务。任一时刻，CPU总是运行一个进程，其他进程处于非运行状态。
#### Program
One *program* may be used to construct many processes. 
A program is a file containing a range of information that describes how to con- struct a process at run time. 
那么程序包含了以下信息:

- Binary format identification
- Machine-language instructions

    (encode the algorithm of the program)
- Program entry-point address
- Data
- Shared-library and dynamic-linking information
- Other information

### Memory Layout of Process
The memory allocated to each process is composed of a number of parts, usually referred to as **segments**. The segments are list in the following:

![The Memory Layout of Process](/assets/typicalMemoryLayout.png)


```c
char globBuf[65536];  //uninitialized data segment
int primes[] = {2, 3, 5, 7}; //intialized data segment

int square(int x){        // Allocated in stack frame for square()
    int result;           
    result = x*x;    
    return result;        // Return value passed via register
}

int main(int argc, char *argc[]){ // stack frame for main() 
    char *p;    // stack frame for main(), wild pointer
    
    p = malloc(1024);    // Points to memory in heap segment, not wild pointer anymore
    
    exit(EXIT_SUCCESS);
}

```

### PID and getpid()

Each process has a process ID (PID), a positive integer that uniquely identifies the process on the system. 
Process IDs are used and returned by a variety of **system calls**(参见*Appendix*).
```c
pid_t getpid(void);    //pid_t is a type, can be interpreted to int
```
This call Always successfully returns **process ID of caller**
```c
pid_t getppid(void);
```
Returns process ID of **parent of caller**
### fork()
*fork()* is used to create new process.
The *fork() system call* creates a new process, the child, which is an almost exact
duplicate of the calling process, the parent.

```c
\*
- In parent: returns process ID of child on success, or –1 on error;
- In successfully created child: always returns 0
*\
pid_t fork(void); 
```

### wait()


### excurve()



