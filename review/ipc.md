**1.** True or False:


- A child process has the same address space as its parent.

- In a parent process, the wait() call blocks until at least one child signals the parent with its exit status.

- 






---
**3.** 
```c
int main(){
    if (fork()==0){
        if (fork()==0){
            fprintf(stderr, "B");
            exit(3);
        }else{
            fprintf(stderr, "B");
            exit(2);
        }
    }else{
        int status;
        fprintf(stderr, "C");
        if (wait(&status) != -1){
            if (WIFEXITED(status)){
                fprintf(stderr, "%d", WEXITSTATUS(status));
            }
        }
        fprintf(stderr, "D");
    }
    fprintf(stderr, "E");
    return 0;
}
```