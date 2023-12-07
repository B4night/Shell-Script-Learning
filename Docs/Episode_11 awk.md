# points & special variables

1. The default field seperator is whitespace
2. **NR**: "Number of Records" - This variable keeps track of the number of input records `awk` has processed. In most cases, this corresponds to the line number being processed.
3. **NF**: "Number of Fields" - This variable holds the number of fields in the current input record. It's useful for processing data with a variable number of columns.
4. **FS**: "Field Separator" - This variable defines the character or regular expression used to separate fields in an input record. By default, it's set to whitespace (spaces and tabs).
5. **OFS**: "Output Field Separator" - Similar to FS, but for output. It defines the separator `awk` uses when printing multiple fields. The default is a space.
6. **RS**: "Record Separator" - This variable defines what `awk` considers to be the end of a record. By default, it's a newline character, meaning `awk` treats each line as a record.
7. **ORS**: "Output Record Separator" - This defines the string used to separate output records. By default, it's a newline character.
8. **FILENAME**: This variable contains the name of the file currently being processed by `awk`.
9. **FNR**: "File Number of Records" - This is similar to NR, but it gets reset to 1 for each new file processed in a multi-file `awk` command.
10. **$0**: This represents the entire current record. So, if you print `$0`, you're printing the whole line.

## The difference between NF and NR

To simplify:

- NF: number of columns
- NR: number of lines

The number will be changed if FS and RS are changed.



# basic format

awk programs are made of one or more `pattern { action }` statements.

If pattern is true, then action will be executed. Otherwise action will not be executed.

# 2 concepts

FS and RS.

FS: field seperator

RS: record seperator

field means columns

recoed means a line. awk processes each line once at a time.

# BEGIN and END

- `BEGIN` is for initial setup before processing any lines.
- The main body of the script processes each line individually.
- `END` is for final actions after all lines have been processed.

# awk usage

``` shell
# set tab as field seperator
awk -F $'\t' 
# $'\t': This specifies that the field separator is a tab character. In awk, and in many programming languages, \t represents a tab. The $ before '\t' tells the shell to interpret \t as a tab character, not as a literal backslash followed by a letter t.

# -v assign value
# OFS:output file seperator
# this will change output seperator from original to '\t'.
awk -v OFS='\t' '{print $1 $2}' data.txt

# In this revised command, awk will print (print $0) each line from filename where the first field equals the value of a and the tenth field equals the value of b.
a=bbo; b=ccd
awk -v a="$a" -v b="$b" '$1 == a && $10 == b { print $0 }' filename

# print line number and char number of each line
awk '{print NR,length($0);}' filename

# print number of columns
awk '{print NF}' -F xx

# switch column 1 and column 2
awk '{print $2, $1}'

# if there is a comma in a column, then print
awk '$1~/,/ {print}'
```

``` shell
# split and do for loop
awk '{split($2,a,",");for (i in a) print $1"\t"a[i]}' filename
# split $2 with ',' and then we get an array. print the first column and '\t' and each element in this array

# usage
$ cat tmp 
aaa;bb,cc;dd

$ awk -F';' '{split($2,a,","); for(i in a) print $1"\t"a[i]}' tmp
aaa	bb
aaa	cc
```

``` shell
# condintional check
awk -v N=7 '{print}/bbo/&& --N<=0 {exit}'

# -v means assign variable N to 7
# '{print}/bbo/&& --N<=0 {exit}': This is the awk program, which consists of a sequence of patterns and actions enclosed in curly braces {};
	# '{print}': This part tells awk to print each line of the input. In awk, actions are performed on lines that match the specified pattern. Since there's no pattern before {print}, it applies to all lines.
	# '/bbo/&& --N<=0 {exit}': This part is a bit more complex:
		# '/bbo/': This is a pattern that matches lines containing the string "bbo".
		# '&& --N<=0': The && is a logical AND operator. --N<=0 is a condition that decrements N by 1 (--N) and then checks if N is less than or equal to 0.
# '{exit}': If the above condition is true (i.e., after the "bbo" string has been found 7 times), awk will execute the exit action, which causes it to stop processing any further input.
```

