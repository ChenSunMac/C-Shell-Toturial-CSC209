![](/assets/File_table_and_inode_table.png)

STDIN_FILENO, STDOUT_FILENO, stdin, stdout 都是Interface的接口，他们的用法和区别又是啥呢？

## STDIN_FILENO, STDOUT_FILENO

STDIN_FILENO, STDOUT_FILENO 的接口比较低级，他们实际上只是file descriptor, 属于 int 类型

```c
/* In /usr/include/unistd.h */
/* Standard file descriptors. */
#define STDIN_FILENO 0 /* Standard input. */
#define STDOUT_FILENO 1 /* Standard output. */
#define STDERR_FILENO 2 /* Standard error output. */
```
- STDIN_FILENO = 0
- STDOUT_FILENO = 1
- STDERR_FILENO  = 2

使用STDIN_FILENO的函数有：open, read, write, close等

```c
#include<unistd.h>
#define SIZE 10

int main(void)
{
        int n;
        char buf[SIZE];
        //读取标准输入到buf中，返回读取字节数。
        while(n=read(STDIN_FILENO,buf,SIZE)){   
                if(n!=write(STDOUT_FILENO,buf,n)){ 
                        perror("write error");//把buf 写到标准输出中
                }
        }
        if(n<0) perror("read error");   
        return 0;
}
```