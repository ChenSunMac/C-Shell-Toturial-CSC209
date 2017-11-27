# Unix, File Structure, Permission

UNIX 是在1969年的BELL实验室（AT&T的一部分）诞生的，硬件平台是Digital PDP-7 minicomputer (With a cost of US$72,000). 
![](https://upload.wikimedia.org/wikipedia/commons/thumb/5/52/Pdp7-oslo-2005.jpeg/300px-Pdp7-oslo-2005.jpeg)

随后由于一系列原因，UCB成为了研究和开发UNIX的主力军，1979年时，UCB已经完成UNIX一个分支的开发，BSD.

Two different currents led to the development of (GNU/) Linux. One of these was the GNU project, founded by Richard Stallman. By the late 1980s, the GNU project had produced an almost complete, freely distributable UNIX implementation. The one part lacking was a working kernel. In 1991, inspired by the Minix kernel written by Andrew Tanenbaum, Linus Torvalds produced a working UNIX kernel for the Intel x86-32 architecture.


但是这些不同的Braches以及开源所带来的问题就是portability problems, (即使现在，笔者也曾经因为在linux上安装驱动兼容等问题二头疼不已)。 

The C language was standardized in 1989 (C89), and a revised standard was produced in 1999 (C99).

The first attempt to standardize the operating system interface yielded POSIX.1, ratified as an IEEE standard in 1988, and as an ISO standard in 1990.

Linux separates implementation from distribution. Consequently, there is no single “official” Linux distribution. Each Linux distributor’s offering consists of a snapshot of the current stable kernel, with various patches applied.

## Kernel
Kernel in UNIX is more like the core Operating System - the central software that manages and allocates computer resources (i.e., the CPU, RAM, and devices).
