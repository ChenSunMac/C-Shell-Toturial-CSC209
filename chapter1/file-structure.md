## Single Dierctory Hierarchy

The kernel maintains a **single hierarchical directory structure** to organize all files in the system. \(This contrasts with operating systems such as _Microsoft Windows_, where each disk device has its own directory hierarchy.\)

Every directory contains at least two entries:

_. \(dot\)_, which is a link to the directory itself, and

_.. \(dot-dot\)_, which is a link to its parent directory, for the root directory, it links to itself.

Each process has a _**current working directory \(cwd\)**_. This is the process's "current location" within the single directory hierarchy, and it is from this directory that relative pathnames are interpreted for the process.

## File Abstraction

**Everything is a file**. 任何东西都是文件

And UNIX has unified file interface with _open, read, write, close_ methods.

#### inode

The data for each file is managed by an array of on-disk data structure called _**inodes**_.

One inode is allocated for each file and each directory.

理解inode首先要理解以下两个部分

第一是文件在硬盘上的存储，硬盘（磁盘）的最小存储单位是“扇区”（sector）, each sector store around 0.5KB;

OS在读取硬盘时，一般一次连续读取多个sector，也就是一个“块”\(block\), 一般是4KB，也就是8个sector.

第二呢，就是文件，任何文件实际都是binary code，那么他们都存储在块里 **（硬盘数据区）**

但是除了纯粹的文件内容，我们还需要知道文件的一些 **meta data（data that describe data）**，比如文件的大小，创建日期，权限等等。

那么 这些metadata的存放区域就是inode,当然也在硬盘里 **\(inode table区域\)**。

硬盘格式化的时候，操作系统自动将硬盘分成两个区域。一个是数据区，存放文件数据；另一个是inode区（inode table），存放inode所包含的信息。

**inode** 里包含了

* 文件字节数
* 拥有者id
* group id
* 读写以及执行权限
* ctime \(上次inode_change_的时间\)； mtime \(上一次内容\(manipulate\)变动的时间\); atime\(上一次文件打开的时间\)
* 链接数 （多少文件名指向这个inode）
* 文件数据block 位置

查看inode 信息



```bash
stat example.txt #查看example.txt这个文件的inode信息
ls -i #列出所在路径的文件并且显示inode号码
ls -i example.txt
#找到example.txt对应的inode
```





