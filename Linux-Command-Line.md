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

## Nano

`nano <filename>` _open file with nano text editor_  
`^O` or `^S` _save changes_  
`^W` _search forward to current position_  

## Hostinger SSH
`rm -rf /.cagefs/tmp/*` _clean temp, reduce "Order Inodes"_  
`find domains/ -type f | wc -l` _count all files in the domains/_  
`tree domains/` _list all files in a tree_  
`rm -r *` _clean all files and directories (first navigate into the folder)_
