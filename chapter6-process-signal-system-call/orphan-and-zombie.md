# Monitoring Child Processes

*wait()* and *waitpid()* can monitoring if the child process is terminated and their status when *exit()* in the MACRO: WEXITSTATUS (and other MACROs like WIFEXITED, WIFSTOPPED)

## Orphan and Zombie

The lifetimes of parent and child processes are usually not the same—either the
parent outlives the child or vice versa.

### Zombie Process
子进程结束快，父进程还在跑也没wait()
A process which has finished the execution but still has entry in the process table to report to its parent process is known as a zombie process. A child process always first becomes a zombie before being removed from the process table. The parent process reads the exit status of the child process which reaps off the child process entry from the process table.