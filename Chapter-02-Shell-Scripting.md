# Shell Scripting

## Understanding Shell

In UNIX/Linux, a shell acts as:

1. command interpreter, a wrapper of the kernel functions/system calls
2. programming environment, with composition of command statements

### How Shell Works

Generally, a shell works as follows:

1. print prompt
2. get command line
3. interpret command
4. look for files
5. prepare parameters
6. execute command

### Command Lookup Mechanism

When a command is issued, it is concatenated to each path in `$PATH` variable and if the file exists, it will be run. The first match takes precedence.

To add lookup directory to `$PATH`, you should use `set` command first and then use `export $PATH` to update it.

If you want to use a command of a local directory, an explicit `./` should be prepended to the command, e.g. `./my_command`.

Since `$PATH` is an attribute of shell, if you want to change the `$PATH` of the current shell with script, you have to use `. script_file`

## Shell Scripts

### Ways to Execute Shell Scripts

1. `sh script\_file`

2. `chmod +x script\_file` (chown, chgrp optionally), then

   `./script\_file`
3. `source script\_file` or `. script\_file`

NOTE: using `sh script\_file` or `./script` forks a new process while `. script\_file` doesn't.

So when the last statement in script\_file is `exit 0`, with `. script\_file`, the shell that executes the command will exit

### Common Scripts

The default shell of many UNIX/Linux distributions is Bash. The following three dotfiles are common:

* `.bash\_profile` is executed when a user logs in
* `.bash\_rc` is executed when a new bash is started
* `.bash\_logout`  is executed when a users logs out

In some Linux distributions, the `service` script to manage services is also common.

## Advanced Shell Script Usages

### Empty Statement

The colon, `:`, is the empty statement in shell script, which has exit code true.

And since it is built-in, it is executed faster than `true`.

### AND and OR List

Commands can be chained using `&&` and `||`, and the behavior is similar to C.

Examples:

    [ -f ~/.bash_aliases ] && . ~/.bash_aliases 

is equivalent to 

    if [ -f ~/.bash_aliases ]; then
        . ~/.bash_aliases
    fi

### Parameter Expansions

Example1:

`${foo:-bar}`: if `foo` is defined, evaluate `foo`, else evaluate (the literal) `bar`

Example2:

    foo=/usr/bin/x11/startx

`${foo#*/}`  : will remove from the start to the minimal occurrence of \*/ of `foo` when output, and the result is:

    usr/bin/x11/startx

`${foo##*/}` : will remove from the start to the maximal occurrence of \*/ of `foo`when output, and the result is:

    startx

Example3:

    bar=/usr/local/etc/local/networks

`${bar%local*}`  : will remove from the end to the minimal occurrence of local\* of bar when output, and the result is:

    /usr/local/etc/

`${bar%%local*}` : will remove from the end to the maximal occurrence of local\* of bar when output, and the result is:

    /usr/

### Here Documents

This technique allows scripts feed input to commands, which require user input. An example is as follows:

    cat << EOF >> log
      foo
      bar
      baz
      EOF

Explanation:

`<< EOF` specifies the terminator of cat input

`>> log` redirect the output

the rest lines emulates interactive input
