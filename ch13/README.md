# Chapter 13: Manipulating Text

## cat and echo

```sh
# view a file
$ cat file1

# print the lines of a file in reverse order
$ tac file1

# concatenate multiple files and display the output
$ cat file1 file2

# combine multiple files and save the output to a new file
$ cat file1 file2 > file3

# append a file to another file
$ cat file1 > file2

# Any subsequent lines typed will go into the file, until CTRL-D is typed
$ cat > file1

# Any subsequent lines typed are appended to the file, until CTRL-D is typed
$ cat >> file1

# A new file is created, To exit enter EOF
$ cat > file1 << EOF
```

```sh
# Add a string in a new file
echo "Hello, World" > file1

# Append a string to a file
echo "Hello, Again" >> file1

# Dispaly an environment variable
echo $variable
```

## Working with large files

```sh
# Open large files with less
$ less somefile
$ cat somefile | less

# Print the first lines
$ head -n 5 somefile

# Print the last lines
$ tail -n 15 somefile

# View compressed files
$ zcat compressed-file.txt.gz
$ zless somefile.gz
$ zgrep -i fail somefile.gz
$ zdiff file1.gz file2.gz

# We can also use xzcat and xzless for xz files
```

## sed and awk
- `sed` is used to modify the contents of a file or input stream (it is stream editor abbreviated)
- `aws` is used to extract and print specific contents of a file

```sh
# operate on file and put the output on standard out
$ sed -e command file1

# Run a scriptfile containing sed commands on a file and put the output to standard out
$ sed -f scriptfile file1

# Substitute the first string occurence in every line
$ sed s/pattern/replace_string/ file

# Substitute all string occurences in every line
$ sed s/pattern/replace_string/g file

# Substiture all string occurences in a range of lines
$ sed 1,3s/pattern/replace_string/g file

# Save changes for string substitution in the same file
$ sed -i s/pattern/replace_string/g file
```

- Be careful with the `-i` option. It's safer to write the output to another file
```sh
$ sed s/pattern/replace_string/g file1 > file2
```

```sh
# operate on a file
$ awk command file

# Run a scriptfile containing awk commands
$ awk -f scriptfile file

# Print entire file
$ awk '{ print $0 }' /etc/passwd

# Print first field
$ awk -F: '{ print $1 }' /etc/passwd

# Print first and seventh field
$ awk -F: '{ print $1 $7 }' /etc/passwd
```

## File manipulation utilities
```sh
# sort the lines according to the characters at the beginning of each line
$ sort file1

# Combine two files, then sort
$ cat file1 file2 | sort

# Sort lines in reverse
$ sort -r file1

# Sort lines by the 3rd field
$ sort -k 3 file1

# remove duplicates from multiple files
$ sort file1 file2 | uniq > file3
$ sort -u file1 file2 > file3 # same thing

# count duplicate entries
$ uniq -c filename

# combine fields from multiple files
$ paste file1 file2

# Use paste with comma delimiter
$ paste -d, file1 file2

# Combine files based on common field
$ join file1 file2

# split a file into segments using a different prefix
$ split file1 <Prefix>
```

## Regular Expressions and Search Patterns
- **Regular expressions** are text strings used for matching a specific pattern or to search for a specific location

Search Patterns | Usage
--- | ---
`.(dot)` | Match any single character
`a|z` | Match a or z
`^` | Match beginning of string
`$` | Match end of string
`*` | Match preceding item 0 or more times

## grep and strings
- grep is extensively used as a primary text searching tool

Command | Usage
--- | ---
`grep [pattern] <filename>` | Search for a pattern in a file and print all matching lines
`grep -v [pattern] <filename>` | Print all lines that do not match the pattern
`grep [0-9] <filename>` | Print the lines that contain the numbers 0 through 9
`grep -C 3 [pattern] <filename>` | Print context of lines (specified number of lines above and below the pattern) for matching the pattern. Here, the number of lines is specified as 3

- `strings` is used to extract all printable character strings found in the file or files given as arguments
```sh
$ strings book1.xls | grep my_string
```

## Miscellaneous Text Utilities
- The `tr` utility is used to translate specified characters into other characters or to delete them. The general syntax is as follows:
```sh
$ tr [options] set1 [set2]
```

Command | Usage
--- | ---
`tr abcdefghijklmnopqrstuvwxyz ABCDEFGHIJKLMNOPQRSTUVWXYZ` | Convert lower case to upper case
`tr '{}' '()' < inputfile > outputfile` | Translate braces into parenthesis
`echo "This is for testing" | tr [:space:] '\t'` Translate white-space to tabs
`echo "This   is   for    testing" | tr -s [:space:]` | Squeeze repetition of characters using -s
`echo "the geek stuff" | tr -d 't'` | Delete specified characters using -d option
`echo "my username is 432234" | tr -cd [:digit:]` | Complement the sets using -c option
`tr -cd [:print:] < file.txt` | Remove all non-printable character from a file
`tr -s '\n' ' ' < file.txt` | Join all the lines in a file into a single line

- `tee` takes the output from any command, and, while sending it to standard output, it also saves it to a file
```sh
$ ls -l | tee newfile
```

- `wc` (word count) counts the number of lines, words, and characters in a file or list of files.

Option | Description
--- | ---
`–l` | Displays the number of lines
`-c` | Displays the number of bytes
`-w` | Displays the number of words

- `cut` is used for manipulating column-based files and is designed to extract specific columns. The default column separator is the tab character. A different delimiter can be given as a command option.

## Summary
- The command line often allows the users to perform tasks more efficiently than the GUI.
- `cat`, short for concatenate, is used to read, print, and combine files.
- `echo` displays a line of text either on standard output or to place in a file.
- `sed` is a popular stream editor often used to filter and perform substitutions on files and text data streams.
- `awk` is an interpreted programming language, typically used as a data extraction and reporting tool.
- `sort` is used to sort text files and output streams in either ascending or descending order.
- `uniq` eliminates duplicate entries in a text file.
- `paste` combines fields from different files. It can also extract and combine lines from multiple sources.
- `join` combines lines from two files based on a common field. It works only if files share a common field.
- `split` breaks up a large file into equal-sized segments.
- Regular expressions are text strings used for pattern matching. The pattern can be used to search for a specific location, such as the start or end of a line or a word.
- `grep` searches text files and data streams for patterns and can be used with regular expressions.
- `tr` translates characters, copies standard input to standard output, and handles special characters.
- `tee` saves a copy of standard output to a file while still displaying at the terminal.
- `wc` (word count) displays the number of lines, words, and characters in a file or group of files.
- `cut` extracts columns from a file.
- `less` views files a page at a time and allows scrolling in both directions.
- `head` displays the first few lines of a file or data stream on standard output. By default, it displays 10 lines.
- `tail` displays the last few lines of a file or data stream on standard output. By default, it displays 10 lines.
- `strings` extracts printable character strings from binary files.
- The `z` command family is used to read and work with compressed files.