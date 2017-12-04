# Redirection, Pipe, chmod

1. Write one line that you would type into the bash shell to run the program markall found in the current directory so that it reads standard input from the file classlist and send the output to the program grep with the argument TOTAL. The output from grep should be saved in a file results

    **ANSWER**
```sh
markall < classlist | grep TOTAL > results
```