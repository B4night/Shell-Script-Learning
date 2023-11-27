# loop redirect

``` shell
#!/bin/bash

for ((a=1; a<5; a++))
do
	if [ $a -eq 1 ] || [ $a -eq 4 ]
	then
		echo a
	else
		echo "$a,$a"
	fi	
done > output
```

`done > output` can redirect the output of the loop to specific files.



# Special parameter

- $0: the script's name
- $1~$8: from the first to the eighth param
- $9 and more: the nighth param and other. Need to use braces around these. 
  e.g.: `{$9}, {$10}`
- $#: the number of params supplied
  - the value of the last param: `${!#}`
- $*: takes all the parameters supplied of the command line as a single word
- $@:  takes all the parameters supplied on the command line  as separate words in the same string.



## param with quotes`""`

Be cautious that all the params need to be quoted except `$#`. But it's not wrong to quote that.

Keep in mind that everytime you come into special params, quote it.



# shift command

When you use the shift command, it moves each parameter variable one position to the  left by default. Thus, the value for variable $3 is moved to $2, the value for variable $2 is  moved to $1, and the value for variable $1 is discarded (note that the value for variable  $0, the program name, remains unchanged).



default: shift 1 places

shift n: shift n places

``` shell
while [ -n "$1" ]
do
	echo xxx
	shift
done
```



# options

Use shift to process options

``` shell
while [ -n "$1" ]
do
	case "$1" in
	-a) echo aaa ;;
	-b) echo bbb ;;
	-c) echo ccc ;;
	*) echo other ;;
	esac
done
```



# getopt command

Use this command to get standard options

e.g.: `getopt ab:cd -a -b test1 -cd test2 test3`

`ab:cd` is the valid options. `b:` means that option b requires file

`-a -b test1 -cd test2 test3` is the string that needs to be parsed



## use getopt and set to replace original command line parameters

`set -- $(getopt -q ab:cd "$@")`

`--` is a option which instructs set to replace the command line parameter variables with the values of the set command's command line

Then we can use case to process standardized optoins



# read command: get user input

``` shell
read name
echo "Name is $name"

read -p "Enter your age: " age
echo "Age is $age"
```



# read from file

``` shell
cat file | while read line
do
	echo $line
done
```

