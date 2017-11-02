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

The *fork() system call* creates a new process, the child, which is an almost exact duplicate of the calling process, the parent.

```c
\*
- In parent: returns process ID of child on success, or –1 on error;
- In successfully created child: always returns 0
*\
pid_t fork(void); 
```
After the *fork()*, each process can modify the *variables in its stack, data, and heap
segments* without affecting the other process.
```c
int main(int argc, char* argv[]){
	printf("I am : %d \n", (int) getpid());
	pid_t pid = fork();
	printf("fork returned: %d \n", (int) pid);

	if (pid < 0) {
		perror ("Fork Failed");
	}
	if (pid == 0) {
		printf("I am the child with pid %d\n", (int) getpid());
		exit(0)
	}
	else if (pid > 0 ){
		printf("I am the parent : %d \n", (int) getpid() );
	}
	return 0;
}
```
***NOTE:*** Although stack, data, and heap segments are freshed, the child shares of all of the parent’s file descriptors (in text segment) **[Kernel 把这些部分标记成read-only]**

#### Race Condition after fork()
After a *fork()*, it is indeterminate which process—the parent or the child—next has access to the CPU. (On a multiprocessor system, they may both simultaneously get access to a CPU.)

The example in the code segment mentioned above may have racing. To solve the race condition, we can let the active process can send a signal after completing the action; the other process waits for the signal.
```c
int main(int argc, char* argv[]){
	printf("I am : %d \n", (int) getpid());
	pid_t pid = fork();
	TELL_WAIT();
	printf("fork returned: %d \n", (int) pid);

	if (pid < 0) {
		perror ("Fork Failed");
	}
	if (pid == 0) {
		WAIT_PARENT();  \\parent first
		printf("I am the child with pid %d\n", (int) getpid());
		exit(0)
	}
	else if (pid > 0 ){
		printf("I am the parent : %d \n", (int) getpid() );
		TELL_CHILD(pid); \\ tell child finished
	}
	return 0;
}
```

### wait()

*wait(&status)* system call has two purposes. 

- First, if a child of this process has not yet terminated by calling *exit()*, then wait() suspends execution of the process until one of its children has terminated. 

等娃儿结束

- Second, the termination status of the child is returned in the status argument of wait()

传娃儿结束的状态 (可以查看*exit()*传的状态)

```c
void doSomeWork(char *name){
	const int NUM_TIMES = 5;
	for (int i  = 0; i < NUM_TIMES; i++) {
		sleep(rand() % 4);
		printf("Done Work in %dth loop for %s \n", i, name);
	}
}

void main(int argc, char* argv[]){
	printf("I am : %d \n", (int) getpid());

	// To check process in terminal -ps -a 
	//sleep(5);
	pid_t pid = fork();

	srand((int) pid); // for rand() 

	if (pid == 0) {
		printf("I am the child with pid %d\n", (int) getpid());
		doSomeWork("Child");
		// wait 233
		exit(233);
	} 

	printf("I am the parent, waiting for child to end\n");
	doSomeWork("Parent");
	// the wait() function returns child pid
	pid_t childpid = wait(NULL);
	printf("Parent Knows the child %d finished\n", (int) childpid);

	int status = 0;
	pid_t childpid = wait(&status);
	printf("Parent Knows the child %d finished with status %d\n", (int) childpid, status);
	// check the value passed by exit() -- 233
	int childReturnValue = WEXITSTATUS(status);
	printf("	Return Value was %d\n", (int) childReturnValue);
}
```

### exec()
*exec()* is a set of a bunch of functions. They generally loads a new program into a process's memory, The existing program text is discarded, and the *stack, data, and heap segments* are freshly created for the new program. This enables a the processes generated by *fork()* to execute different functions. 

- *execve(pathname, argv, envp)* system call loads a new program (pathname,
with argument list argv, and environment list envp) into a process's memory.


***NOTE:*** Although stack, data, and heap segments are freshed, the child shares of all of the parent’s file descriptors (in text segment) **[Kernel 把这些部分标记成read-only]**
 
