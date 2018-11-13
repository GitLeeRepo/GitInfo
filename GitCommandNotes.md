# Overview

An organized collection of my notes from various sources, with the excellent [Git Pro Book v2](https://git-scm.com/book/en/v2/) online book by Scott Chacon and Ben Straub being the primary source.  All the content of their book is licensed under the [Creative Commons Attribution Non Commercial Share Alike 3.0 license](https://creativecommons.org/licenses/by-nc-sa/3.0/). 

# References

## My Own Notes

* [GitHubSpecific](https://github.com/GitLeeRepo/GitInfo/blob/master/GitHubSpecific.md#overview)
* [GitReferences](https://github.com/GitLeeRepo/GitInfo/blob/master/GitReferences.md#overview)
* [MarkdownTagsAndTips](https://github.com/GitLeeRepo/GitInfo/blob/master/MarkdownTagsAndTips.md#overview)

# Terminology

* Local Repository - the repository on your local system. The .git directory.  When you do a **git commit** the versioned files are added here.
* Working Directory (Working Tree) - that area of the local repository where you work.  Visible to the local operating system.  This is where the files go when you do a **git checkout** (pulled from the .git repository directory).
* Index (Staging Area) - Files to be committed,  Use the **git add** command to add files to the index,
* Upstream Repository - the remote repository (such as GitHub).  The default remote is called origin, which is created when you do a clone or use the **git remote add** command.  List remotes with the **git remote -v**.

# Important Directories

* /etc/ - System wide (user independent files (\Program Files\git\etc on Windows). Use **git config --system** to interact with this file.
* ~/.gitconfig - User wide configurations (\Users\username\.gitconfig on Windows).  Use **git config --global** to interact with this file.
* The local Repository .git/config file.

Note the precedence for these files.  The local takes highest precedence, then the global, and finally the system wide.

An example of what's stored here is the **user.name** and **user.email** settings.

# .gitignore

* The files and directories listed in .gitignore will not be added to the repository.  An example of a filename and directory entry in .gitignore (notice the directory name has a forward slash after it:

  ```
  filename.txt

  dirname/
  ```

* Note: If you notice a file or directory doesn't seem to be ignore by a .gitignore entry, then remove it from the cache with:

  ```
  git rm --cached filename
  ```

  or

  ```
  git rm -r --cached directoryname
  ```

# Git initialization

## With git init

* **git init** - init repo in current dir
* **git init \<repositoryname\>** - init repo in specified repository dir

## With git clone

* **git clone https://github.com/GitLeeRepo/GitInfo.git** - will create git repository on the local system called GitInfo.
* **git clone https://github.com/GitLeeRepo/GitInfo.git MyGitInfo** - will create git repository on the local system called MyGitInfo.

Note that git clone will create the directory, initialize the repository, checks out the latest version of the files to the working directory, and set the remote origin equal to the URL supplied with git clone.


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

Note that if you use a wildcard for filename you need to proceed the wild card with a \\ (backslash) so that git doesn't expand the file list in addition to the shell.  For example **git rm \\\***.

# Git rename/move

* **git mv \<oldname\> \<newname\>**

  Note that if you renamed the file outside of git then you need to do a **git rm \<oldname\>** followed by **git add \<newname\>**.

# Unstaging a file

* **git reset HEAD \<filename\>**

```bash
# unstage all the files
git reset HEAD *
```

# Reverting a file -  Discard changes

* **git checkout -- \<filename\>** - will replace the modified file with the file from the last commit.  Note the **two dashes** after **checkout** are part of the command and need to be **included**.

This is useful when you get a **merge error** during **git pull** informing you that you have **untracked changes**.  If you don't want to keep any of the changes on the **local host** then run this command.

```bash
git checkout -- * 
```

Note the **two dashes** after the **checkout**.

Note: if you run this command, for example **`git checkout *`**, and it doesn't remove the **working directory files**, it likely indicates you **never previously committed them**.  In this case, simply **delete the files** using **rm**.

Also note that if you have **staged** some of the files that you want to **remove with checkout** then you need to **unstage them first** with **`git reset HEAD <filename>`**.

```bash
# unstage all the files
git reset HEAD *
```

# Git commit

* **git commit** - commit the files in staging (will bring up text editor to add message)
* **git commit -m "'<the message\>"** - commit the files adding a message
* **git commit -a** - lets you bypass the git add that is used to add the files to staging first.  It will commit all modified files regardless of whether they were staged first.

# Working with Remote Repositories

## For remote branch and checkout commands refer to:

* [Remote branch commands](#git-remote-branch-commands)
* [Remote checkout commands](#git-remote-checkout-commands)

## Displaying remote repositories

* **git remote -v** - get a list of remote repositories and their URLs that were previously added with either a **git clone \<remote url\>** or a **git remote add \<Remote Name\> \<remote url\>** command.  The -v argument specifies that the URLs should be included, otherwise it's just the remote name.

## Check remote status

To check with the remote is ahead of your local repository:

* **git fetch**

A useful script to check several repositories:

```bash
#!/bin/bash

for d in */ ; do
    echo "$d"
    cd $d
    git fetch
    if [ $( git rev-parse HEAD ) == $( git rev-parse @{u} ) ]
    then
        echo "Up to date"
    else
        echo ">>>>>>>>>>>>>>>>>>>>Either Remote updated (pull needed) and/or unpushed local commit"
    fi
    cd ../
    echo ""
done
```
Note this will detect if the remote is ahead, but will also trigger for a local commit not yet pushed.  Untracked or staged files should not trigger the out of sync message.  If it is the first time the fetch is run it will also display the fetch message which will indicate whether the the remote is ahead of the local, but subsequent runs will only display the above message.  A git status will also give you more detail, but this script is intended to be run on many repositories, so less detail is often desired.  Refer to my gitstatus.sh script in this repository for a script that provides status information on multiple repositories.

## Adding Remote name references

* **git remote add \<remote name\> \<remote url\>** - the shorter \<remote name\> can now be used to refer to the remote instead of the URL, in for example push and pull commands.

## Changing the URL of a remote repository

* **git remote set-url origin \<remote url\>** - replace any current URL with the specified one for the specified remote (origin in this case)

## Remote Fetching (clone, fetch, merge, pull)

* **git clone \<remote url\>** - get a remote repo cloned to local repository.  It will create the repository, so don't use this if the repository already exists locally.  Refer to clone comments above for more details.
* **git fetch \<remote name or remote url\>** - brings any remote changes into your repository (.git) but not your working directory, you must merge or pull to do that.  This is useful to see what changes have taken place on the remote since you cloned or pulled.
* **git merge origin/\<branchname\>**
* **git pull origin** - Does both a fetch and a merge so your working directory is updated as well as your .git repository location.

## Git push to remote

* **git push -u origin newbranch** -- pushes a **new branch** on the **local** to the **remote** creating the **new branch on the remote**.  Can confirm this works from using it.
* **git push \<remote name or url\> \<local branch name\>** - for example **git push origin master** pushes your master branch to the remote. The branch name is optional, if excluded it will be your current branch.  Will create a branch with the same name on the remote.
* **git push \<remote name or url\> \<local branch name\>:\<remote branch name\>** - will push your local branch to the remote giving it the remote branch name specified.

Note that if the remote branch has been changed by someone else since you last pulled then this will not work.  You have to first pull and merge their changes into your changes and then attempt to push again.

## Show remote info

* **git remote show \<remote name or url\>** - displays info on the remote repository such as the fetch and push URLs, what remote branches there are and whether it is tracked, what remote branch your master pulls from (ex remote master) and what remote branch your master pushes to (ex remote master)

## Renaming a remote

* **git remote rename oldname newname**

## Removing a remote name

* **git remote remove \<remote name\>** - same as **git remote rm \<remote name\>**

## Overwriting Local Repo with Remote

```
git fetch origin
git reset --hard origin/master
git add .
git push
```

Note: the instructions I saw stopped at **reset** but that didn't fix the conflict.  It showed the files as uncached.  I did an **add** and **push** afterwards which seemed to sync things up, i.e. The last change on the remote was still there.

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

Commands

## Git remote checkout commands

* **git checkout -b \<local branch name\> origin/\<server branch name\>** - checkout the remote branch to the local branch
* **git checkout --track origin/\<remote branch name\> - 

# Git diff

* **git diff** - to see the differences between what has **not** been staged and your last commit
* **git diff** --staged - to see the differences between what **has** been staged and your last commit

Note that if you want to use an external diff compare tool use the **git difftool** command.  Run **git difftool --tool-help** to see a list of external diff tools on your system and those that are supported but not currently on the system.  If no external tool is used (you're using **git diff** not **git difftool**) then an internal vim/man page like viewer is used.

# Git log

Note: optionally, for a specific log entry add enough of the left part of the commit checksum to the command to uniquely identify it (it doesn't take many characters)

* **git log \<optional checksum\>** - displays a history of the commits, including the message, the user name and email, the date and time, and the SHA-1 checksum.  Note that most recent commit is displayed first.
* **git log -\<\#\>** - displays only the specified number of commits, for example **git log -2** shows only the last two commits.
* **git log -p \<optional checksum\>** - displays the commit history along with the differences between the commits
* **git log --stat** - displays various statistics associated with the commits (the number of files changed, the number of insertions, the number of deletions, etc).
* **git log --pretty=oneline --abbrev-commit** - displays one line per commit, with the commit id and commit message. Also, display a much shorter (abbreviated) commit checksum, which is helpful since you will likely only need a small portion of this to identify a particular commit. 
* **git log --grep="syscalls"** - display the entry/entries associated with the grep regex pattern (syscalls in this case)

# Git tag

* **git tag -a \<tagname\> -m "\<tag message\>"** - adds an annotated tag (the -a) to the current merge.  Annotated tags are usually what you want rather than temporary tags which is what you get without the -a arg.
* **git tag -a \<tagname\> \<commit checksum\>** - tags the specified prior merge based on its checksum (you don't have to enter the whole thing).  You can get the prior merge checksums by running the **git log** command.
Note that tags are not automatically pushed to the remote when you do a push.  You must either push the specified tagname or all your tags, for example:
* **git push origin \<tagname\>**
* **git push origin --tags** - will push all your tags in your current repository to the remote server.

# Configuration Commands ad Files

Refer to:

* [git config command docs](https://git-scm.com/docs/git-config)
* [gitattributes docs](https://git-scm.com/docs/gitattributes)

## Display configuration settings

* **`git config --list`** -- list all configuration settings (system, global, local)
* **`git config --local --list`** -- list local (current repository) configuration settings
* **`git config --global --list`** -- list global (current user) configuration settings
* **`git config --system --list`** -- list system (all users) configuration settings
* **`git check-attr -a .`** -- display all the **.gitattributes** settings for the **current folder** (must be the **repository root** when using just the **dot** reference, otherwise provide the **path**)

Note: On **Windows** the **--system** had several configurations, while on **Linux** the **/etc/gitconfig** did not exist, which is fine since I am the only user.

## .gitattributes

Refer to:

* [gitattributes docs](https://git-scm.com/docs/gitattributes)

The **.gitattributes** file is placed in the **root** of the **repository** and contains **custom settings** that apply to that repository.  It uses the following **syntax**:

```
pattern	attr1 attr2 ...
```

Where **pattern** is a **path/name** of particular **file pattern**, including **wildcards** such as **`*`**.  Examples include:

```
*           text=auto
*.txt       text
*.vcproj    text eol=crlf
*.sh        text eol=lf
*.jpg       -text
```

This will ensure that **eol** is handled **automatically** for all files, which means the **.txt** will be **crlf** on Windows, and **lf** on all other systems, with overrides for explicit file endings (**crlf for .vcproj**, **lf for .sh**), with **.jpg** files being **excluded from normalization**.

In addition to **editing the .gitattributes** in the **repository root** you can run the **git check-attr -a <path>`** command to view the **settings**.

## Local Configuration

Contains settings such as:

* remote.origin.url=
* remote.origin.fetch=
* branch.master.remote=origin
* branch.master.merge=refs/heads/master

## Global Configuration

You can either change the **global configurations** using the **commands** in this section, or you can **edit** the **.gitconfig** file in your **home directory** (applies to both **Linux** and **Windows**).

```bash
git config --global --edit
# should be equivalent to
vi ~/.gitconfig
```

### Username and email config settings

* **git config --global user.name "\<username\>"** - set username
* **git config --global user.name** - display username
* **git config --global user.email "\<email\>"** - set email
* **git config --global user.email** - display email

### Configure editor to be used by git

* **git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -nosession"**
* **git config --global core.editor** - display the currently set editor

## Credentials

For sites that require credentials, if they are not configured/stored you will be prompted each time you connect to the remote repository.

* On Windows Git uses Credentials Manager to securely store your username and password.  You only need to enter enter them the first time you use that remote repository

* On Linux, a simple, but not highly secure method (since they are stored on the file system in clear text) is to do the following:

  ```bash
  git config credential.helper store

  git pull origin master  (or any other command that will prompt for your credentials
  ```
  This will prompt for your username and password, but subsequent attempts will be read from your `~/.git-credentials` file

  For better security you can store the credentials in the cache for a specified amount of time.  For example:

  ```bash
  # to change in your global settings so that it will continue to be available
  git config --global credential.helper 'cache --timeout=3600'
  # if you don't want to store it in global settings
  git config credential.helper 'cache --timeout=900'

  git pull origin master  (or any other command that will prompt for your credentials
  ````
  In this case your credentials will be stored in the cache for an hour in the first case and 15 minutes (900 seconds)

## CRLF Conversion, Warnings and Strategy

### Strategy

For the most part I try to stick to just using **lf**, including on **Windows**, particularly for **Markdown** files.  I think this is probably best handled by placing the following in the **.gitattributes** file in the appropriate **repository roots**.

### Turn of Warnings

Did this on 2018-09-07 for the **Linux Subsystem for Windows**, but it is still applied when running for **Windows** itself.

```
git config --global core.safecrlf false
```

### Consider Disabling the Conversion

From StackOverflow:

>You should use **core.autocrlf input** and **core.eol input**. Or just don't let git change the line endings at all with **autocrlf false** and get rid of highlighting of crlfs in diffs, etc with **core.whitespace cr-at-eol**.

# Issues/Errors and Solutions


## Error bad signature - fatal: index file corrupt

**Error Message**

```bash
error: bad signature
fatal: index file corrupt
```

**Solution:**

```bash
rm -f .git/index
git reset
```

**Comment**

This error occurred with an **Unreal Engine 4 Project** after a computer crash.  Running the commands above fixed it.

## Inconsistencies between how Windows and Linux Subsystem for Windows view the same repository directory

Sometimes I run into the situation where **Windows** shows files as **modified** and the **Linux Subsystem** does not.  This is on the same actual files and directories.  This is likely due to the **crlf** issue between Windows checkout and Linux checkouts, where git will try to add the **cr** on **checkout**, and remove it on **check in**.  It try to minimize this by using **lf only** on both Windows and Linux.  Many editors handle **lf** only files fine on Windows.

# Upgrading git

## Linux

### Adding Git to Ubuntu Repository

You can get a more recent version of **git** by adding the **ppa:git-core/ppa** repository to **apt**

```bash
sudo add-apt-repository ppa:git-core/ppa -y
sudo apt-get update
sudo apt-get install git -y
git --version
```

Note: after the **apt-get update** I ran **sudo apt-get upgrade** instead of **sudo apt-get install git -y**.

On the **Linux Subsystem for Windows** I had version **2.7.4**, which was the most recent version available with the default **apt** repository, even though it was **3 years old**.  After adding the above **ppa:git-core/ppa** repository and upgrading I was on the most recent **2.19.1** as of **2018-10-12**.


