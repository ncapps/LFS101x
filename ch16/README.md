# Chapter 16: More on Bash Shell Scripting

## String Manipulation
Operator | Meaning
--- | ---
`[ string1 > string2 ]]` | Compares the sorting order of string1 and string2.
`[[ string1 == string2 ]]` | Compares the characters in string1 with the characters in string2.
`myLen1=${#string1}` | Saves the length of string1 in the variable myLen1.


## Parts of a String
- [Example: String Tests and Operations](https://courses.edx.org/asset-v1:LinuxFoundationX+LFS101x+1T2020+type@asset+block/labsol-teststrings.html)
```sh
# Extract the first n characters of a string
${string:0:n}

# Extract all character in a string after a dot (.)
${string#*.}
```

## The case Statement
- `case` statements are often used to handle command-line options
- It is a good alternative to nested, multi-level `if-then-else-fi` code blocks
- [Example: Using the case Statement](https://courses.edx.org/asset-v1:LinuxFoundationX+LFS101x+1T2020+type@asset+block/labsol-case.html)
```sh
case expression in
   pattern1) execute commands;;
   pattern2) execute commands;;
   pattern3) execute commands;;
   pattern4) execute commands;;
   * )       execute some default commands or nothing ;;
esac
```

## Looping constructs
- The `for` loop operates on each element of a list of items
```sh
for variable-name in list
do
    execute one iteration for each item in the list until the list is finished
done
```

- The `while` loop repeats a set of statements as long as the control command returns true
```sh
while [ condition is true ]
do
    Commands for execution
    ----
done
```

- The `until` loop repeats a set of statements as long as the control command is false
```sh
until [ condition is false ]
do
    Commands for execution
    ----
done
```

## Debugging bash Scripts
- Run a bash script in debug mode either by doing bash `–x ./script_file`, or bracketing parts of the script with `set -x` and `set +x`
- Redirect errors to a file `./test.sh 2> error.log`

File stream | Description | File Descriptor
--- | --- | ---
stdin | Standard Input, by default the keyboard/terminal for programs run from the command line | 0
stdout | Standard output, by default the screen for programs run from the command line | 1
stderr | Standard error, where output error messages are shown or saved | 2

## Creating Temporary Files and Directories
- The best practice is to create random and unpredictable filenames for temporary storage. One way to do this is with the `mktemp` utility

Command | Usage
--- | ---
`TEMP=$(mktemp /tmp/tempfile.XXXXXXXX)` | To create a temporary file
`TEMPDIR=$(mktemp -d /tmp/tempdir.XXXXXXXX)` | To create a temporary directory

## Discarding Output with /dev/null
```sh
# Discard stdout, display stderr
$ ls -lR /tmp > /dev/null

# Discard stdout and stderr
$ ls -lR /tmp >& /dev/null
```

- Generate a randome number with `$RANDOM`

## Summary
- You can manipulate strings to perform actions such as comparison, sorting, and finding length
- You can use Boolean expressions when working with multiple data types, including strings or numbers, as well as files
- The output of a Boolean expression is either true or false
- Operators used in Boolean expressions include the && (AND), ||(OR), and ! (NOT) operators
- We looked at the advantages of using the case statement in scenarios where the value of a variable can lead to different execution paths
- Script debugging methods help troubleshoot and resolve errors
- The standard and error outputs from a script or shell commands can easily be redirected into the same file or separate files to aid in debugging and saving results
- Linux allows you to create temporary files and directories, which store data for a short duration, both saving space and increasing security
- Linux provides several different ways of generating random numbers, which are widely used
