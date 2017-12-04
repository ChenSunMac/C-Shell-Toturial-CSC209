# Variable

### 赋值
在shell 里面赋值用"="，但是要注意不能有空格，VAR=value是OK的，因为shell识别到"="以后就会执行赋值操作; 但是VAR = value不行，因为shell会认为VAR是一个程序从而去寻找相应的同名程序来执行
```bash
MY_MESSAGE="Hello World"
variable=value
variable='value'
variable="value"
echo $MY_MESSAGE
```
- 如果 value 包含了空白符，那么就必须使用引号包围起来。
- 单引号： 原样输出，里面是什么就是什么
- 双引号： 解析输出，先解析变量名和命令
 
```
nuts="NUTS!!!"
var1='JOJO:${nuts}'
var2="JOJO:${nuts}"
echo $var1
echo $var2
```
 
The shell does not care about types of variables; they may store strings, integers, real numbers - anything you like. (但实际上还是以string的形式存储的)

```bash
# like printf() in C
MYVAR="BIZZARE ADVENTURE"
echo "JOJOs: $MYVAR"
```

- 声明变量不用$, 调用变量得用$
- 以上是显式赋值(Explicitly),本篇文末还有隐式赋值的介绍


最后如果希望删除变量，我们可以：
```sh
unset variable_name
```

---
### Some Special Vairables

首先我们来看看带数字类的保留的变量：**$0, $1, .. $9**
- The variable **$0** is the basename of the program as it was called (相当于**argv[0]**)
- **$1 .. $9** are the first 9 additional parameters the script was called with(相当于**argv[1]**, **argv[2]**,...)

另外还有几个符号类型的保留变量：**$@, $* $#**
- **$@** is all parameters **$1 .. whatever** (除了**$0**以外所有的数字型, 所有argument), 相当于**argv**
- **$***  is similar to **$@** only **$*** does not preserve white space (As a general rule, use **$@** and avoid **$***)
- **$#** is the number of parameters the script was called with **argc**

```bash
#!/bin/sh
echo "I was called with $# parameters" 
echo "My name is $0"
echo "My first parameter is $1"
echo "My second parameter is $2"
echo "All parameters are $@"
```

---
除了以上这些和当前run的环境相关的variables以外，还有
- **$?** contains the exit value of the last run command
- **$$** is the PID (Process IDentifier) of the currently running shell
- **$!** is the PID of the last run background process

一般debug复杂程序的时候可以用

```bash
#!/bin/sh
/usr/test_Dir/test_program
if [ "$?" -ne "0" ]; then
  echo "Sorry, we had a problem there!"
fi
```

---
# Wild Cards

 - The asterisk character (*****, also called "star") matches zero or more characters
 
 For example, **doc*** matches **doc** and **document** but not **dodo**. 一切皆有可能
 
 - The question mark ? matches exactly one character.

For example the pattern **123?** will match **123** and **1234**, but not **12345**. 一个皆有可能

- ranges of characters enclosed in square brackets (**[ and ]**) match a single character within the set

For example, **[A-Za-z]** matches any single uppercase or lowercase letter

---
# Command in Shell

我们还可以再shell里面直接使用shell command 从而得到隐式赋值：
有两种等价的形式：
```sh
variable=`command`
variable=$(command)
longFileList=`ls -l`
date=`date +%H:%M:%S`
```






