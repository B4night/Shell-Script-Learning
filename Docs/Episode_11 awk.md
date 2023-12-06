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
$ /tmp cat tmp 
aaa;bb,cc;dd

$ /tmp awk -F';' '{split($2,a,","); for(i in a) print $1"\t"a[i]}' tmp
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

