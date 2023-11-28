# Redirect error

e.g.: `ls -al badfile 2> test`

`2>` means file description 2 is rediredted to test



# Redirect errors and data

e.g.: `ls -al file1 file2 2> error 1> data`



# redirect in scripts

`echo "this is an error" >&2`

This means the echo message will be redirected to stderr. But this redireciton is temporary.

## Permanent redirections

e.g.: `exec 1>testout`, `exec 2>error`

`exec 0<inputfile`

## redirect file descriptions

e.g.: `exec 3>&1`, this means fd 3 will direct to the fd 1

## create a fd

`exec 3<> testfile`

now fd3 represents testfile

## close a fd

`exec 3>&-`

# /dev/null

data redirected to this file will not be saved

  