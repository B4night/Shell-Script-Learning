# Useful Options

1. `-type`: assign types
   - `d`: directory
   - `f`: regular file
2. `-name`: use pattern to find
3. `-exec`: execute commands
4. `-printf`: control print format
5. `-size`: filter files that satisfies specific size.
6. `-remove`: remove files or empty directories
7. `-empty`: empty files

# Usage

## execute on find filesW

``` shell
find . -name '*.php' -exec sed -i 's/www/w/g' {} \;
```

1. `find . -name '*.php'`:
   - `find` is a command used to search for files in a directory hierarchy.
   - `.` specifies the current directory as the starting point for the search.
   - `-name '*.php'` tells `find` to look for files whose names end with `.php`. The asterisk (`*`) is a wildcard character that matches any number of characters.
2. `-exec sed -i 's/www/w/g' {} \;`:
   - `-exec` allows you to execute another command on each file that `find` locates.
   - `sed` is a stream editor used to perform basic text transformations on an input stream (a file or input from a pipeline).
   - `-i` is an option for `sed` that means "edit files in place", which allows `sed` to modify the file directly.
   - `'s/www/w/g'` is the `sed` command that replaces all occurrences of `www` with `w` in each line.
   - `{}` is a placeholder for the `find` command that represents the current file being processed.
   - `\;` marks the end of the command executed by `-exec`.

## find files meets size requirements

``` shell
find / -type f -size +4G
# find files whose sizes are bigger than 4 gigabytes
```

## delete empty files

``` shell
find . -type f -empty -delete
```

