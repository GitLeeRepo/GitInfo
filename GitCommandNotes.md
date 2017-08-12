# Terminology

* Workspace - Local Checkout
* Index - Files to be committed,  Also refered to as staging.  Use the git add command to add files to the index,
* Local Reposistory - the repo on your local system where you work
* Upstream Reposistory - the remote repository (such as GitHub).  The default remote is called origin, which is created when you do a clone or use the git remote add command.  List remotes with the git remote -v command.

# Git initialization
git init - init repo in current dir

git init <repository> - init repo in specified <repository> dir

# Git status

git status - status of repo

# Git add

git add <filename> - add file to staging (uncommitted)

git add . - add all files to staging

git add --all - add all files and files deleted to staging

# Git commit

git commit - commit the files in staging (will bring up text editor to add message)

git commit -m "<message>" - commit the files adding a message

# Git branch

git branch - list the branches

git branch <name> - add the named branch

git branch -d <name> - delete the branch (will warn if branches not merged)

git branch -D <name> - will force delete even if not merged

git checkout <branch name> - switch to the specified branch

# Remote Fetching (clone, fetch, merge, pull)

git clone - get a remote repo cloned to local

git fetch origin

git merge origin/branchname

git pull origin

# Config global user and email

## Set username

git config --global user.name

## Show username

git config --global user.name

## Set email

git config --global user.email "email@example.com"

## Show email

git config --global user.email