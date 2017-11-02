# User Mode and Kernel Mode

Every modern operating system supports the two modes: **User Mode and Kernel Mode** for CPU.

![](/assets/system-calls.png)

*Kernel Mode*:
- When CPU is in kernel mode, the code being executed can access any memory address and any hardware resource.
- Hence kernel mode is a very privileged and powerful mode.
- If a program crashes in kernel mode, the entire system will be halted.
在这个mode里，你才是真正的为所欲为的

*User Mode*:
- When CPU is in user mode, the programs don't have direct access to memory and hardware resources.
- In user mode, if any program crashes, only that particular program is halted.
- That means the system will be in a safe state even if a program in user mode crashes.


Hence, most programs in an OS run in user mode.


## System Call
当你需要跳出OS给你圈的一亩三分地用其他资源的时候就需要它了
When a program in user mode requires access to RAM or a hardware resource, it must ask the kernel to provide access to that resource. This is done via something called a system call.


When a program makes a system call, the mode is switched from user mode to kernel mode. This is called a context switch.

Then the kernel provides the resource which the program requested. After that, another context switch happens which results in change of mode from kernel mode back to user mode.


Generally, system calls are made by the user level programs in the following situations:

- Creating, opening, closing and deleting files in the file system.
- Creating and managing new processes.
- Creating a connection in the network, sending and receiving packets.
- Requesting access to a hardware device, like a mouse or a printer.


