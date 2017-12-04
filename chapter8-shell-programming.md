
# Why Shell Script

- Shell script can take input from user, file and output them on screen.
- Save lots of time.
- To automate some task of day today life.
- System Administration part can be also automated.

For example:
```bash
#!/bin/sh                  # 指定脚本解释器，这里是用/bin/sh做解释器的
cd ~                       # 切换到当前用户的home目录
mkdir shell_tut            # 创建一个目录shell_tut
cd shell_tut               # 切换到shell_tut目录
                
for ((i=0; i<10; i++)); do  # 循环条件，一共循环10次
    touch test_$i.txt       # 创建一个test_1…10.txt文件
done                        # 循环体结束
```

cd, mkdir, touch都是系统自带的程序，一般在/bin或者/usr/bin目录下。for, do, done是sh脚本语言的关键字。
```bash
#!/usr/bin/perl    # for perl script
#!/usr/bin/python  # for python script 
```
## Philosophy

- 脚本用的永远比写的多
- 读的永远比用的多

So try to be as **clear** and **efficiency** as possible.


执行shell 很简单，只需要
```sh
sh filename.sh
```