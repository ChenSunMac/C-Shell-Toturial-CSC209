**0.** True or False:

- Global variables should never be declared in header files.



**1.** Consider the C program below which produces the output:
```
Even positions are 0246 and odd positions are 1357
Even positions are ACE and odd positions are BD
```
Complete the function parity strings as described in the function comment. Your program should generate this output without making any changes to main. Your function must not change parameter *s*.

**1(a)**
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
/* Return a pointer to an array of two strings. 
The first is the characters of string s that are in odd positions 
The second is the characters from s that are in even positions */
char ** parity_strings(char * s) {

}
```

```c
int main() {
    char s1[9] = "01234567";
    char ** r = parity_strings(s1);
    printf("Even positions are %s and odd positions are %s\n", r[0],r[1]);
    char * s2 = "ABCDE";
    r = parity_strings(s2);
    printf("Even positions are %s and odd positions are %s\n", r[0],r[1]);
}
```

**1(b)** Which call in main() will fail if we want to change parameter *s*? and Why?

**1(c)** The program as written has a memory leak in the main function. Explain where this is?

**1(d)** Complete a function free all that could be added to the program to fix the memory leak. 

```c
void free_all( ) {


}
```

---

**2.** What is the result of the following running snippets?

```
char *s = "UofT";
s[0] = 'V';
printf("%s\n", s);
```
program Crashes because string literal array are read-only.

---
**3.** What kind of error are you likely to see if you declare a *global variable* inside of a header file?

**ANSWER**: Multiple definition.


**4.(a)** Write one line code that divides integer variable *a* by 2 without using division operator.

```c
a=a>>1
```
**4.(b)** Write one line code that sets all but the 5th bit in the integer variable a. The 5th bit remains unchanged.
```c
a=a|~(1<<5)
```

**5.** 

```c
char s[11] = "0123456789";
char *t = "source";
char *p = s+3;
strncpy(s+2, t, 9);
printf("%s\n", s);
```
**5(a).** What is the output?
```
01source
``` 
**5(b).** What is the type of &t and *p; and what is the value of p[2]?
```
char **;  char;  r
```


**6.** Complete the following C function that returns the number of bits that are set to 1 in the argument set.

```c
int count_ones(unsigned int set){
    unsigned int count = 0;
    while(n){
        count += n%2;
        n >> = 1;
    }
    return count;
}

```


**7.** In A2, *freelist* was a linked list that contained the address and size of blocks that had been freed. THe freelist is kept in increasing order by *addr*. Adjacent blocks could be collapsed together. For example, if one block has addr:0x60400 and size: 0x10 and the next block has addr = 0x60410. then the two blocks can be combined into one.

Write function *coalesce* that takes a list of blocks ordered by address and collapses all blocks that are adjacent into a single block. Returns the head of the list.


```c
struct block {
    void * addr;
    int size;
    struct block *next;
}
```

```c
struct block *coalesce (struct block *list){
    struct block current = list;
    struct block next_node = current -> next;
    
    while (current -> next != NULL){
        if (next_node -> addr == current->addr + current->size){
            current->size = current->size + next_node->size;
            current->next = next_node->next;
            free(next_node)
        }
    }
}
```



