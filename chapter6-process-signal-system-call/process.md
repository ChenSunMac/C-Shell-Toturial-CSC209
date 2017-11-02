# Process
A **process** is an instance of an executing program. Many processes may be running the same program.
如果把CPU(承担所有的计算任务)当做一个它就像一座工厂，时刻在运行。

假定工厂的电力有限，一次只能供给一个车间使用。也就是说，一个车间开工的时候，其他车间都必须停工。背后的含义就是，单个CPU(one kernel)一次只能运行一个任务。

Process就是工厂的车间，它代表CPU所能处理的单个任务。任一时刻，CPU总是运行一个进程，其他进程处于非运行状态。

一个车间里，可以有很多工人。他们协同完成一个任务。线程就好比车间里的工人。一个进程可以包括多个线程。车间的空间是工人们共享的，比如许多房间是每个工人都可以进出的。这象征一个进程的内存空间是共享的，每个线程都可以使用这些共享内存。

可是，每间房间的大小不同，有些房间最多只能容纳一个人，比如厕所。里面有人的时候，其他人就不能进去了。这代表一个线程使用某些共享内存时，其他线程必须等它结束，才能使用这一块内存。

一个防止他人进入的简单方法，就是门口加一把锁。先到的人锁上门，后到的人看到上锁，就在门口排队，等锁打开再进去。这就叫"互斥锁"（Mutual exclusion，缩写 Mutex），防止多个线程同时读写某一块内存区域。

还有些房间，可以同时容纳n个人，比如厨房。也就是说，如果人数大于n，多出来的人只能在外面等着。这好比某些内存区域，只能供给固定数目的线程使用。

这时的解决方法，就是在门口挂n把钥匙。进去的人就取一把钥匙，出来时再把钥匙挂回原处。后到的人发现钥匙架空了，就知道必须在门口排队等着了。这种做法叫做"信号量"（Semaphore），用来保证多个线程不会互相冲突。

不难看出，mutex是semaphore的一种特殊情况（n=1时）。也就是说，完全可以用后者替代前者。但是，因为mutex较为简单，且效率高，所以在必须保证资源独占的情况下，还是采用这种设计。
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



