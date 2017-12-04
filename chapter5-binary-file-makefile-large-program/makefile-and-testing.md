# Makefile

It is a road map from .c and .h to .o and .exe.


makefile是用来告诉make命令如何编译和链接这几个文件。我们的规则是：
1）如果这个工程没有编译过，那么我们的所有c文件都要编译并被链接。
2）如果这个工程的某几个c文件被修改，那么我们只编译被修改的c文件，并链接目标程序。
3）如果这个工程的头文件被改变了，那么我们需要编译引用了这几个头文件的c文件，并链接目标程序。

```makefile
target ... : prerequisites ...
	command
	...
	...
```


# Testing with make

当程序写好了希望用make来做项目的测试，那么我们希望make当中就应该有那么一个target 比如说是testSomething来做目标，然后出一个program.exe什么的：
```
testSomething :
	program.exe
```
再进阶一点呢，我们甚至可以用
```
testSomething :
	program.exe < input.txt > output.txt
	diff correct.txt output.txt
```

References: [http://www.cs.toronto.edu/~penny/teaching/csc444-05f/maketutorial.html](http://www.cs.toronto.edu/~penny/teaching/csc444-05f/maketutorial.html)