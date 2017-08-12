#create an alias named origin
git remote add origin https://github.com/Traeken/PythonSandbox.git
git push -u origin master

#above push the same as:
git push -u https://github.com/Traeken/PythonSandbox.git master


#get a list of aliases
git remote -v

#rname an alias
git remote rename origin mynewalias


