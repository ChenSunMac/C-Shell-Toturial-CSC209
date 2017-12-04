# Redirection, Pipe, chmod

1. Write one line that you would type into the bash shell to run the program markall found in the current directory so that it reads standard input from the file classlist and send the output to the program grep with the argument TOTAL. The output from grep should be saved in a file results

```
**ANSWER**
```

```sh
markall < classlist | grep TOTAL > results
```

2. Write one line that you would type into the bash shell to set the permissions for the file prog to remove read write and execute permissions for everyone who is not the owner of the file or in the group.

