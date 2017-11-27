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
#查看example.txt这个文件的inode信息
stat example.txt 

#列出所在路径的文件并且显示inode号码
ls -i 

#找到example.txt对应的inode
ls -i example.txt 
```


每个inode节点的大小，一般是128字节或256字节。inode节点的总数，在格式化时就给定，一般是每1KB或每2KB就设置一个inode。假定在一块1GB的硬盘中，每个inode节点的大小为128字节，每1KB就设置一个inode，那么inode table的大小就会达到128MB，占整块硬盘的12.8%.

```bash
# Disk space being used by File systems 查看每个硬盘分区的inode总数和已经使用的数量
df -i
```
系统内部这个过程分成三步：首先，系统找到这个文件名对应的inode号码；其次，通过inode号码，获取inode信息；最后，根据inode信息，找到文件数据所在的block，读出数据。

---
### HARD link and SOFT link 文件名与inode 分离的UNIX世界 

Unix/Linux系统允许，多个文件名指向同一个inode号码。

这意味着，可以用不同的文件名访问同样的内容；对文件内容进行修改，会影响到所有文件名；但是，删除一个文件名，不影响另一个文件名的访问。这种情况就被称为"硬链接"（hard link）。
![](/assets/inode1.png)
```bash
# create hard LiNk to files
ln file1.txt file2.txt 
```

创建目录时，默认会生成两个目录项："."和".."。前者的inode号码就是当前目录的inode号码，等同于当前目录的"硬链接"；后者的inode号码就是当前目录的父目录的inode号码，等同于父目录的"硬链接"。所以，任何一个目录的"硬链接"总数，总是等于2加上它的子目录总数（含隐藏目录）。
![](/assets/inode2.png)
文件A和文件B的inode号码虽然不一样，但是文件A的内容是文件B的路径。读取文件A时，系统会自动将访问者导向文件B。因此，无论打开哪一个文件，最终读取的都是文件B。这时，文件A就称为文件B的"软链接"（soft link）或者"符号链接（symbolic link）。 这个和shortcut很像

```bash
#create -soft LiNk to files
ln -s sourceFile1.txt linkfile.txt 
```

打开一个文件以后，系统就以inode号码来识别这个文件，不再考虑文件名。因此，通常来说，系统无法从inode号码得知文件名，但是可以从inode知道owner。
