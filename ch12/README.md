# Chapter 12: User Environment

## Identifying the current user
```sh
# identify the current user
$ whoami
# list the currently logged-on users
$ who
```

## User startup files
- The command shell program (generally bash) uses one or more startup files to configure the user environment.
- Files in the `/etc` directory define global settings for all users, while initialization files in the user's home directory can include and/or override the global settings.

## Order of the startup files
1. `/etc/profile`
2. `~/.bash_profile`
3. `~/.bash_login`
4. `~/.profile`

- Most commonly, users only fiddle with `~/.bashrc`, as it is invoked every time a new command line shell initiates, or another program is launched from a terminal window, while the other files are read and executed only when the user first logs onto the system.

## Creating aliases
- You can create customized commands or modify the behavior of already existing ones by creating aliases
- Most often, these aliases are placed in your ~/.bashrc file so they are available to any command shells you create
```sh
# removes an alias
$ unalias
# list aliases
$ alias
```

## Basics of users and groups
- All Linux users are assigned a unique user ID (uid), which is just an integer; normal users start with a uid of 1000 or greater.
- Linux uses groups for organizing users. Groups are collections of accounts with certain shared permissions.

```sh
# add new user
$ sudo useradd bjmoose
# remove user
$ sudo userdel bjmoose
# give information about the current user
$ id
# add new group
$ sudo /usr/sbin/groupadd anewgroup
# remove group
$ sudo /usr/sbin/groupdel anewgroup
# List the groups the user already belongs to
$ groups rjsquirrel
# Add a user to an existing group
$ sudo /usr/sbin/usermod -a -G anewgroup rjsquirrel
```

## The root Account
- You can use `sudo` to assign more limited privileges to user accounts. On a temporary basis for a specific subset of commands.
- When assigning elevated privileges, you can use the command `su` (switch or substitute user) to launch a new shell running as another user (you must type the password of the user you are becoming)
- Granting privileges using `sudo` is less dangerous and is preferred. By default, `sudo` must be enabled on a per-user basis.
- sudo configuration files are stored in the `/etc/sudoers` file and in the `/etc/sudoers.d/` directory.

## Environment variables
- Environment variables are quantities that have specific values which may be utilized by the command shell, such as bash, or other utilities and applications.
- There are a number of ways to view the values of currently set environment variables; one can type `set`, `env`, or `export`.
- By default, variables created within a script are only available to the current shell; child processes (sub-shells) will not have access to values that have been set or modified
- Allowing child processes to see the values requires use of the `export` command.

Task | Command
--- | ---
Show the value of a specific variable | echo $SHELL
Export a new variable value | export VARIABLE=value (or VARIABLE=value; export VARIABLE)
Add a variable permanently | 1. Edit ~/.bashrc and add the line export VARIABLE=value. 2. Type source ~/.bashrc or just . ~/.bashrc (dot ~/.bashrc); or just start a new shell by typing  bash

- `HOME` is an environment variable that represents the home (or login) directory of the user
- `cd` without arguments will change the current working directory to the value of `HOME`

- `PATH` is an ordered list of directories (the path) which is scanned when a command is given to find the appropriate program or script to run. Each directory in the path is separated by colons (:)
- In the example `:path1:path2`, there is a null directory before the first colon (:). Similarly, for `path1::path2` there is a null directory between path1 and path2
```sh
# prefix a private bin directory to your path
$ export PATH=$HOME/bin:$PATH
```

- The environment variable `SHELL` points to the user's default command shell (the program that is handling whatever you type in a command window, usually bash)

**The PS1 Variable and the Command Line Prompt**
- Prompt Statement (PS) is used to customize your prompt string in your terminal windows to display the information you want.
- `\u` - User name
- `\h` - Host name
- `\w` - Current working directory
- `\!` - History number of this command
- `\d` - Date

```sh
$ echo $PS1
$ export PS1=`\u@\h:\w$ `
student@example.com:~$ # new prompt
```

## Recalling previous commands
- To view the list of previously executed commands, you can just type `history` at the command line
- This information is stored in `~/.bash_history`

Key | Usage
--- | ---
Up/Down arrow keys | Browse through the list of commands previously executed
!! (Pronounced as bang-bang) | Execute the previous command
CTRL-R | Search previously used commands

## Keyboard shortcuts
Keyboard Shortcut | Task
--- | ---
CTRL-L | Clears the screen
CTRL-D | Exits the current shell
CTRL-Z | Puts the current process into suspended background
CTRL-C | Kills the current process
CTRL-H | Works the same as backspace
CTRL-A | Goes to the beginning of the line
CTRL-W | Deletes the word before the cursor
CTRL-U | Deletes from beginning of line to cursor position
CTRL-E | Goes to the end of the line
Tab | Auto-completes files, directories, and binaries

## File ownership
- In Linux and other UNIX-based operating systems, every file is associated with a user who is the owner. Every file is also associated with a group (a subset of all users) which has an interest in the file and certain rights, or permissions: read, write, and execute.

Command | Usage
--- | ---
`chown` | Used to change user ownership of a file or directory
`chgrp` | Used to change group ownership
`chmod` | Used to change the permissions on the file, which can be done separately for owner, group and the rest of the world (often named as other)

- Files have three kinds of permissions: read (r), write (w), execute (x). These are generally represented as in `rwx`.
- These permissions affect three groups of owners: user/owner (u), group (g), and others (o).
- There are a number of different ways to use chmod. For instance, to give the owner and others execute permission and remove the group write permission:

```sh
$ ls -l somefile
-rw-rw-r-- 1 student student 1601 Mar 9 15:04 somefile
$ chmod uo+x,g-w somefile
$ ls -l somefile
-rwxr--r-x 1 student student 1601 Mar 9 15:04 somefile
```

- This kind of syntax can be difficult to type and remember, so one often uses a shorthand which lets you set all the permissions in one step. This is done with a simple algorithm, and a single digit suffices to specify all three permission bits for each entity. This digit is the sum of:
    - 4 if read permission is desired
    - 2 if write permission is desired
    - 1 if execute permission is desired.
- Thus, 7 means read/write/execute, 6 means read/write, and 5 means read/execute.

```sh
$ chmod 755 somefile
$ ls -l somefile
-rwxr-xr-x 1 student student 1601 Mar 9 15:04 somefile

# example of chown
$ sudo chown root:root file1

# example of chgrp
$ sudo chgrp bin file1
```

## Summary
- Linux is a multi-user system.
- To find the currently logged on users, you can use the `who` command.
- To find the current user ID, you can use the `whoami` command.
- The `root` account has full access to the system. It is never sensible to grant full root access to a user.
- You can assign root privileges to regular user accounts on a temporary basis using the `sudo` command.
- The shell program (bash) uses multiple startup files to create the user environment. Each file affects the interactive environment in a different way. `/etc/profile` provides the global settings.
- Advantages of startup files include that they customize the user's prompt, set the user's terminal type, set the command-line shortcuts and aliases, and set the default text editor, etc.
- An environment variable is a character string that contains data used by one or more applications. The built-in shell variables can be customized to suit your requirements.
- The `history` command recalls a list of previous commands, which can be edited and recycled.
- In Linux, various keyboard shortcuts can be used at the command prompt instead of long actual commands.
- You can customize commands by creating aliases. Adding an alias to `/.bashrc` will make it available for other shells.
- File permissions can be changed by typing `chmod` permissions filename.
- File ownership is changed by typing `chown owner filename`.
- File group ownership is changed by typing `chgrp group filename`.

