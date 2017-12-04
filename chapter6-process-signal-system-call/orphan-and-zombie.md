# Monitoring Child Processes

_wait\(\)_ and _waitpid\(\)_ can monitoring if the child process is terminated and their status when _exit\(\)_ in the MACRO: WEXITSTATUS \(and other MACROs like WIFEXITED, WIFSTOPPED\)

## Orphan and Zombie

The lifetimes of parent and child processes are usually not the same—either the  
parent outlives the child or vice versa.

### Zombie Process

子进程结束快，父进程还在跑也没wait\(\),虽然子进程已经结束，但是还占着进程表, 这个时候子进程的状态变为EXIT_ZOMBIE, 并且the process’s parent被kernel通过SIGCHLD signal告知"你孩子死了". 然后父进程**应该**去执行wait()然后给孩子收尸，在**wait()以后**, zombie process completely removed.

This normally happens very quickly, so you won’t see zombie processes accumulating on your system. However, if a parent process isn’t programmed properly and never calls wait(), its zombie children will stick around in memory until they’re cleaned up.

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



