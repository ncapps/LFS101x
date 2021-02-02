# Chapter 11: Text Editors

## Creating files without using an editor
```sh
# echo
$ echo line one > myfile
$ echo line two >> myfile

# use cat combinde with redirection
$ cat << EOF > myfile
> line one
> line two
> line three
> EOF
$
```

## Introduction to vi
- Typing `vimtutor` launches a short but very comprehensive tutorial for those who want to learn their first `vi` commands.
- vi has three modes: Command, Insert, and Line
- [commands for vi](https://prod-edxapp.edx-cdn.org/assets/courseware/v1/dd0b84d079c38cca37826462d16a904e/asset-v1:LinuxFoundationX+LFS101x+3T2018+type@asset+block/VI_Editor.pdf)

## Working with files in vi

Command | Usage
--- | ---
`vi myfile` | Start the editor and edit myfile
`vi -`r myfile | Start and edit myfile in recovery mode from a system crash
`:r file2` | Read in file2 and insert at current position
`:w` | Write to the file
`:w` myfile | Write out to myfile
`:w!` file2 | Overwrite file2
`:x or :wq` | Exit and write out modified file
`:q` | Quit
`:q!` | Quit even though modifications have not been saved

## Changing Cursor Positions in vi

Key | Usage
--- | ---
`arrow keys` | To move up, down, left and right
`j or <ret>` | To move one line down
`k` | To move one line up
`h or Backspace` | To move one character left
`l or Space` | To move one character right
`0` | To move to beginning of line
`$` | To move to end of line
`w` | To move to beginning of next word
`:0 or 1G` | To move to beginning of file
`:n or nG` | To move to line n
`:$ or G` | To move to last line in file
`CTRL-F or Page Down` | To move forward one page
`CTRL-B or Page Up` | To move backward one page
`^l` | To refresh and center screen

## Searching for test in vi

Command | Usage
--- | ---
`/pattern` | Search forward for pattern
`?pattern` | Search backward for pattern

Key | Usage
--- | ---
`n` | Move to next occurrence of search pattern
`N` | Move to previous occurrence of search pattern

## Working with Text in vi

Key | Usage
`a` | Append text after cursor; stop upon Escape key
`A` | Append text at end of current line; stop upon Escape key
`i` | Insert text before cursor; stop upon Escape key
`I` | Insert text at beginning of current line; stop upon Escape key
`o` | Start a new line below current line, insert text there; stop upon Escape key
`O` | Start a new line above current line, insert text there; stop upon Escape key
`r` | Replace character at current position
`R` | Replace text starting with current position; stop upon Escape key
`x` | Delete character at current position
`Nx` | Delete N characters, starting at current position
`dw` | Delete the word at the current position
`D` | Delete the rest of the current line
`dd` | Delete the current line
`Ndd` or `dNd` | Delete N lines
`u` | Undo the previous operation
`yy` | Yank (copy) the current line and put it in buffer
`Nyy` or `yNy` | Yank (copy) N lines and put it in buffer
`p` | Paste at the current position the yanked line or lines from the buffer.

