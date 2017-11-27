# Pipe

A **pipe** is a _system call_ that creates a **unidirectional** communication link between two file descriptors.

建立pipe可以让两个进程进行单方向通信。

```
SYSTEM CALL: pipe();                                                          

  PROTOTYPE: int pipe( int fd[2] );                                             
    RETURNS: 0 on success                                                       
             -1 on error: errno = EMFILE (no free descriptors)                  
                                  EMFILE (system file table is full)            
                                  EFAULT (fd array is not valid)                

  NOTES: fd[0] is set up for reading, fd[1] is set up for writing
```
---
- Pipe is a byte stream:
    + The process reading from a pipe can read blocks of data of any size， regardless of the size of blocks written by the writing process
    + The data passes through the pipe sequentially in byte (**not possible to use lseek()**)

- Pipe is *unidirectional*

***NOTE***:
Attempts to read from a pipe that is currently empty **block** until at least one byte has been written to the pipe. If the write end of a pipe is closed, then a process reading from the pipe will see end-of-file (i.e., read() returns 0) once it has read all remaining data in the pipe

---
### Example \(Pipe in One Process\)

The array of two file descriptors is **fd\[2\]**. Whatever is written to **fd\[1\]** will be read from **fd\[0\]**.

```c
int main(int argc, char **argv)
{
    int n;
    int fd[2];
    char buf[1025];
    char *data = "hello... this is sample data";

    pipe(fd);
    write(fd[1], data, strlen(data));
    if ((n = read(fd[0], buf, 1024)) >= 0) {
        buf[n] = 0;    /* terminate the string */
        printf("read %d bytes from the pipe: \"%s\"\n", n, buf);
    }    
    else
        perror("read");
    exit(0);
}
```
![](/assets/pipe1.png)
### Example \(Pipe between Parent and Child\)


Following list the steps for creating a pipe to transfer data from a parent to a child:
```c
int filedes[2];
if (pipe(filedes) == -1) /* Create the pipe */
    errExit("pipe");
switch (fork()) { /* Create a child process */
    case -1:
        errExit("fork");
    case 0: /* Child */
        if (close(filedes[1]) == -1) /* Close unused write end */
            errExit("close");
        /* Child now reads from pipe */
        break;
    default: /* Parent */
        if (close(filedes[0]) == -1) /* Close unused read end */
            errExit("close");
        /* Parent now writes to pipe */
        break;
}
```



![](/assets/pipe2.png)


***NOTE***:
Tt is **not usual** to have both the parent and child reading from a single pipe is that if two processes try to simultaneously read from a pipe, we can’t parent process be sure which process will be the first to succeed—the two processes race for data.










