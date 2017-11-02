# Process
A **process** is an instance of an executing program. Many processes may be running the same program.

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
Process IDs are used and returned by a variety of **system calls**.
```c
pid_t getpid(void);    //pid_t is a type, can be interpreted to int
```

### fork()




