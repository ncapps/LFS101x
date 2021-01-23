# Chapter 7: Command Line Operations

- A **terminal emulator** program emulates (simulates) a standalone terminal within a window on the desktop. By this, we mean it behaves essentially as if you were logging into the machine at a pure text terminal with no running graphical interface. Most terminal emulator programs support multiple terminal sessions by opening additional tabs or windows.

## Basic utilities
```sh
cat # used to type out a file (or combine files)
head # used to show the first few lines of a file
tail # used to show the last few lines of a file
man # used to view documentation.
```

- Most input lines entered at the shell prompt have three basic elements:
    - Command: the name of the program you are executing
    - Options: one or more options that modify what the command may do
    - Arguments: what the command operates on

## Rebooting and shutting down
```sh
shutdown # shut down the system
reboot # reboot the system
```

## Locating applications
- In general, executable programs and scripts should live in `/bin`, `/usr/bin`, `/sbin`, `/usr/sbin`, or somewhere under `/opt`

```sh
which # locate programs
# OR
whereis # alternative to locate programs
```

## Accessing directories
```sh
pwd # Displays the present working directory
cd ~ # Change to your home directory
cd .. # Change to parent directory
cd - # Change to previous directory
```

## Absolute and relative paths
- **Absolute pathname**: An absolute pathname begins with the root directory and follows the tree, branch by branch, until it reaches the desired directory or file. Absolute paths always start with /.
- **Relative pathname**: A relative pathname starts from the present working directory. Relative paths never start with /.

## Exploring the filesystem
```sh
cd / # Change current directory to the root (/) directory
ls # List the contents of the present working directory
ls -a # List all files, including hidden files and directories
tree # Displays a tree view of the filesystem
```

## Hard links and soft (symbolic) links
- The ln utility is used to create hard links and (with the -s option) soft links, also known as symbolic links or symlinks. These two kinds of links are very useful in UNIX-based operating systems.
- Symbolic links take no extra space on the filesystem (unless their names are very long). They are extremely convenient, as they can easily be modified to point to different places. An easy way to create a shortcut from your home directory to long pathnames is to create a symbolic link.
- soft links can point to objects even on different filesystems, partitions, and/or disks and other media,  which may or may not be currently available or even exist.

```sh
$ touch file1
$ ln file1 file2 # Create hard link: file2
$ ls -li file1 file2 # List files with inode number and count

$ ln -s file1 file3
$ ls -li file1 file3
```

## Working with files
- **Viewing files**
```sh
cat # View small files
tac # View file backwards
less # Used to view larger files because it is a paging program.
# Use / to search for a pattern forward
# Use ? to serach for a pattern backward
tail -n 10 # Print the last n lines of a file
head -n 10 # Print the first n lines of a file
```

- **Creating files or directories**
```sh
touch sampfile # Create empty file
mkdir sampdir # Creates sampdir directory
rmdir # Removes empty directory
rm -rf # Remove a directory and all of its contents
```

- **Moving, Renaming, or Removing a file**
```sh
mv # Rename a file
rm # Remove a file
rm -f # Forcefully remove a file
rm -i # Interactively remove a file
```

- **Modifying the Command Line Prompt**
The `PS1` variable is the character string that is displayed as the prompt on the command line. Most distributions set `PS1` to a known default value, which is suitable in most cases. However, users may want custom information to show on the command line.
```sh
$ echo $PS1
\[\e[0;32m\]\u \[\e[39m\]➜\[\e[39m\] \[\e[34;1m\]~\[\e[39m\] \[\e[0;37m\]$ \[\e[39m\]
```

## Standard File Streams
- When commands are executed, by default there are three standard file streams (or descriptors) always open for use: standard input (standard in or `stdin`), standard output (standard out or `stdout`) and standard error (or `stderr`).

- In Linux, all open files are represented internally by what are called file descriptors. Simply put, these are represented by numbers starting at zero. `stdin` is file descriptor 0, `stdout` is file descriptor 1, and `stderr` is file descriptor 2

name | symbolic name | value
--- | --- | ---
standard input | stdin | 0
standard output | stdout | 1
standard error | stderr | 2

## I/O Redirection
```sh
# Change the input source to be a file
$ do_something < input-file

# Send the output to a file
$ do_something > output-file

# Redirect stderr to a file
$ do_something 2> error-file

# Write stdout and stderr to the same file
$ do_something > all-output-file 2>$1
# OR
$ do_something >& all-output-file
```

## Pipes
- The UNIX/Linux philosophy is to have many simple and short programs (or commands) cooperate together to produce quite complex results, rather than have one complex program with many possible options and modes of operation
```sh
# A pipeline allows Linux to combine the actions of several commands into one
$ command1 | commmand2 | command3
```

## Searching for files
- `locate` utilizes a database created by the `updatedb` utility
- `find` recurses down the filesystem tree from the given directory and locates files that match specified conditions
- Another good use of `find` is being able to run commands on the files that match your search criteria. The `-exec` option is used for this purpose.
```sh
# list fiels and directories with both zip and bin in their name
$ locate zip | grep bin

# Sample exercise
$ locate -r '\.doc$'
/home/vagrant/tmp/example.doc

# Find log files
$ sudo find / -name "*.log"

# Search for files and directories named gcc
$ find /usr -name gcc

# Search only for directories named gcc
$ find /usr -type d -name gcc

# Search only for regular files named gcc
$ find /usr -type f -name gcc

# Find and remove all fiels that end with .swp
$ find -name "*.swp" -exec rm {} ';'

$ find / -ctime 3 # Find files based on inode metadata time (days)
$ find / -atime 3 # Find files based on accessed/last read time
$ find / -mtime 3 # Find files based on modified/last written time
$ find / cmin 3 # File files based on inode meta time (minutes)

# Find files based on size
$ find / -size 0
```

## Wildcards and matching file names
Wildcard | Result
--- | ---
`?` | Matches any single character
`*` | Matches any string of characters
`[set]` | Matches any character in the set of characters
`[!set]` | Matches any character not in the set of characters

## Package Management Systems on Linux
- The core parts of a Linux distribution and most of its add-on software are installed via the Package Management System.
- There are two broad families of package managers: those based on **Debian** and those which use **RPM** as their low-level package manager.
- Both package management systems operate on two distinct levels: a low-level tool (such as dpkg or rpm) takes care of the details of unpacking individual packages, running scripts, getting the software installed correctly
- A high-level tool (such as apt, yum, dnf or zypper) works with groups of packages, downloads packages from the vendor, and figures out dependencies
- The Advanced Packaging Tool (apt) is the underlying package management system that manages software on Debian-based systems.
- yum is an open source command-line package-management utility for the RPM-compatible Linux systems that belongs to the Red Hat family.
- [Basic packaging commands](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/f478e1c28b54f5df1d53ef1bc855b2e3/asset-v1:LinuxFoundationX+LFS101x+3T2018+type@asset+block/Basic_Packagaing_Commands.pdf)

## Summary
- Virtual terminals (VT) in Linux are consoles, or command line terminals that use the connected monitor and keyboard.
- A terminal emulator program on the graphical desktop works by emulating a terminal within a window on the desktop.
- There are two types of pathnames: absolute and relative.
    - An absolute pathname begins with the root directory and follows the tree, branch by branch, until it reaches the desired directory or file.
    - A relative pathname starts from the present working directory.
