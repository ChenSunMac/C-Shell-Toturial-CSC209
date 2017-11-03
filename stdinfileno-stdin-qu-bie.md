STDIN_FILENO, STDOUT_FILENO, stdin, stdout 都是Interface的接口，他们的用法和区别又是啥呢？

## STDIN_FILENO, STDOUT_FILENO

STDIN_FILENO, STDOUT_FILENO 的接口比较低级，他们实际上只是file descriptor, 属于 int 类型

- STDIN_FILENO = 0
- STDOUT_FILENO = 1
- STDERR_FILENO  = 2

使用STDIN_FILENO的函数有：read、write、close等
