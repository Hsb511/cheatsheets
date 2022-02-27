# Git Cheatsheet

## Setup & config

```bash
# Clone a repository into a new directory
git clone https://github.com/Hsb511/cheatsheets.git

# Create an empty Git repository or reinitialize an existing one
git init 

# Get and set repository or global options i.e. : user infos, editor, ...
git config user.name myusername
git config user.email my@email.com
git config --global core.editor "code --wait"
```

## Basic snapshotting

```bash
git status

git diff

# Add all the modified files in the src/ directory to the index
git add src/*

git restore

git commit -m ""

```

## Branching and merging

```bash

git branch

git checkout

git merge

git log

git reset

git stash

```

## Sharing and updating

````bash
git fetch

git pull

git push

git submodule

```
