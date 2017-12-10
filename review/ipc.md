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
**ANSWER** : 3; ABC2DE, ACB2DE, BAC2DE, BCA2DE, CAB2DE, CBA2DE