# Useful options

``` shell
-n: specify maximum args
-p: add prompt, be more interactive
-t: --verbose, print commands along with output
-0: changes the delimiter from whitespece(or others) to a null character
	This is useful when dealing with input that may contain spaces like filename.
	e.g.: 'a description.md'
-I: replace strs
```



# Usage

``` shell
# use prompts before running commands
ls | xargs -L1 -p head
# this will interactively ask whether to apply head on each file

ls | xargs -L1 -p file
```

``` shell
# specify arg nums
echo 0 1 2 3 4 | xargs -n 2 echo
# output:
# 0 1
# 2 3
# 4
```

``` shell
# test -t
$ echo 0 1 2 3 4 | xargs -n 2 -t echo
echo 0 1
0 1
echo 2 3
2 3
echo 4
4
```

``` shell
# test -0, especially useful when dealing with filenames
$ ls
'first file'  'second file'
$ ls | xargs -n1   	# this will treat whitespace as delimiter
first
file
second
file
$ ls | xargs -0 -n1	# tread null as demiliter
first file
second file
```

``` shell
# test -I
ls | xargs -n1 -I {} head {}	# {} is placeholder

# or
ls | xargs -n1 -I f head f
```

