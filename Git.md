# Welcome to my Git study notes #

## *** These notes are written depending on my understanding of what i learned *** ##

### Table of contents ###
- Git concepts
- Intro to Git
- Branches 
- Merging and More


### Git Concepts ###

*Git is a tool for continous integration of code that uses repositories locally and remotely in which they can be connected to each other.

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
- `git push` pushed the commit into the remote repository so both repos are in the same level (not ahead of each other)
- `git pull` pulling any changes remotely to the local repo
- `git checkout` switch between branches 

### Branches ###

