# echo

`echo -n` : do not start a new line after output the str



## e.g.

``` shell
$ cat echo.sh 
#/bin/sh
echo -n "hello  "
date
$ ./echo.sh 
hello  Mon Nov 20 11:17:43 AM CST 2023     
```



# switch between split terminals and tabs

use `ctrl + shift + arrow` to switch between split terminals

use `alt + number` to switch between seperate tabs



# get the output of the command

``` shell
# use ` or $() to get the output of the command and assign it to variables

$ cat command_assign.sh 
#/bin/bash

d1=`date`
d2=$(date)

echo $d1
echo $d2
$
$
$ ./command_assign.sh 
Mon Nov 20 02:13:30 PM CST 2023
Mon Nov 20 02:13:30 PM CST 2023
```



# command return value

command returns 0 if it executes successfully



# customize exit status code

``` shell
$ cat test13
#!/bin/bash
# testing the exit status
var1=10
var2=30
var3=$[$var1 + $var2]
echo The answer is $var3
exit 5

$ ./test13
<output>

$ echo $?
5
```



# if statement

``` shell
if command
then
	commands
else
	commands
fi
```

## elif

``` shell
if xx
then
	xx
elif xx
then
	xx
elif
then
	xx
else
	xx
fi
```



# test command

`[ condition ]`: This can be used for integers, strings, files

**Caution**: bash can only handle integers

```
The test Numeric Comparisons
Comparison Description
n1 -eq n2 	Checks if n1 is equal to n2
n1 -ge n2 	Checks if n1 is greater than or equal to n2
n1 -gt n2 	Checks if n1 is greater than n2
n1 -le n2 	Checks if n1 is less than or equal to n2
n1 -lt n2 	Checks if n1 is less than n2
n1 -ne n2 	Checks if n1 is not equal to n2


The test String Comparisons
Comparison Description
str1 = str2 	Checks if str1 is the same as string str2
str1 != str2 	Checks if str1 is not the same as str2
str1 < str2 	Checks if str1 is less than str2
str1 > str2 	Checks if str1 is greater than str2
-n str1 		Checks if str1 has a length greater than zero
-z str1 		Checks if str1 has a length of zero

The test File Comparisons
Comparison Description
-d file 	Checks if file exists and is a directory
-e file 	Checks if file exists
-f file 	Checks if file exists and is a file
-r file 	Checks if file exists and is readable
-s file 	Checks if file exists and is not empty
-w file 	Checks if file exists and is writable
-x file 	Checks if file exists and is executable
-O file 	Checks if file exists and is owned by the current user
-G file 	Checks if file exists and the default group is the same as the current user
file1 -nt file2 	Checks if file1 is newer than file2
file1 -ot file2 	Checks if file1 is older than file2
```

# double brackets

provide advanced features for string comparisons

`[[ expression ]]`

provides: pattern matching

``` shell
if [[ $USER == r* ]]
then
	echo "HI"
else
	echo "NO"
fi
```



# switch-case

``` shell
case variable in
pattern1 | pattern2) commands1;;
pattern3) commands2;;
*) default commands;;
esac
```



# for-loop

``` shell
for var in list
do 
	commands
done
```



# C-style for command

``` shell
for ((i = 1; i <= 10; i++))
do
	command
done
```



# multiple test commands

``` shell
while echo $var1
	  [ $var1 -ge 0 ]
do
	command
done
```

