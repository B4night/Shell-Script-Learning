This is a documentation about sed

# using `""` and `''` in shell commands

## Single quotes

Everything enclosed in single quotes retains its literal meaning.

## Double quotes

This allows some special characters to be interpreted bu the shell.

 

# Options

- s: substitude
- d: delete
- a: append
- i: insert



# Sed: stream editor

``` shell
# remove the 1st line
sed 1d filename

# remove lines from [2, 3]
sed 2,3d filename

# remove lines that contain specific str
sed "/bbo/d" filename
sed "/bbo/Id" filename 	# this is case insensitive

# Remove lines whost nth character is not equal to a value(e.g. 5th char not equal to 2)
sed -E '/^.{5}[^2]/d' filename	# -E means extended syntax
#aaaa2aaa (you can stay)
#aaaa1aaa (delete!)

# in-place change
sed -i "/bbo/d" filename

# remove empty lines
sed "/^$/d" filename

# insert to nth line
sed "ni >$i" filename	# ni means insert to the nth line

# add string to the beginning of file
sed -i "1s/^/[/" filename

# add string to the end of file
sed -i '$s/$/]/' filename

# add strings to certain line number
sed -e "1isomething" -e "3isomething"	# ni means insert to the nth line

# add string to the beginning of every line
sed -e 's/^/str/' filename

# add string to the end of each line
sed -e 's/$/\]\}/' filename

# add a line after the line which matches the pattern
sed '/hello*/a world' filename

# substitution
sed 's/A/B/g' filename
# e.g.
sed 's/path=.*/path=\/my\/new\/path/g' filename

# do substitude operation from line 3 to line 10
sed '3,10s/aaa/bbb/' filename

# print from line 10 to line 100
sed -n 10,100p filename

# print every nth lines
sed -n '0~3p' filename
# start at line 0, print every 3 lines.

# print odd lines
sed -n '1~2p' filename

# remove ending commas
sed 's/,$//g' filename

# multiple sed operations within 1 quotes. Seperate by `;`
sed 's/a/b/g;s/c/d/g' filename


```



# The difference between `'s/a/b/'` and `'s/a/b/g`

`s/a/b/` will only replace the fitst match in a line while the `s/a/b/g` will replace all of the matches in a line.

``` shell
$ cat testfile             
apple
banana
avocado
$ sed -e 's/a/b/' testfile
bpple
bbnana
bvocado
$ sed -e 's/a/b/g' testfile
bpple
bbnbnb
bvocbdo
```

