**1.** True or False:


- A child process has the same address space as its parent.

- In a parent process, the wait() call blocks until at least one child signals the parent with its exit status.

- It is possible that a parent process exits before its child process finishes.

- In a parent process a wait call always blocks.

- A process running in the background cannot be killed.






---
**3.** 
```c
int main(){
    if (fork()==0){
        if (fork()==0){
            fprintf(stderr, "A");
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
**3(a).** How Many processes including the original one are created?
 
**3(b).** Write all possible output orders:

**3(c).** Is it possible for a child process in this program to ever become an orphan? Explain:
**ANSWER** : 3; ABC2DE, ACB2DE, BAC2DE, BCA2DE, CAB2DE, CBA2DE; Yes, the child of child could run slow and the original and first child could terminate first.