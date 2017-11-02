# Monitoring Child Processes

*wait()* and *waitpid()* can monitoring if the child process is terminated and their status when *exit()* in the MACRO: WEXITSTATUS (and other MACROs like WIFEXITED, WIFSTOPPED)

## Orphan and Zombie

The lifetimes of parent and child processes are usually not the same—either the
parent outlives the child or vice versa.

### Zombie Process
子进程结束快，父进程还在跑也没wait(),虽然子进程已经结束，但是还占着进程表
A process which has finished the execution but still has entry in the process table to report to its parent process is known as a zombie process. A child process always first becomes a zombie before being removed from the process table. The parent process reads the exit status of the child process which reaps off the child process entry from the process table.
```c
int main()
{
    // Fork returns process id
    // in parent process
    pid_t child_pid = fork();
 
    // Parent process 
    if (child_pid > 0)
        sleep(50);
 
    // Child process
    else       
        exit(0);
 
    return 0;
}
```