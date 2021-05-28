# Git & GitHub

## Configurations (blames)

`git config --list`  
`git config --global user.name "Themistoklis Dimitriou"`  
`git config --global user.email themis.dimitriou@outlook.com`  

## 

`#` _there are changes that are not yet inside the repository_  
`+` _new files that are staged to be added to the repository_  
`*` _there are changes available (?)_  


## Basic Commands
`git init` _initialize repository (create .git)_  
`git add <filename>` _stage a file_  
`git commit -m "<message>"` _commit staged files_  
`git add -A && git commit -m "<message>"` _add all files and commit_  
`git commit -a -m "<message>"` _-a is a shortcut for add all_  
`git add .` _add all modified files_  

## Github
__push__  
`git remote add origin https://github.com/thdim/youingreece.git`  
`git push origin master`  

__pull__    
`git pull origin master`  


__ FROM MS NOTES ___

## Setup a tracking
git branch --set-upstream-to=origin/master master
git pull (now you can just pull)

### Changes and logs
`git status`
`git diff <filename>` or `<sha code>` _get differences_
`git log` _Find log file  
`git log --graph` (the log file with branch merges info)  
`git log --pretty=oneline` (show all commits in "one line per commit" format)  
`git annotate <filename>` (like log but for a specific file)  
`git show <sha>` (more info about a specific commit)  
`git show HEAD` (info about the latest commit)  
`git show HEAD~1` (HEAD - 1 commit)  

## Clone
`git clone https://github.com/thdim/html5boilerplate.com.git`  

## Undoing Changes  
`git checkout -- <filename>` (undo non commited changes)  
`git reset HEAD <filename>` (undo added files, then you can checkout to restore)  
`git checkout <sha> <filename>` (restore a version based on the sha, git log to find sha's)  

git reset HEAD . (Unstage changes of all files)
git checkout -- . (restore all changes)

## Branches
git branch <name> (Create a new branch)
git branch (Shows existing branches)
git checkout <branch-name> (Switch to another branch)
git checkout -b <branch-name> (Create and switch to a new branch)
git push origin <branch> (Send the branch to github)
git checkout --track origin/test (Creates test branch locally, switchs to it and tracks it following the github test branch *NOT WORKING)

## Merge branches
git checkout <branch> (Switch to the destination branch)
git merge <source-branch> <destination-branch> (merge source to destination)
git branch -d <source-branch> (delete source)
git push origin <source-branch> (push changes to github)
git merge --abort (abort last merge)

## Type of merges
// Fast-Forward Merge (the child branch adds a new future without changes in the parent branch)
// In case of a conflict we need to remove the additional git lines manually (<<<< HEAD ===== >>>>> sha)

## Tags
git tag -a <version> -m "<msg>" (save current status into a version)
git tag -a <version> <sha> -m "<msg>" (add tag to the given sha version)
git show <version> (shows info about a specific version/tag)
git push origin --tags (just git push will not do the job, you need the --tags to push tags)

## Ignore files & folders
.gitignore (filename that contains paths that git should ignore, can include specific files or folders)
https://github.com/github/gitignore (A collection of useful .gitignore templates)
