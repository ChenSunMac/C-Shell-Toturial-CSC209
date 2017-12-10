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




