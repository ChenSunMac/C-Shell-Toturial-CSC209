# C环境配置
在大部分电脑上，我们只需要 **文本编辑器** 和 **C编译器** 就可以开始玩儿C啦。

常用的文本编辑器有：
- Notepad
- OS Edit command
- Brief
- Epsilon
- EMACS 
- vim/vi
- Sublime Text
- atom
...

除了上述编辑器以外，还可以直接使用各类IDE
- Visual Studio
- Eclipse
...

## C 编译器 （Compiler）
写在源文件中的源代码是人类可读的源。它需要"编译"，转为机器语言，这样 CPU 可以按给定指令执行程序, 最常用的免费可用的编译器是 GNU 的 C/C++ 编译器

### Linux

Check GNU-GCC version by
```sh
gcc -v
```

如果未安装 GCC，那么请按照 http://gcc.gnu.org/install/ 上的详细说明安装 GCC


### Mac
下载Xcode： developer.apple.com/technologies/tools/ 

### Windows
安装 MinGW， 访问 MinGW 的主页 www.mingw.org，进入 MinGW 下载页面，下载最新版本的 MinGW 安装程序
添加安装的 MinGW 的 bin 子目录到 PATH 环境变量中