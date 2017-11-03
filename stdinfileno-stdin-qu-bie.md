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

## stdin, stdout, stderr

stdin类型为 FILE* , 也就是stream:
```c
/* /usr/include/stdio.h */
/* Standard streams.  */
extern struct _IO_FILE *stdin;          /* Standard input stream.  */
extern struct _IO_FILE *stdout;         /* Standard output stream.  */
extern struct _IO_FILE *stderr;         /* Standard error output stream.  */
```

对应的函数前面都有f开头，如fopen, fread, fwrite, fclose 标准库调用等


## 简单的类比
也就是说STDIN_FILENO, STDOUT_FILENO 是低级的接口，可以把它们看做是手机号码，在计算机系统里，只要知道STDIN_FILENO, STDOUT_FILENO标记的数字(int), 那么就可以知道对应的文件。就跟咱们打电话，只要输入号码，就可以知道整个移动网络里对应的那个手机终端。

而stdin之类的是更高级的接口，更像是对这个手机的整个接口，好比拿手机去扫蓝牙/插USB.

