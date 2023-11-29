# Pre-knowledge

1. In regex, ^ and $ mean the begin and the end of a line
2. use `Egrep`  to enable extended regular expression



# Usage

``` shell
# count empty lines
grep -c "^$" ./*

# only return numbers
grep -o "[0~9]*"

# extract lines that contain 3 consecutive digitals
egrep "[0-9]{3}"

# return also 3 lines after match
grep -A 3 'bbo'

# return also 3 lines before match
grep -B 3 'bbo'

# return also 3 lines before and after match
grep -C 3 'bbo'n lines before and after matched lines


# grep strings that contains str
egrep "S.*" ./*
# .* means multiple [0~n] random chars

# -v: not contain
grep -v "^#" ./*	# output lines not start with #

# grep and return line number
grep -c "str" ./*

# count lines that satisfies needs
grep -o "str" | wc -l

# ignore case
grep -i

# recursively grep in directories
grep str -R /dir/

# grep all content of fileA from fileB
grep -f fileA fileB

# grep a tab
grep $'\t'


```

