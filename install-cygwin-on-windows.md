## 在Windows上安装Cygwin

在Windows上使用unix环境的方法有很多，比如今天介绍的通过Cygwin提供完整的类Unix模拟环境，也可以选择使用Win10的Developer Mode的Linux Subsystem，同样也可以直接安装虚拟机。

在视频录制的这个世界线里，与 UNIX shell 相比，Windows COMMAND 实用程序的功能并不是特别的好，通过Cygwin在 Windows 环境中提供给UNIX开发人员一片熟悉的天地，就像是中国人在美国找到了中餐馆。

在本节教程里，我们要教大家如何在Windows上安装并使用 Cygwin

### 安装Cygwin

访问 [https://cygwin.com/install.html](https://cygwin.com/install.html) 下载Cygwin 安装程序

安装程序本身非常小（大约 600KB），因为大多数 Cygwin 软件是在安装过程中下载的

在大多数情况下，推荐的安装选项是合适的，也可以进行定制，但是要注意几点：

* **不要在 Windows 系统的根目录（比如 C:）中安装 Cygwin。**
  最好把 Cygwin 安装在它自己的子目录中，比如默认目录（C:\cygwin）或 C:\Program Files\cygwin。（您选择的目标目录将成为模拟的 UNIX 环境的根目录`/`。例如，如果在 C:\cygwin 中安装，那么虚拟的 /usr/bin 实际上是 C:\cygwin\usr\bin） 。
* 对于**Install For**选项，不要选择**Just Me**。
* 把**Default Text File**类型设置为**Unix**，从而尽可能提高与其他 UNIX 机器上存储的现有文件的兼容性

选择完镜像以后，安装程序就会显示可用的类别和包的完整列表：

单击加号展开对应的类别；单击 “循环” 标志在 Skip（忽略此包）和包的所有可用版本之间循环，顺便说一下，如果选择 B 列，就会下载二进制包；选择 S，也会下载源代码



为了使我们安装的Cygwin能够编译程序，我们需要安装gcc编译器，默认情况下，gcc并不会被安装，我们需要选中它来安装。为了安装gcc，我们用鼠标点开组件列表中的“Devel”分支，在该分支下，有很多组件，我们必须的是：

**binutils   
gcc   
gcc-mingw   
gdb**

### 验证安装与使用

cygcheck -c cygwin

会打印出当前cygwin的版本和运行状态，如果status是ok的话，则cygwin运行正常。

依次输入gcc –version，g++ --version，make –version，gdb –version进行测试，如果都打印出版本信息和一些描述信息，非常高兴的告诉你，你的cygwin安装完成了！

### 结语

Cygwin 并不是完美的 UNIX 模拟环境，但已经相当好了。



