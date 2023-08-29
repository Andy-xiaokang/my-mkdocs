# shell_learning docs
!!! abstract "docs for shell"
    some easily forgotten commands and very important knowledge for shell 

## Using the shell
[键盘特殊符号中英文名称对照表](https://ajiew.me/keyboard-special-symbols/)

|symbol |English |meaning |
|:---:|:---:|:---:|
|`.`|dot |current working directory|
|`..`|dot dot |parent directory|
|`~`|tilde|home directory |
|`/`|slash |root directory |
|`-`|dash |last working directory |
|`$`|dollar |you are not root user |
|`#`|sharp or hash key|**you are root user**|


[more symbol English](https://tool.lu/symbol/).
If the shell is asked to execute a command that doesn't match one of its programming keywords, it consult an ***environment variable*** called `$PATH` that lists which directories the shell should search for programs when it is given the command.  
![截屏2023-05-18 23.28.19](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/%E6%88%AA%E5%B1%8F2023-05-18%2023.28.19.png)
When we run the `echo` command, the shell see that it should execute the program `echo`, and the search though the `:` seperated lists of directories in `$PATH` for a file by the name. when it finds it, it runs it.

***

## navigating in the shell
A path that starts with `/` is called an *absolute* path. Any other path is a *relative* path. relative paths are relative to the current working directory.  

|command|meaning|
|:---:|:---:|
|`pwd`|present working directory|
|`cd`|change directory|
|`ls`|list directory contents|
|`mv`|move/rename a file|
|`cp`|copy a file|
|`mkdir`|make a new directory|
|`man`|manual page|


![截屏2023-05-19 13.52.02](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/%E6%88%AA%E5%B1%8F2023-05-19%2013.52.02.png)
`ls` print the contents of the current directory. most commands accept flags and options(flags with values) that start with `-` to modify their behaviour.`ls -l` gives us a bunch more information about each file or directory present. First, the `d` at the begining of the line tells us that `markdown` is a directory. Then follow three groups of three characters(rwx)(r-x)(r-x). These indicate what permissions the owner of the file(**niyasushi**), the owning group(**users**), and everyone else respectively have on the relevant item. A `-` indicates that the given principal does not have on the given item. above only the owner is allowed to modify (`w`) the `markdown` directory(i.e., add/remove files in it). To enter a directory, a user must have "search"(represented by "execute": `x`) permissions on that directory(and its parents). To list its contents, a user must have read(`r`) permissions on that directory. Notice that nearly all the files in `/bin` have the `x` permission set for the last group, "everyone else", so that anyone can excute those programs.

***

## connecting programs
In the shell, programs have two primary “streams” associated with them: their **input stream** and their **output stream**. When the program tries to read input, it reads from the input stream, and when it prints something, it prints to its output stream. Normally, a program’s input and output are both your terminal. That is, your keyboard as input and your screen as output. However, we can also rewire those streams!

|command|meaning|
|:---:|:---:|
|`< file`|rewire the input stream|
|`> file`|rewire the output stream|
|`>> file`|append a file|
|`1>&2`|stdout rewire stderr|
|`2>&1`|stderr rewire stdout|
|`cat`|concatenate and print files|
|`|`|pipe|
|`sudo`|execute a command as super user|
|`chmod`|[change mode](https://zh.wikipedia.org/wiki/Chmod)|
|'grep'|[globally search a regular expression and print](https://zh.wikipedia.org/wiki/Grep)|

a brief introduction for chmod
![截屏2023-05-19 17.35.36](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/%E6%88%AA%E5%B1%8F2023-05-19%2017.35.36.png)

***

## shell scripting
To assign variables in bash, use the syntax `foo=bar` and access the value of the variable with `$foo`.  In general, in shell scripts the space character will perform argument splitting. Strings in bash can be defined with `'` and `"` delimiters, but they are not equivalent. Strings delimited with `'` are literal strings and will not substitute variable values whereas `"` delimited strings will.

|symbol|meaning|
|:---:|:---:|
|`$0`|Name of the script|
|`$1` to `$9`|Arguments to the script. `$1` is the first argument and so on|
|`$#`|Number of arguments|
|`$@`|the list of all the arguments|
|`$$`|Process identification number (PID) for the current script|
|`$_`|Last argument from the last command|
|`$?`|the exit status of the last command|
|`!!`|Entire last command, including arguments|

Commands will often return output using `STDOUT`, errors through `STDERR`. A value of `0` usually means everything went OK; anything different from `0` means an error occurred.
Exit codes can be used to conditionally execute commands using `&&` (and operator) and `||` (or operator), both of which are short-circuiting operators.  
![截屏2023-05-20 18.30.53](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/%E6%88%AA%E5%B1%8F2023-05-20%2018.30.53.png)

Another common pattern is wanting to get the output of a command as a variable. This can be done with ***command substitution***. Whenever you place `$( CMD )` it will execute CMD, get the output of the command and substitute it in place. For example, if you do for file in `$(ls)`, the shell will first call ls and then iterate over those values. A lesser known similar feature is process substitution, `<( CMD )` will execute CMD and place the output in a temporary file and substitute the `<()` with that file’s name. 
```shell
#!/bin/bash
echo "starting program at $(date)"
echo "Running program $0 with $# arguments with pid $$"
for file in "$@"; do
	grep foobar "$file" > /dev/null 2> /dev/null
	if [[ $? -ne 0 ]]; then
		echo "File $file doesn't exist foobar, adding one"
		echo "# foobar" >> "$file"
	fi
done		
```

### shell globbing
* ***Wildcards*** - Whenever you want to perform some sort of wildcard matching, you can use `?` and `*` to match one or any amount of characters respectively. For instance, given files `foo`, `foo1`, `foo2`, `foo10` and `bar`, the command `rm foo?` will delete `foo1` and `foo2` whereas `rm foo*` will delete all but `bar`.  
* ***Curly braces***`{}`-Whenever you have a common substring in a series of commands, you can use curly braces for bash to expand this automatically. 
![截屏2023-05-20 19.31.38](https://raw.githubusercontent.com/Andy-xiaokang/Picgo/master/images/%E6%88%AA%E5%B1%8F2023-05-20%2019.31.38.png)

***

## task

```sh
 find ./ -name '*.html' -print0 | xargs -0 tar vcf html.zip
```

```sh
 find . -type f -print0 | xargs -0 ls -lt | head -10
```

## shell tools
[tldr](https://tldr.sh)  
[find](https://www.man7.org/linux/man-pages/man1/find.1.html)  
[autojump](https://github.com/wting/autojump)  
[tree](https://linux.die.net/man/1/tree)  
[nnn](https://github.com/jarun/nnn)


