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
