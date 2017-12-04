# Math Expressions

以下三种都是完成2+2这样任务的
```bash
val=`expr 2 + 2`
var=$[2+2]
var=$((2+2))
```
- 在用expr的时候，表达式和运算符之间要有空格expr 2+2 是错的
- 支持 +, -, *, /, %, == ...



### Relation operator:


```bash
a=10
b=20
if [ $a -eq $b ]
then
   echo "$a -eq $b : a is equal to b"
else
   echo "$a -eq $b: a is not equal to b"
fi
```