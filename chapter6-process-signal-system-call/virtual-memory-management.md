# Virtual Memory

**Virtual Memory** \(also virtual storage\) is a memory management technique that provides an "idealized abstraction of the storage resources that are actually available on a given machine".

The aim of this technique is to make efficient use of both the CPU and RAM (physical memory).
也就是说利用这种技术，可以计算机可以有较之物理空间“看上去更大的空间”，所以才叫**Virtual** Memory


![Page of a process](/assets/page.png)


Modern microprocessors intended for general-purpose use, a **memory management unit, or MMU**, is built into the hardware. The MMU's job is to translate virtual addresses into physical addresses.

![MMU Translate Virtual Addresses into Physical Addresses](/assets/MMU.jpg)


程序在运行时，OS把程序以page的形式，分页按需装入内存，注意，他不是连续装入的，有时候先装入这一块，有时候先装入那一块，甚至有一些呢虽然也在Virtual Memory里面，但是并不在RAM的物理地址中，有可能因为执行优先级低，放进了Secondary Memory (如上图)。

我们可以看到在这里，一个process的memory layout被大卸八块分别存储在实际的物理地址里。

### Page Replacement Algorithm
Page replacement algorithms are the techniques using which an Operating System decides which memory pages to swap out, write to disk when a page of memory needs to be allocated. 
- First In First Out (FIFO) algorithm 
   
     Easy to implement, keep a list, replace pages from the tail and add new pages at the head.
- Optimal Page algorithm

  


