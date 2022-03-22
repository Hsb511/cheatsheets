# Git Cheatsheet

## Setup & config

```bash
# Clone a repository into a new directory
git clone https://github.com/Hsb511/cheatsheets.git

# Create an empty Git repository or reinitialize an existing one
git init 

# Get and set repository or global options i.e. : user infos, editor, proxy, ...
git config user.name myusername
git config user.email my@email.com
git config --global core.editor "code --wait"
git config --global http.proxy 127.0.0.1:8888
git config --list

# Add a new remote, show current remote, update remote (switch from https to ssh)
git remote add origin https://github.com/USERNAME/REPOSITORY.git
git remote -v
git remote set-url origin git@github.com:USERNAME/REPOSITORY.git
```

## Basic snapshotting

```bash
# Show all the current staged and unstaged changes on the working tree 
git status

# Show all the current unstaged changes or compare two commits 
git diff
git diff 00df25f fc3050f  

# Add all the modified files in the src/ directory to the staging index
git add src/*

# Force to delete a file (or directory) and stage it
git rm -f */myClass.kt

# Reset all the specified unstaged changes or unstaged them if --staged specified
git restore src/*
git restore --staged src/*

# Captures a snapshot of the project's currently staged changes
git commit -m "An awesome message"
git commit --amend -m "This message will overwrite the previous one"
git commit --amend --no-edit 

# Create a commit that undo all the changes of the specified commit
git revert 00df25f

# Temporarily shelves changes. Re-apply the last stash. List all the stashes. Delete the specified stash
git stash
git stash pop
git stash list
git stash drop stash@{31}

# Remove untracked files from the working tree
git clean -f 
```

## Branching and merging

```bash
# Create a new branch. List all the branches. Delete the specified branch
git branch clean/src
git branch --list
git branch -D clean/src

# Switch branches. if -b specified create and switch branches
git checkout clean/src
git checkout -b fix/src

# Show all the commit logs in the current branch
git log

# Reset the HEAD of the current branch to the specified commit keeping the changes or not if --hard specified
git reset HEAD^
git reset 00df25f --hard

# Merge the specified branch into the current one if none is specified
git merge develop
git merge --abort
git merge --continue
git merge --squash

# Reapply all the commits of master on top of topic since their divergence
git rebase master topic

# Pick the specified commit from any other branch and add it on top of your current branch. Don't forget to checkout before ! 
git cherry-pick 62ecb3
```

## Sharing and updating

````bash
git fetch

git pull

git push

git submodule

git tag

```
