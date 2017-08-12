# create an alias named origin
git remote add origin https://github.com/Traeken/PythonSandbox.git
git push -u origin master

# above push the same as:
git push -u https://github.com/Traeken/PythonSandbox.git master


# get a list of aliases
git remote -v

# rename an alias
git remote rename origin mynewalias

# fetching
git fetch origin 
Note the above updates info on any changes on the remote, without this git status will show them in sync even when not
but it doesn't pull the actual changes over, needs to be followed by a merge or pull to to that

# merging
git merge origin/branchname

# pulling does both a fetch and merge
git pull origin branchname



