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



