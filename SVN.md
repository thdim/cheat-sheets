`go to w/`


`svn status -u` compare docker SVN with the portal SVN


* _changed in the certal repository_  
M _modified locally?_  
? _don't know_  

`svn update <filename>` Merge one file  
`svn update .` Merge all with M and * - (r) mark resolved  
`svn revert <filename>` Revert to the latest from the live repository  
`rm <filename>` and `rm -f <folder>`  remove files from docker

## New Branch

1. Right click in /trunk and go to "TortoiseSVN" -> "Branch/tag"  
2. Go to /src/braches and type svn checkout <url of the branch>  
