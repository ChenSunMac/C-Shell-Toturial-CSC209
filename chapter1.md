# Unix, File Structure, Permission

UNIX 是在1969年的BELL实验室（AT&T的一部分）诞生的，硬件平台是Digital PDP-7 minicomputer (With a cost of US$72,000). 
![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Pdp7-oslo-2005.jpeg/300px-Pdp7-oslo-2005.jpeg)

随后由于一系列原因，UCB成为了研究和开发UNIX的主力军，1979年时，UCB已经完成UNIX一个分支的开发，BSD.

Two different currents led to the development of (GNU/) Linux. One of these was the GNU project, founded by Richard Stallman. By the late 1980s, the GNU project had produced an almost complete, freely distributable UNIX implementation. The one part lacking was a working kernel. In 1991, inspired by the Minix kernel written by Andrew Tanenbaum, Linus Torvalds produced a working UNIX kernel for the Intel x86-32 architecture.


但是这些不同的Braches以及开源所带来的问题就是portability problems, (即使现在，笔者也曾经因为在linux上安装驱动兼容等问题二头疼不已)。 

The C language was standardized in 1989 (C89), and a revised standard was produced in 1999 (C99).

The first attempt to standardize the operating system interface yielded POSIX.1, ratified as an IEEE standard in 1988, and as an ISO standard in 1990.

Linux separates implementation from distribution. Consequently, there is no single “official” Linux distribution. Each Linux distributor’s offering consists of a snapshot of the current stable kernel, with various patches applied.

---
## Kernel
Kernel in UNIX is more like the core Operating System - the central software that manages and allocates computer resources (i.e., the CPU, RAM, and devices).
### Tasks performed by Kernel
 - Process Scheduling
The Definition of Process will be discussed under File I/O section

  (***preemptive multitasking*** operating system)
    + preemptive means the rules governing which processes receive use of the CPU and for how long are determined by the kernel process scheduler, rahter than processes themselves
    + Multitasking means that multiple processes can simultaneously reside in memory and each may receive use of the CPU

 - Memory Management

     + Linux employs virtual memory management, a technique confers 2 main advantages 
  
    + processes are isolated from each other and the kernel, 一个独立的进程不能 read or modify another process or Kernel  
    + increases the likelihood that, at any moment in time, there is at least one process that the CPU(s) can execute.

 - file system

 - Access to devices

   The kernel provides programs with an interface that standardizes and simplifies access to devices, while at the same time arbitrating access by multiple processes to each device.

- Networking

  
- **system call application programming interface (API)**:

  + Processes can request the kernel to perform various tasks using kernel entry points known as system calls.