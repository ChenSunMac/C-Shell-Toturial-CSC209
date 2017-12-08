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