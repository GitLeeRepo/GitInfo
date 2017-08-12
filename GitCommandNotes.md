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

* **git config --global user.name="/<username/>"** - set username
* **git config --global user.name** - display username
* **git config --global user.email="/<email/>"** - set email
* **git config --global user.email** - display email


# Git initialization

* **git init** - init repo in current dir
* **git init repositoryname** - init repo in specified repository dir

# Git status

* **git status** - status of repo

# Git add

* **git add filename** - add file to staging (uncommitted)

* **git add .** - add all files to staging

* **git add --all** - add all files and files deleted to staging

# Git rm

* **git rm filename** - remove the file from your working directory and the index (Staging)
* **git rm filename --cached** - remove from the index (Staging) only.

# Git commit

* **git commit** - commit the files in staging (will bring up text editor to add message)

* **git commit -m "the message"** - commit the files adding a message

# Git branch

* **git branch** - list the branches

* **git branch branchname** - add the named branch

* **git branch -d branchname** - delete the branch (will warn if branches not merged)

* **git branch -D branchname** - will force delete even if not merged

* **git checkout branch branchname** - switch to the specified branch

# Remote Fetching (clone, fetch, merge, pull)

* **git clone** - get a remote repo cloned to local

* **git fetch origin**

* **git merge origin/branchname**

* **git pull origin**

# Config global user and email

## Set username

* **git config --global user.name="username"**

## Show username

* **git config --global user.name**

## Set email

* **git config --global user.email "email@example.com"**

## Show email

* **git config --global user.email**