``` shell
# list all the files and the last line of all the files in current working directory
ls | xargs -I file awk 'END{print FILENAME,$0}' file
```

``` shell
# add str to column
awk 'BEGIN{OFS="\t"}; $3="str"$3'
# Caution: modifying a field which causes the entire record to be rebuilt will trigger the default action {print}
```

``` shell
# print lines that don't contain pattern
awk '!/bbo/' file
# !: This is a negation operator. It inverts the match, so the expression !/bbo/ matches any line that does not contain "bbo".
```

``` shell
# print all columns(without the last column)
awk '{NF-=1}; {print}' file
# NF: number of fields
```

# `'pattern {action};'` statement

pattern need to be non-zero so that the action statment will execute

``` shell
awk -F';' 'NF > 2 {NF -= 2}; {print}' filename

# logical and
awk 'NR > 1 && NR < 4 {print}' filename

# remove lines that only contain whitespeces
awk 'NF' filename

# perform calculations
awk '{SUM = SUM + $1}; END {print SUM}' filename
# AWK support the standard arithmetical operators. And will convert values between text and numbers automatically depending on the context. 
```

## also, pattern can be regex

``` shell
# find lines that at least contain one char
awk '/./ {COUNT += 1}; END {print COUNT}' filename

# match lines containing specific words
awk '/word/ { print }' filename

# match lines where a specific field has a pattern
awk '$2 ~ /word/ ' filename

# invert match
awk '! /word/' fielname
```

# arrays in awk

Arrays is awk are like map in C++.

``` shell
awk '+$1 { CREDITS[$3]+=$1 }
     END { for (NAME in CREDITS) print NAME, CREDITS[NAME] }' FS=, file
# +$1 is a condition, means that if $1 is numeric, then the action will be done.
# CREDITS is an array. Key-value pair
```

``` shell
# print duplicate lines
awk 'a[$0]++' filename
# explination
# a[$0]++ is a condition, if it returns non-zero, then {print} the line
# a[$0] returns old value. Its behavior is the same with C++'s ++ operation


# remove duplicate lines(print duplicate lines only once)
awk '!a[$0]++' filename
```

# field formatting

``` shell
awk '+$1 { printf("%s ", $3) }' filename

awk '+$1 { printf("%10s | %4d\n",  $3, $1) }' FS=, file
```

# awk's string functions

``` shell
# toupper
awk '$3 { print toupper($0); }' file

# change part of the string
awk '{ $3 = toupper(substr($3,1,1)) substr($3,2) } $3' FS=, OFS=, file

# split fields into sub-fields
awk '+$1 { split($2, DATE, " "); print $1,$3, DATE[2], DATE[3] }' FS=, OFS=, file
# this means using whitespaces to splic $2, then stores the values in array DATE

# search and replace patterns with awk commands
awk '+$1 { gsub(/ +/, "-", $2); print }' FS=, file
# search `/ +/` pattern in $2 and then replace it with "-"
```

# call external functoin

``` shell
awk 'BEGIN{ printf("UPDATED: "); system("date") }; /^UPDATED:/ { next }; { print }' filename
```

1. The command starts by printing "UPDATED: " followed by the current date and time.
2. Then, it reads `file` line by line.
3. Any line that starts with "UPDATED:" is skipped (not printed).
4. All other lines are printed as they are.
5. Use `system()` to call external command

# add field

``` shell
awk '+$1 { CMD | getline $5; close(CMD); print }' CMD="uuid -v4" FS=, OFS=, file
```

- The command reads the specified `file`.
- For each line where the first field is a non-zero number, it executes the `uuid -v4` command to generate a new UUID.
- This UUID replaces the value of the fifth field in the line.
- The modified line is then printed out, with fields separated by commas.

