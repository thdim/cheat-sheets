## Basic Command Structure  

`command -options arguments`  

__Understand -options arguments with ncal__  
`ncal` _display calendar of the current month_   
`ncal -j` _days count from the start of the year (not the month)_  
`ncal -M` _start the week on Monday (default Sunday)_  
`ncal -3` _previous current and next month_  
`ncal -j3` _combine options_  
`ncal -A 2` _2 months after the current month_  
`ncal 1982` _display calendar of the given year_  
`ncal august 1982` _and month_  
`who -a` _shows information for the logged in users_  

__man (manual) command__  
`man date` _options and arguments manual_  
`q` _exit manual_  
`h` _navigation help of the man page_  
`up & down key` _move the manual one line up or down_  
`space or f` _move the manual one page down (forward)_  
`b` _move the manual one page up (back)_
`\` _search for a text_  

__type & which__  
`type clear` _will return the type of the command_  
`type cd` _build-in shell command_  
`which clear` _the exact location of the executable_  
`help cd` _for build-in shell commands (they don't have man)_  

## Navigation  

`pwd` _print working directory (where am I?)_  
`ls` _list the contents of the current directory_  
`ls /etc/` _list the contents of the /etc/_  
`ls -l` _long info_  
`ls -a` _include all (hidden)_  
`ls -h` _human readable size_  
`cd folder/` _change directory_  
`cd ..` _go back one level_  
`cd /` _root_  
`cd ~` _home_  

__basic folders__  
`/bin` _executable programs (binaries)_  
`/etc` _configs and init scripts_  
`/media` _connect to removable media (USB, Disks)_  
`/var` _logs, caches, output of executables_  
`/root` _the "home" of the root user_  
`/usr` _executable files (installed)_  

## Creating Files & Folders  

`touch <filename>` _create new file (changes the modification times if file exist)_  
`touch <filename> <filename>` _create multiple new files_  
`file <filename>` _determines the type of a file (not by extension) and returns info about it_  
`mkdir <folder>` _create new directory_  
`mkdir <folder> <folder>` _create multiple new directories_  
`mkdir -p <parent>/<child>` _create parent directory (and child)_  

## Delete, Copy, Move

__Delete__  
`rm <file>` _delete a file_  
`rm <file> <file>` _seperate with space to remove multiple files_  
`rm -d <dir>` OR `rmdir <dir>` _remove empty directories_  
`rm -r <dir>` _remove directories and everything inside (recursively)_  
`rm -ri <dir>` _i = interactive, prompts removal questions (recursively)_  

__Move__  
`mv <file> <file> <target_dir>` _moves one or more files in a directory_  
`mv <dir>/ <dir>/ <target_dir>/` _moves one or more directories in a directory (target dir must exist)_  

__Copy__  
`cp <source> <target>` _copy source to target_  
`cp -r <source_dir> <target_dir>` _-r is needed to copy directories_  

## Shortcuts & History  

`ctrl + l` _clear screen_  
`ctrl + a` _move at the Start of the line_  
`ctrl + e` _move in the End of the line_  

`alt + f` _moves the cursor one word forward_  
`alt + b` _moves the cursor one word backward_  

`history | less` _will show the cmds history per page (arrows will go down per line, shift will go down per page)_  
`!<num-in-history>` _will execute the cmnd in the given line of history_  

## Files

`cat <file>` _read and display the contents of a file_  
`less <file>` _read and interactivly display the contents of a file_  
`tac <file>` _like cat but in reverse order (start to end)_  
`tail -<num> <file>` _Show the last n number of lines in a file_  
`head -<num> <file>` _SHow the top n number of lines in a file_  
`wc -l <file>` _Count the number of lines in a file_  
`wc -w <file>` _Count the number of words in a file_  
`sort <file>` _Sort the content of a file with ABC mode_  
`sort -r <file>` _Sort in reversed order_  

## Nano

`nano <filename>` _open file with nano text editor_  
`ctrl O` or `ctrl S` _save changes_  
`ctrl + W` _search forward to current position_  
`ctrl + \` _search and replace_  
`ctrl + /` _go to line_  

## Redirects

### Redirect Standard Output
_Standard Output:_ Will output the result of a command in the console  
__WARNING:__ Using redirect will overwrite the destination filename  

`command > filename` _Will output the result of the "command" into the "filename"_  
`ls -l /usr/bin > list.txt` _Example_  

### Appending Standard Output
`date >> log.txt` _Will append the result of the date command into the log.txt (add it into the end of the file)_  

## Hostinger SSH
`rm -rf /.cagefs/tmp/*` _clean temp, reduce "Order Inodes"_  
`find domains/ -type f | wc -l` _count all files in the domains/_  
`tree domains/` _list all files in a tree_  
`rm -r *` _clean all files and directories (first navigate into the folder)_
