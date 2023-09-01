# Initial workflow

echo "# SimpleTestProject" >> README.md
``` git
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/zagzag2011/SimpleTestProject.git
git push -u origin main
```             
…or push an existing repository from the command line
git remote add origin https://github.com/zagzag2011/SimpleTestProject.git
git branch -M main
git push -u origin main


git --version
git status
git config --list
git config --global user.name "UserName"
git config --global user.mail "user@example.com"
git config color.ui auto
git add -A
git reset
git commit -m "Commit details"
git log
git log --stat
git branch -a

git ls-tree -r master --name-only
Checks tracked files

git branch --merged

# WorkFlow:
git checkout -b new-feature
git add .
git commit -m "New feature commit"
git push -u origin new-feature
git checkout main
git pull origin main
git merge new-feature
git push origin master 
git branch -d new-feature
git push origin --delete new-feature
=========================
# Undoing or changing things:
Reverting changed, which are not even in the staging area:
git checkout fileName
-
Returning to commit:
git reset 

Modifying last message of the commit, which had been already done:
git commit --amend -m "New text"
-
Add a file to the last commit:
git add newFile
git commit --amend newFile (save and close out)
-
If commited to the wrong branch:
git log (grab a beginning to commit's hash)
git checkout new-feature
git cherrypick 1bfdsdf (beginning to commit hash of the master branch)
git checkout master
--------
git clean -df
Deletes all untracked files and directories


