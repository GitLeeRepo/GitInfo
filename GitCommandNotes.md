# Overview and Credits

An organized collection of my notes from various sources, with the excellent [Git Pro Book v2](https://git-scm.com/book/en/v2/) online book by Scott Chacon and Ben Straub being the primary source.  All the content of their book is licensed under the [Creative Commons Attribution Non Commercial Share Alike 3.0 license](https://creativecommons.org/licenses/by-nc-sa/3.0/). 

# Terminology

* Local Reposistory - the repository on your local system. The .git directory.  When you do a **git commit** the versioned files are added here.
* Working Directory (Working Tree) - that area of the local repository where you work.  Visible to the local operating system.  This is where the files go when you do a **git checkout** (pulled from the .git repository directory).
* Index (Staging Area) - Files to be committed,  Use the **git add** command to add files to the index,
* Upstream Reposistory - the remote repository (such as GitHub).  The default remote is called origin, which is created when you do a clone or use the **git remote add** command.  List remotes with the **git remote -v**.

# Important Directories

* /etc/ - System wide (user independent files (\Program Files\git\etc on Windows). Use **git config --system** to interact with this file.
* ~/.gitconfig - User wide configurations (\Users\username\.gitconfig on WIndows).  Use **git config --global** to interact with this file.
* The local Repository .git/config file.

Note the precedence for these files.  The local takes highest precedence, then the global, and finally the system wide.

An example of what's stored here is the **user.name** and **user.email** settings.

# Git config

## Username and email config settings

* **git config --global user.name="\<username\>"** - set username
* **git config --global user.name** - display username
* **git config --global user.email="\<email\>"** - set email
* **git config --global user.email** - display email

## Configure editor to be used by git

* **git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -nosession"**
* **git config --global core.editor** - display the currently set editor

## Display config settings

* **git config --list** 

# Git initialization

## With git init

* **git init** - init repo in current dir
* **git init \<repositoryname\>** - init repo in specified repository dir

## With git clone

* **git clone https://github.com/GitLeeRepo/GitInfo.git** - will create git repository on the local system called GitInfo.
* **git clone https://github.com/GitLeeRepo/GitInfo.git MyGitInfo** - will create git repository on the local system called MyGitInfo.

Note that git clone will create the directory, initialize the repository, checks out the latest version of the files to the working directory, and set the remote origin equal to the url supplied with git clone.


# Git status

* **git status** - status of repo

# Git add

* **git add \<filename\>** - add file to staging (uncommitted)

* **git add .** - add all files to staging

* **git add --all** - add all files and files deleted to staging

Note that if a directory is supplied rather than a file name the entire directory and its files and subdirectories will be added.

Note that git add both adds currently untracked files to staging (and thus they become tracked files) and adds modified tracked files to staging.  It can also be used to mark merge-conflicted files as resolved.

Note that if you modify a file staged by git add after it was staged, the second version will be unstaged, with the first version being what will be committed.  You must run git add again to stage the latest revision.

# Git rm

* **git rm \<filename\>** - remove the file from your working directory and the index (Staging)
* **git rm \<filename\> --cached** - remove from the index (Staging) only.

Note that if you use a wildcard for filename you need to preceed the wild card with a \\ (backslash) so that git doesn't expand the file list in addition to the shell.  For example **git rm \\\***.

# Git rename/move

* **git mv \<oldname\> \<newname\>**

Note that if you renamed the file outside of git then you need to do a **git rm \<oldname\>** followed by **git add \<newname\>**.

# Unstaging a file

* **git reset HEAD \<filename\>**

# Reverting a file

* **git checkout -- \<filename\>** - will replace the modified file with the file from the last commit.

# Git commit

* **git commit** - commit the files in staging (will bring up text editor to add message)

* **git commit -m "'<the message\>"** - commit the files adding a message

* **git commit -a** - lets you bypass the git add that is used to add the files to staging first.  It will commit all modifed files regardless of whether they were staged first.

# Working with remote repositories

## For remote branch and checkout commands refer to:

* [Remote branch commands][## Git remote branch commands]

* [Remote checkout commands][## Git remote checkout commands]

## Displaying remote repositories

* **git remote -v** - get a list of remote repositories and their URLs that were previously added with either a **git clone \<remote URL\>** or a **git remote add \<Remote Name\> \<remote URL\>** command.  The -v arguement specifies that the URLs should be included, otherwise it's just the remote name.

## Adding Remote name references

* **git remote add \<remote name\> \<remote URL\>** - the shorter \<remote name\> can now be used to refer to the remote instead of the URL, in for example push and pull commands.

## Remote Fetching (clone, fetch, merge, pull)

* **git clone \<remote URL\>** - get a remote repo cloned to local repository.  It will create the repository, so don't use this if the repository already exists locally.  Refer to clone comments above for more details.

* **git fetch \<remote name or remote URL\>** - brings any remote changes into your repository (.git) but not your working directory, you must merge or pull to do that.  This is useful to see what changes have taken place on the remote since you cloned or pulled.

* **git merge origin/\<branchname\>**

* **git pull origin** - Does both a fetch and a merge so your working directory is updated as well as your .git repository location.

## Git push to remote

* **git push \<remote name or URL\> \<local branch name\>** - for example **git push origin master** pushes your master branch to the remote. The branch name is optional, if excluded it will be your current branch.  Will create a branch with the same name on the remote.

* **git push \<remote name or URL\> \<local branch name\>:\<remote branch name\>** - will push your local branch to the remote giving it the remote branch name specified.

Note that if the remote branch has been changed by someone else since you last pulled then this will not work.  You have to first pull and merge their changes into your changes and then attempt to push again.

## Show remote info

* **git remote show \<remote name or URL\>** - displays info on the remote repository such as the fetch and push URLs, what remote branches there are and whether it is tracked, what remote branch your master pulls from (ex remote master) and what remote branch your master pushes to (ex remote master)

## Renaming a remote

* **git remote rename oldname newname**

## Removing a remote name

* **git remote remove \<remote name\>** - same as **git remote rm \<remote name\>**

# Git branch

## Overview

Text

## Git local branch commands

* **git branch** - list the branches

* **git branch \<branchname\>** - add the named branch

* **git branch -d \<branchname\>** - delete the branch (will warn if branches not merged)

* **git branch -D \<branchname\>** - will force delete even if not merged

## Git local checkout commands

* **git checkout \<branchname\>** - switch to the specified branch

* **git checkout -b \<branchname\>** - create the branch and switch to it

* **git checkout -b \<tagname\> \<branchname\>** - checkout the merge with the specified tag to the specified branch which is created

## Git remote branch commands

## Git remote checkout commands

* **git checkout -b \<local branch name\> origin/\<server branch name\>** - checkout the remote branch to the local branch

# Git diff

* **git diff** - to see the differences between what has **not** been staged and your last commit
* **git diff** --staged - to see the differences between what **has** been staged and your last commit

Note that if you want to use an external diff compare tool use the **git difftool** command.  Run **git difftool --tool-help** to see a list of external diff tools on your system and those that are supported but not currently on the system.  If no external tool is used (you're using **git diff** not **git difftool**) then an internal vim/man page like viewer is used.

# Git log

* **git log** - displays a history of the commits, including the message, the user name and email, the date and time, and the SHA-1 checksum.  Note that most recent commit is displayed first.
* **git log -p** - displays the commit history along with the differences between the commits
* **git log -\<\#\>** - displays only the specified number of commits, for example **git log -2** shows only the last two commits.
* **git log --stat** - displays various statistcs associated with the commits (the number of files changed, the number of insertions, the number of deletions, etc).

# Git tag

* **git tag -a \<tagname\> -m "\<tag message\>"** - adds an annotated tag (the -a) to the current merge.  Annotated tags are usually what you want rather than temporary tags which is what you get without the -a arg.

* **git tag -a \<tagname\> \<commit checksum\>** - tags the specified prior merge based on its checksum (you don't have to enter the whole thing).  You can get the prior merge checksums by running the **git log** command.

Note that tags are not automatically pushed to the remote when you do a push.  You must either push the specified tagname or all your tags, for example:

* **git push origin \<tagname\>**

* **git push orign --tags** - will push all your tags in your current repository to the remote server.

# Config global user and email

## Set username

* **git config --global user.name="\<username\>"**

## Show username

* **git config --global user.name**

## Set email

* **git config --global user.email "\<email\>"**

## Show email

* **git config --global user.email**