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


### Orphan Process
父进程太快，没了以后子进程没了爹娘被 init process 收养
Parent finishes execution and exits while the child process is still executing and is called an orphan process now
```c
int main()
{
    // Create a child process      
    int pid = fork();
 
    if (pid > 0)
        printf("in parent process");
 
    // Note that pid is 0 in child process
    // and negative if fork() fails
    else if (pid == 0)
    {
        sleep(30);
        printf("in child process");
    }
 
    return 0;
}
```