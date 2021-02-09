# Chapter 15: The Bash Shell and Basic Scripting

- Commonly used interpreters include: `/usr/bin/perl, /bin/bash, /bin/csh, /usr/bin/python and /bin/sh`
- a shell is a command line interpreter which provides the user interface for terminal window
```bash
#!/bin/bash
# Simple bash script

echo "Hello Linux Foundation Student"
```

- All shell scripts generate a return value upon finishing execution, which can be explicitly set with the `exit` statement.
- By convention, success is returned as 0, and failure is returned as a non-zero value. The return value is stored in the environment variable represented by `$?`

## Basic Syntax and Special Characters

Character | Description
--- | ---
`#` | Used to add a comment, except when used as `\#`, or as `#!` when starting a script
`\` | Used at the end of a line to indicate continuation on to the next line
`;` | Used to interpret what follows as a new command to be executed next
`$` | Indicates what follows is an environment variable
`>` | Redirect output
`>>` | Append output
`<` | Redirect input
`|` | Used to pipe the result into the next command
`&&` | Proceed until something fails
`||` | Proceed until something succeeds


## Built-In Shell Commands
- Compiled applications are binary executable files, generally residing on the filesystem in well-known directories such as `/usr/bin`.
- Shell scripts always have access to applications such as `rm, ls, df, vi, and gzip`, which are programs compiled from lower level programming languages such as C.

## Script Parameters
- Within a script, the parameter or an argument is represented with a `$` and a number or special character.

Parameter | Meaning
--- | ---
`$0` | Script name
`$1` | First parameter
`$2 $3, etc.` | Second, third parameter, etc.
`$*` | All parameters
`$#` | Number of arguments

## Command Substitution
At times, you may need to substitute the result of a command as a portion of another command. It can be done by enclosing the inner command in `$( )`

## Exporting Environment Variables
- By default, the variables created within a script are available only to the subsequent steps of that script.
- Any child processes (sub-shells) do not have automatic access to the values of these variables.
- To make them available to child processes, they must be promoted to environment variables using the export statement:
```sh
export VAR=value
# OR
VAR=value ; expprt VAR
```
- While child processes are allowed to modify the value of exported variables, the parent will not see any changes; exported variables are not shared, they are only copied and inherited.

## Functions
- Using functions in scripts requires two steps:
1. Declaring a function
2. Calling a function
```sh
# Function declaration
function_name () {
   command...
}

```
- [Example: Working with Files and Directories](https://courses.edx.org/asset-v1:LinuxFoundationX+LFS101x+1T2020+type@asset+block/labsol-testfile.html)

## The if Statement
- When an `if` statement is used, the ensuing actions depend on the evaluation of specified conditions, such as:
1. Numerical or string comparisons
2. Return value of a command (0 for success)
3. File existence or permissions.

```sh
if condition ; then
    statements
else
    statements
fi
```

- In modern scripts, you may see doubled brackets as in `[[ -f /etc/passwd ]]`. This is not an error. It is never wrong to do so and it avoids some subtle problems, such as referring to an empty environment variable without surrounding it in double quotes

## File Conditions
Condition | Meaning
--- | ---
`-e file` | Checks if the file exists.
`-d file` | Checks if the file is a directory.
`-f file` | Checks if the file is a regular file (i.e. not a symbolic link, device node, directory, etc.)
`-s file` | Checks if the file is of non-zero size.
`-g file` | Checks if the file has sgid set.
`-u file` | Checks if the file has suid set.
`-r file` | Checks if the file is readable.
`-w file` | Checks if the file is writable.
`-x file` | Checks if the file is executable.

## Boolean Expressions
Operator | Operation | Meaning
--- | --- | ---
`&&` | AND | The action will be performed only if both the conditions evaluate to true.
`\|\|` | OR | The action will be performed if any one of the conditions evaluate to true.
`!` | NOT | The action will be performed only if the condition evaluates to false.

## Numerical Tests
Operator | Meaning
--- | ---
`-eq` | Equal to
`-ne` | Not equal to
`-gt` | Greater than
`-lt` | Less than
`-ge` | Greater than or equal to
`-le` | Less than or equal to


## Arithmetic Expressions
- Arithmetic expressions can be evaluated in the following three ways
- [Example: Arithmetic and Functions](https://courses.edx.org/asset-v1:LinuxFoundationX+LFS101x+1T2020+type@asset+block/labsol-testmath.html)
```sh
# Using the expr utility
expr 8 + 8
echo $(expr 8 + 8)

# Using the $((...)) syntax
echo $((x+1))

# Using the built-in shell command let
let x=( 1 + 2 ); echo $x
```

## Summary
- Scripts are a sequence of statements and commands stored in a file that can be executed by a shell. The most commonly used shell in Linux is bash.
- Command substitution allows you to substitute the result of a command as a portion of another command.
- Functions or routines are a group of commands that are used for execution.
- Environmental variables are quantities either preassigned by the shell or defined and modified by the user.
- To make environment variables visible to child processes, they need to be exported.
- Scripts can behave differently based on the parameters (values) passed to them.
- The process of writing the output to a file is called output redirection.
- The process of reading input from a file is called input redirection.
- The `if` statement is used to select an action based on a condition.
- Arithmetic expressions consist of numbers and arithmetic operators, such as +, -, and *.


