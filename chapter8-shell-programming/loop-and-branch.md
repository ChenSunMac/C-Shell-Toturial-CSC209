# Loops

In Bash, we have **for and while loops**

## For Loops

**For loops** iterate through a set of values until the list is exhausted:
很像python (or python 像bash...)

**for** *variable* **in** *list*
**do**
  stuff here 
**done**

```bash
#!/bin/sh
for i in 1 2 3 4 5
do
  echo "Looping ... number $i"
done
```

---
## While Loops

**while** [*Boolean Expression*]
**do**
  stuff here 
**done**


```bash
#!/bin/sh
INPUT_STRING=hello
while [ "$INPUT_STRING" != "bye" ]
do
  echo "Please type something in (bye to quit)"
  read INPUT_STRING
  echo "You typed: $INPUT_STRING"
done
```


# Branch

基本的if...then...else... :

```bash
if [ ... ]
then
  # if-code
else
  # else-code
fi
```
如果你喜欢elseif:

```bash
if  [ something ]; then
 echo "Something"
 elif [ something_else ]; then
   echo "Something else"
 else
   echo "None of the above"
fi
```


Case:
```bash
#!/bin/sh

echo "Please talk to me ..."
while :
do
  read INPUT_STRING
  case $INPUT_STRING in
	hello)
		echo "Hello yourself!"
		;;
	bye)
		echo "See you again!"
		break
		;;
	*)
		echo "Sorry, I don't understand"
		;;
  esac
done
echo
```


## Example: read myfile line by line and processing with while and case:
```bash
#!/bin/sh
while read f
do
  case $f in
	hello)		echo English	;;
	howdy)		echo American	;;
	gday)		echo Australian	;;
	bonjour)	echo French	;;
	"guten tag")	echo German	;;
	*)		echo Unknown Language: $f
		;;
   esac
done < myfile****
```

