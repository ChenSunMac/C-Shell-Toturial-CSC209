# User Mode and Kernel Mode

Every modern operating system supports the two modes: **User Mode and Kernel Mode** for CPU.

*Kernel Mode*:
- When CPU is in kernel mode, the code being executed can access any memory address and any hardware resource.
- Hence kernel mode is a very privileged and powerful mode.
- If a program crashes in kernel mode, the entire system will be halted.


*User Mode*:
- When CPU is in user mode, the programs don't have direct access to memory and hardware resources.
- In user mode, if any program crashes, only that particular program is halted.
- That means the system will be in a safe state even if a program in user mode crashes.


Hence, most programs in an OS run in user mode.