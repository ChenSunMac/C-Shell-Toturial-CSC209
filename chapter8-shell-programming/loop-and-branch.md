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




