# Welcome to my Git study notes #

## *** These notes are written based on my personal understanding of what i learned *** ##

### Table of contents ###
- Git concepts
- Intro to Git
- Branches 
- Merging and More


### Git Concepts ###

*Git is a tool for continous integration of code that uses repositories locally and remotely in which they can be connected to each other.*

In CI using Git:
- The code is continously updated by push/pull 
- We can keep history of changes through commit hashes
- Commits can be reverted and changes are tracked
- Commits are followed by message description

The basic concepts of git:
1) the remote repo consists of where the code lives
2) local repo contains the local copy only
3) history is basically the git log
4) staging is the commit changes before pushing

The uses of git are various such as:
1) Cloning a remote repo locally 
2) Initializing a repo locally and pushing it to a remote repo
3) Merging, editing branches
4) Stashing commits, ignoring files, etc..

#### Intro to git ###

First of all to connect the local computer with any remote repo there must be an ssh authentication between both.
- The remote repo will save the ssh authentication code of the local computer.

Now we can clone the repo locally.
- `git clone <repo address>` clones the remote repo to local
- `git init` initializes the current directory as a local repository
- `git log` shows local history of changes
- `git status` shows current state if there are any changes 
- `git add <file>` adds the changed file into the staging area so it can be committed
- `git commit` commits changes with an option to describe the commit in a message
- `git push` push the commit into the remote repository so both repos are in the same level (not ahead of each other)
- `git pull` pulling any changes remotely to the local repo
- `git checkout` switch between branches 

### Branches ###

It is important to maintain the state of the master branch

`git checkout -b <branchname>` switches to a new branch

When editing a branch then requesting for a merge to the master branch the request is reviewed before pulling the branch to master.
When deleting any branch the master is protected.
To avoid branch merge status in the git log we often do a pull rebase while pulling using `git pull -r` then pushing any commits
Sometimes we may have merge conflicts so we wont be able to do a `git pull -r`. We must resolve the conflicts in a code editor to review the differences then we may do a `git rebase --continue` so we can push normally after pulling a conflict version earlier.

##### git ignroe #####
The .gitignore is basically a configuration that includes files that are specific to a user and can be excluded in any push/pull by other users so these files are removed from the remote repository until removing the configuration from the .gitignore.

After including files in .gitignore we can remove the files from the remote repo using `git rm -r --cahced <filename>` 

##### git stash #####
If we have an unfinished work that we want to commit later we can save it using `git stash` and if we want to get to it back we use `git stash pop`

##### going back in history through commit log #####
We use the commit hash to navigate to any point of commit so we will be in a detached head state which allows us to create a new branch till this point of commit.
`git checkout <commit hash>`

##### undoing and changing commands #####
We can reset earlier commits and remove any edits by using `git reset --hard HEAD~3` the ~3 in the command indetifies the reverse numbering of the specific commit we want
We can also correct commit changes which is basically undoing `git commit` by using `git reset HEAD~1`
To overwritte the last commit we can use `git commit --amend`
If we tried to push normally to remote after changing earlier commits then we will get an error and alternatively we use `--force` as an option to correct commits sequence between remote and local. *Bad idea in a shared branch which causes conflicts*
`git revert <commit hash>` reverts last commit but does not override last one

#### Merging branches ####
In the command line we can merge master into another branch by `git merge master` as master is our source
Or we can do it using the UI

### Git for devops ###
* Git is important in the IaaS such as "kubernetes configuration files", "terraform and ansible conf files" and "bash/python scripts"*
* It is also important in the CI/CD pipeline and build automation such as jenkins *
Which will need the setup of integration for build automation tool and application git repo.
