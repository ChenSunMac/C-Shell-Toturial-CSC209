**1.** True or False:


- A child process has the same address space as its parent.

- In a parent process, the wait() call blocks until at least one child signals the parent with its exit status.

- It is possible that a parent process exits before its child process finishes.

- In a parent process a wait call always blocks.

- A process running in the background cannot be killed.

- File descriptor are inherited across both fork and exec calls.

- A child process whose parent calls wait cannot become a zombie.

- You can send a signal to a process you do not own.

//F
- You can send a signal to a process that is not related to the process sending the signal.

//F
- The function htonl() is used to convert a string to a port number.

// CONVERT NUMBER to NUMBER
- The bind call associaes a port number with the server process.

// ASSOCIATE SOCKET FD to SERVER ADDR

- When a process running in the background writes to stdout, the output appears on the screen.

// this is how > &1 worked.



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


**4.** 
```c
int main(){
	int var = 1;
	int status;
	int r = fork();

	if (r==0){ // process X
		var++;
		r = fork();
		if (r==0){
			var ++;
			exit(var);} 
		else { // process Y
			if (wait(&status) != -1) {
				if (WIFEXITED(status)){
					printf("A %d\n", WEXITSTATUS(status));}
			}
			var += 2;
		}}
	else{ // process Z
		printf("W %d\n", var);
		if (wait(&status) != -1){
			if (WIFEXITED(status)){
				printf("B %d\n", WEXITSTATUS(status));}
		}

	}
	printf("C %d\n", var);
	return 0;
}
```

**4(a).** Write all possible output orders for this program.

 ```
 W 1;A 3;C 4; B 0;C 1
 A 3;C 4;W 1; B 0;C 1
 A 3;W 1;C 4; B 0;C 1
 ``` 

**4(b).** Can process X or Y become an orphan? 
No

**4(c).** Can process X or Y become an zombie?
It can be before wait() call clear the process table.