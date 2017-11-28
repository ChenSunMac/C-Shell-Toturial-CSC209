# Variable

### 赋值
在shell 里面赋值用"="，但是要注意不能有空格，VAR=value是OK的，因为shell识别到"="以后就会执行赋值操作; 但是VAR = value不行，因为shell会认为VAR是一个程序从而去寻找相应的同名程序来执行
```bash
MY_MESSAGE="Hello World"
echo $MY_MESSAGE
```

The shell does not care about types of variables; they may store strings, integers, real numbers - anything you like. (但实际上还是以string的形式存储的)

```bash
# like printf() in C
MYVAR="JOJOs BIZZARE ADVENTURE"
echo "MYVAR is: $MYVAR"
```

### Some Special Vairables

首先我们来看看带数字类的保留的变量：**$0, $1, .. $9**