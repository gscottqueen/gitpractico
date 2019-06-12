# gitpractico

---
## Legend:

### $ git command
description

- `common use`

```
A---B  Visual A
     \
      B  Visual B
```
---

## Common Git Commands

### $ git config
Your username and email address should be the same as the one used with your git hosting provider i.e. github, bitbucket, gitlab etc

- `git config --global user.name "username"`
- `git config --global user.email "email address"`

### $ git clone
The repo is cloned into the specified directory, replace "directory" with the directory you want

- `git clone <repo-url> <directory>`

```
A---B  origin <repo-url>
     \
      B  local <directory>
```

### $ git log
Shows the commit logs all on one line

- `git log --pretty=oneline`

### $ git status
Show the working tree status in abbreviated form

- `git status --short`

### $ git branch
Add a new branch and switch to the new branch

- `git checkout -b <new name>`

```
A---B  current <branch>
     \
      B  new local <branch>
```

### $ git diff
`<sha1>` and `<sha2>` are the sha hash of the commits you want to compare

- `git diff <sha1> <sha2>`

```
A---B  <sha1>
 \   \    +   +   +
  A---B---C---D---E  <sha2>
```

### $ git pull
Incorporates changes from a remote repository into the current branch. In its default mode, git pull is shorthand for `git fetch` followed by `git merge FETCH_HEAD`

- `git pull origin <branch>`

```
      A---B---C + G feature
     /       /
D---E---F---G  origin develop
```

### $ git merge
Incorporates changes from the named commits (since the time their histories diverged from the current branch) into the current branch.

- `git merge <branch-name>`

```
      A---B---C feature
     /         \
D---E---F---G---H master
```

### $ git push
Update remote refs along with associated objects

- `git push origin <branch-name>`

```
**local**

      A---B---C feature
     /
D---E---F---G---H master

**remote origin before**

      A  feature
     /
D---E---F---G---H master

**remote origin after**

      A---B---C feature
     /
D---E---F---G---H master
```

### $ git revert/reset
`git revert` creates a new commit that undoes the changes from a previous commit. This command adds new history to the project. If you want to undo more than one commit, let's say 5 commits, run `git revert HEAD~5`. 

[Documentation on git-scm](https://git-scm.com/docs/git-revert)

`git reset` basically just changes the commit that your local copy of the repository is pointing at - otherwise known as the "branch head." In order to roll back to a certain commit, grab the SHA for the commit that you want to roll back to (let's say e349b4c72640a0b8553330b620adf684963ba4b5) and run `git reset --hard e349b4c72640a0b8553330b620adf684963ba4b5`.  This will then restore your code to that commit so you can take a look at it. From there you could `git reset --hard` to another commit, or simply run `git pull` to get back up to speed. 

There are several other options on the [git-scm documentation](https://git-scm.com/docs/git-reset). 


### $ git merge --fast-forward
[Top stack-overflow response](https://stackoverflow.com/a/29673993/9280297): "If Master has not diverged, instead of creating a new commit, git will just point master to the latest commit of the feature branch. This is a “fast forward.” There won't be any "merge commit" in fast-forwarding merge."

**Resource** : [Git Branching Basic Branching and Merging](http://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

### $ git push --force
Overwrites the particular remote branch with your local version without any additional checks or asking for permission

- `git push origin <branch> --force`

![gif](images/r_292990_JmRu7.gif "Logo Title Text 1")
<span style="color:red; font-weight:bold;">DANGER ZONE</span>
> A force push overwrites a remote branch with your local branch, regardless of the status of that remote branch. This is not ideal in a team scenario as it might result in one developer overwriting other developers’ commits (this could happen when the developer forgot to do a git pull to fetch the newer commits).

## Git Flow
Instead of a single master branch, this workflow uses two branches to record the history of the project. The master branch stores the official release history, and the develop branch serves as an integration branch for features.

### $ git flow init
`git flow init` on an existing repo will create the develop branch

Console considerations:

```
$ git flow init
Initialized empty Git repository in ~/project/.git/
No branches exist yet. Base branches must be created now.
Branch name for production releases: [master]
Branch name for "next release" development: [develop]

How to name your supporting branch prefixes?
Feature branches? [feature/]
Release branches? [release/]
Hotfix branches? [hotfix/]
Support branches? [support/]
Version tag prefix? []

$ git branch
* develop
 master
```

gitflow         | git
----------------|-----------------------------------------------
`git flow init` | `git init`
&nbsp;          | `git commit --allow-empty -m "Initial commit"`
&nbsp;          | `git checkout -b develop master`

```
            origin
            /    \
      develop  master
```

### $ git flow feature start
Create a feature branch

gitflow                            | git
-----------------------------------|--------------------------------------------
`git flow feature start MYFEATURE` | `git checkout -b feature/MYFEATURE develop`

```
            origin
            /    \
      develop  master
      /   |       |
feature
```

### $ git flow feature publish
Share a feature branch on the remote server

gitflow                              | git
-------------------------------------|------------------------------------
`git flow feature publish MYFEATURE` | `git checkout feature/MYFEATURE`
&nbsp;                               | `git push origin feature/MYFEATURE`



### $ git flow feature finish
Finalize a feature branch

gitflow                             | git
------------------------------------|--------------------------------------
`git flow feature finish MYFEATURE` | `git checkout develop`
&nbsp;                              | `git merge --no-ff feature/MYFEATURE`
&nbsp;                              | `git branch -d feature/MYFEATURE`

```
            origin
            /    \
      develop  master
      /   |       |
  feature |       |
     |    |       |
      A   |       |
       \  |       |
          A       |
```

---
## Resources
- [Git SCM](https://git-scm.com/doc)
- [Bitbucket Git Docs](https://www.atlassian.com/git/tutorials/saving-changes)
- [GitExplorer](https://gitexplorer.com/)
- [Git Flow Cheatsheet](https://danielkummer.github.io/git-flow-cheatsheet/)
- [Git Flow Breakdown](https://gist.github.com/JamesMGreene/cdd0ac49f90c987e45ac)
