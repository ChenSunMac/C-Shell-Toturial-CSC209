**1.** Consider the C program below which produces the output:
```
Even positions are 0246 and odd positions are 1357
Even positions are ACE and odd positions are BD
```
Complete the function parity strings as described in the function comment. Your program should generate this output without making any changes to main. Your function must not change parameter *s*.

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