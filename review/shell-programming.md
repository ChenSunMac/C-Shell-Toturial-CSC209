# Redirection, Pipe, chmod

**1.**  Write one line that you would type into the bash shell to run the program markall found in the current directory so that it reads standard input from the file classlist and send the output to the program grep with the argument TOTAL. The output from grep should be saved in a file results

**ANSWER**

```sh
markall < classlist | grep TOTAL > results
```

**2.** Write one line that you would type into the bash shell to set the permissions for the file prog to remove read write and execute permissions for everyone who is not the owner of the file or in the group.

**ANSWER**

```sh
chmod o-rwx prog
```

**3.** In the current directory, some of the files contain the string *FIX ME*. Write a shell command that counts the number of lines containing this phrase in the files ending in *.c*


```sh
grep "FIX ME" *.c | wc 
```



# Shell program

**1.**  Write out the output for the following commands:

```sh
y=thurs
y='$y day'
echo y
```

```sh
z="fri day"
for piece in "$z"
    do
        echo "$piece *"
    done
```
```sh
z="fri day"
for piece in $z
    do
        echo "$piece *"
    done
```


**2.**  Write a shell program *longer* that takes two filenames as command line arguments and prints to *stdout* the content of the file that is longer.  By default, the length is determined as the number of lines, but if the script is called with an optional -w argument (that must come before the filenames), it determines length based on the number of words instead.

(longer File1 File2; ## length depends on line count)
(longer -w File1 File2; ## length depends on word count)


```sh
if ["$1" -eq "-w"]; then
    shift
    length1=`wc -w "$1"`
    length2=`wc -w "$2"`
else
    length1=`wc -l "$1"`
    length2=`wc -l "$2"`
if [$length1 -ge $length2]; then
    cat "$1"
else
    cat "$2"
fi
```

**3.**  Write a shell program using loop to create five files named file1, file2,... file5. They should have the number of line corresponding to their name. For example, file4 should have 4 lines. It does not matter what content you put in the lines in files.

```sh
for i in 1 2 3 4 5; do
    touch "file$i"
    count=0
    while [$count -lt $i]
    do
        count=`expr $count+1`
        echo $i >> file$i
    done
done
```

**4.** Without using the wc program, write a bash shell program that prints the number of C source code files in the current working directory.

```sh
index=0
for file in `ls *.c`; do
    index=$[$index+1]
done
echo $index
``` 


**6.** One line command in bash shell to send the QUIT signal to the process with ID 718.

```sh
kill -QUIT 718 #or
kill -SIGQUIT 718 #or
kill -3 718
```

**7.** One line command in bash shell to retrieve the number of processes being run by the user "jojo".
```sh
ps -u jojo | wc -l        #or
ps aux | grep jojo | wc -l
```

**8.** Shell program in bash taht checks if folder "csc209" exists. If exists, print "EXISTS", else, creates it.

```sh
DIR="csc209"
if [-d "$DIR"];
then 
    echo "EXISTS"
else
    mkdir "$DIR"
fi
```


