# gitpractico

---
Legend:
## git command

`common use`

description

---

## git config

`git config --global user.name "username"`

`git config --global user.email "email address"`

Your username and email address should be the same as the one used with your git hosting provider i.e. github, bitbucket, gitlab etc

## git clone

`git clone <repo-url> <directory>`

```
A---B  origin <repo-url>
     \
      B  local <directory>
```

The repo is cloned into the specified directory, replace "directory" with the directory you want

## git log
`got log`

Shows the commit log with the most recent commit first. Displays commit ID, author, date, commit message.

`git log --pretty=oneline`

Same as above, but shows each commit on one line, displaying only the commit ID and commit message. 

## git status

`git status --short`

Show the working tree status in abbreviated form

## git branch

`git checkout -b <new name>`

```
A---B  current <branch>
     \
      B  new local <branch>
```

Add a new branch and switch to the new branch

## git diff

`git diff <sha1> <sha2>`

```
A---B  <sha1>
 \   \    +   +   +
  A---B---C---D---E  <sha2>
```

sha1 and sha2 are the sha hash of the commits you want to compare

## git pull

`git pull origin <branch>`

```
      A---B---C feature
     /       /
D---E---F---G---H origin develop
```

Incorporates changes from a remote repository into the current branch. In its default mode, git pull is shorthand for `git fetch` followed by `git merge FETCH_HEAD`

## git merge

`git merge <branch-name>`

```
      A---B---C feature
     /         \
D---E---F---G---H master
```

Incorporates changes from the named commits (since the time their histories diverged from the current branch) into the current branch.

## git push


## git revert/reset


## git flow


## git flow init


## git flow feature start


## git flow feature publish


## git push origin <feature>


## git flow feature finish
