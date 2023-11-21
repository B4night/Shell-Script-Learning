# Local variables and Global variables

`echo $var_name` is used to see the value of a variable.



## global variables

``` shell
$ gvar=haha
$ env | grep gvar=haha
$ env | grep 'gvar=haha'
$ echo $gvar
haha

$ export gvar		# now gvar is a global variable
$ echo $gvar
haha
$ env | grep 'gvar=haha'
gvar=haha
```

## add global variables in `~/.bashrc`

``` shell
# e.g.
export PATH="/home/cfei/anaconda3/bin:$PATH"
export PATH="/opt/typora:$PATH"
```

## remove global variable

just use `unset`

e.g. : `unset gvar`