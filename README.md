# OMGit! <3
Git Quick Reference

## Setting up

### Set author name 
(to be show on version history)

```console
git config --global user.name "<firstname lastname>"
```
e.g.:
```console
git config --global user.name "Andréia Bohner"
```

### Set email address

```console
git config --global user.email "<email>"
```

### Set automatic CLI coloring for Git

```console
git config --global color.ui auto
```

### Configure line-ending (CRLF)

```console
git config core.autocrlf
```
show current CRLF config

```console
git config --global core.autocrlf <input|true|false>
```
set line-ending style

- ```input```: convert crlf to lf on commit but not the other way around
- ```false```: turn off crlf
- ```true```: converts lf endings into crlf

e.g.: 
```console
git config --global core.autocrlf input
```

## Workflow

### Create a new repository from current local directory (local files)

```console
git init <repository_name>
```

### Create a new repository locally from a remote repository

```console
git clone <repository_url>
```
e.g:
```console
git clone https://github.com/path/repository.git
```

### Create a new branch

```console
git checkout -b <branch_name> [base_banch]
```

create a new branch based on `[base_branch]` or on current branch if `[base_banch]` isn't informed

or:

```console
git branch <branch_name>
```

create a new branch based on current branch

### Get new changes, branches, and tags from remote repository

(just get the changes, it doesn't merge them - doesn't update tracking branches)

```console
git fetch <remote_name>
```

it's usually:

```console
git fetch origin
```

### Check changes on current branch

```console
git status
```

Show the status of your working directory: 
- new, staged, and modified files.
- current branch name
- current commit identifier
- changes pending to commit

### Add a local changed file to stage area

```console
git add <path/to/file.txt>
```

### Add all local changes to stage area

```console
git add .
```

### Commit staged local changes on current local branch

```console
git commit -m "<commit_message>"
```
e.g.:
```console
git commit -m "Initial commit"
```

### Change to another local branch

```console
git checkout <branch_name>
```

### Get a remote branch locally

```console
git fetch origin
git checkout <remote_branch_name>
```
or:
```console
git checkout -t origin/<remote_branch_name>
```

### Merge another local branch on current local branch

```console
git merge <branch_name_to_merge_on_current_branch>
```

### Merge changes from a remote branch on current local branch

(fetch from remote and merge into local)

```console
git pull origin <remote_branch_name>
```

### Push local changes to a remote branch

```console
git push origin <remote_branch_name>
```

- `-u`: add upstream (tracking) reference
```console
git push -u origin <remote_branch_name>
```

- `--tags`: push also the tags
```console
git push --tags origin <remote_branch_name>
```

- `--force`: if there are changes on remote branch that aren't in local branch (command refuses to update the remote), and you want to overwrite them:
```console
git push --force origin <remote_branch_name>
```

### List all operations made on local repository

e.g. commits, checkouts, pull, ...

```console
git reflog
```

### Have to work on another branch. What to do with the changes on current branch?

Move them to stash: a place to temporarily store the modified and staged files in order to change branches

#### Put the current working directory changes into stash, for later use
```console
git stash
```

#### List stack-order of stashed file changes

```console
git stash list
```

#### Get the stored stash content into working directory, and drop it from stash.

```console
git stash pop
```

## Checking changes

### Changes not staged

```console
git diff
```

### Changes staged but not commited

```console
git diff --staged
```

## Undo Things

### Unstage a file
(retain the changes in working directory)

```console
git reset <path/to/file.txt>
```

### Remove a file from stage area

```console
git checkout -- <path/to/file.txt>
```

### Undo local commit

```console
git reset --soft HEAD^
```

```console
git reset HEAD <path/to/file.txt>
```

### Reverting changes

```console
git reset [--hard] <target_reference>
```

Switches the current branch to the target reference, leaving
a difference as an uncommitted change.

- `--hard`: discard all changes

```console
git revert <commit_sha>
```

Create a new commit, reverting changes from the specified commit.
It generates an inversion of changes.

## Removing

### Remove local branch

```console
git branch -d <branch_name>
```
- `-D` instead of `-d` forces deletion

### Remove remote branch

```console
git push --delete <remote_name> <branch_name>
```
e.g.:
```console
git push --delete origin my_remote_branch
```

### Remove a tag from local repository

```console
git tag -d <name>
```

### Remove a tag from remote repository

```console
git push --delete origin <tag_name>
```
or:
```console
git push origin :refs/tags/tag_name
```

### Remove changes from stash

Remove the `[stash_name]` informed or the last one if none is provided.
```console
git stash drop [stash_name]
```
e.g.:
```console
git stash drop stash@{0}
```

## Tagging

Types of tags:
- `lightweight`: just the commit checksum stored in a file, i.e., a pointer to a specific commit
- `annotated`: stored as full objects in Git (checksummed; contain the tagger name, email, and date; have a tagging message; and can be signed and verified with GNU Privacy Guard - GPG).

### List all tags

```console
git tag
```

### Create a lightweight tag for current commit or for [commit sha], if informed.

```console
git tag <name> [commit_sha]
```

### Create an annoted tag for current commit if [commit sha] it's not informed 

```console
git tag -a <name> [commit_sha] [-m "tagging_message"]
```
e.g.: 
```console
git tag -a v2.1 -m "version 2.1"
```

### Show tag data with the commit that was tagged

```console
git show v2.1
```
