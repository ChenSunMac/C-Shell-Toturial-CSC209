We will explain the Dangling, Wild, Null and Void Pointer here.

- Dangling and Wild Pointer may result in Segment Fault.
- Void Pointer is a Type
- Null Pointer is a Value (0)

### Dangling Pointer

A pointer pointing to a memory location that has been **deleted (or freed)** is called *dangling pointer*. There are three different ways where Pointer acts as dangling pointer

1. De-allocation of memory or free()
```c
// Deallocating a memory pointed by ptr causes
// dangling pointer
int main()
{
    int *ptr = (int *)malloc(sizeof(int));
 
    // After below free call, ptr becomes a 
    // dangling pointer
    free(ptr); 
     
    // No more a dangling pointer
    ptr = NULL;
}
```

2. Function call, the local variable and goes out of scope after function return 
```c
int *fun()
{
    // x is local variable and goes out of
    // scope after an execution of fun() is
    // over.
    int x = 5;
 
    return &x;
}
 
// Driver Code
int main()
{
    int *p = fun();
    // p points to something which is not
    // valid anymore
    printf("%d", *p);
    return 0;
}
```


### Void Pointer
Void pointer is a specific pointer type – void *. Void refers to the type. Basically the type of data that it points to is can be any.
Void pointers cannot be dereferenced. It can however be done using typecasting the void pointer. 

```c
int main()
{
    int x = 4;
    float y = 5.5;
     
    //A void pointer
    void *ptr;
    ptr = &x;
 
    // (int*)ptr - does type casting of void 
    // *((int*)ptr) dereferences the typecasted 
    // void pointer variable.
    printf("Integer variable is = %d", *( (int*) ptr) ); // 4
 
    // void pointer is now float
    ptr = &y; 
    printf("\nFloat variable is= %f", *( (float*) ptr) ); // 5.50000
 
    return 0;
}
```


### NULL Pointer

NULL Pointer is a pointer which is pointing to nothing. In case, if we don’t have address to be assigned to a pointer, then we can simply use NULL.

```c
int main()
{
    // Null Pointer
    int *ptr = NULL;
     
    printf("The value of ptr is %u", ptr); // 0 
    return 0;
}
```
- An uninitialized pointer stores an undefined value. A null pointer stores a defined value, but one that is defined by the environment to not be a valid address for any member or object.
- Null pointer is a value, while void pointer is a type

### Wild pointer

A pointer which has not been initialized to anything (not even NULL) is known as wild pointer. The pointer may be initialized to a non-NULL garbage value that may not be a valid address.

```c
int main()
{
    int *p;  /* wild pointer */
 
    int x = 10;
 
    // p is not a wild pointer now
    p = &x;
 
    return 0;
}
```