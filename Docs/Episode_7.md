# package management

This section is mainly about `dnf` command.

``` shell
# search 
dnf search

# install
dnf install

# remove
dnf remove

# remove packages and unnecessary dependencies
autoremove

# checks for updates, but not download
check-update

# revert to the previous version
downgrade

# provide basic information about the package
info

# reinstall the package
reinstall

# upgrade
upgrade

# Useful optoins
-q # quiet mode, aka non-interactive
-l # list pachages

```

# bash globbing

- *
- ?
- []
- {}

4 regex above can be used in shell commands to save time.

``` shell
ls *.c

ls a?b.c

ls [a-z]*.c

ls test.{c,cpp}
```

# get the length of variables

``` shell
var="some string"
echo ${#var}
```

${#varname} is the length

# get the substr

``` shell
var="this is a string"
echo "${var:0:1}"
# t

echo "${var:0:3}"
# thi

echo "${var:2}"		# from idx 2 to the end
# is is a string

echo "${vat::5}"	# from begin to idx 5
# this 
```

# Replace the first one and all

``` shell
$ var=aabbaa

$ echo ”${var/a/,}“ 
”,abbaa“

$ echo ”${var//a/,}“
”,,bb,,“
```

# Mathematical calculation

``` shell
echo $(( 10+5 ))
```

The format is like: `$(( formula ))`

