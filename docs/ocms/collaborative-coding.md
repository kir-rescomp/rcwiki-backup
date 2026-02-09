---
title: Collaborative coding
description: Suggestions on how to use git and GitHub
published: true
date: 2023-05-05T11:56:41.508Z
tags: sop
editor: markdown
dateCreated: 2023-04-28T15:20:22.104Z
---

# Collaborative coding
In-house bioinformatic tools and pipelines are often collaborative projects, with multiple people contributing to the code. We use git to version control our code, and projects are deposited into the OCMS github repository. Here, I'll outline some tips on how to use git and github when it comes to collaborative coding.

# Version control with git
Git is a version control system that documents history of changes, tracking what changes were made, who made them, where they were made, and whether those changes conflict with changes made by others. Using this system, you can track your own local changes, and also manage how your changes are integrated with the project. If you are not familiar with the bisics of git, such as staging and committing changes, I recommend their [tutorial page](https://git-scm.com/docs/gittutorial). Since git is extensive in its features, people usually develop a way of working and version controlling that works for them. This page offers a starting point, outlining a suggested way of utilizing git.

## Git terminology
The [git tutorial page](https://git-scm.com/docs/gittutorial) is a great place to get started in learning about the basics of git, but I'll briefly define a few commonly used terms and features:

`repository` = a project/directory tracked by git
`branch` = another "copy" of your repository. Changes in one branch won't affect other branches unless you merge the two branches.
`commit` = tell git to add your changes to the change history
`stage` = changes that are "staged" are ready to be committed
`remote repository` = repository on github. By default remote repositories are called `origin`
`local repository` = repository in your local environment.

# OCMS Github repositories
Github is a place where we can store and share coding projects in a way that preserves your git revision history. This means that Github serves that as both a way to share/distribute code and to integrate/manage changes to the project. Git projects on Github are called repositories. OCMS has an organization page ([https://github.com/OxfordCMS](https://github.com/OxfordCMS)), where all our in-house bioinformatic tools and pipelines are stored.

# Starting a new local repository
## From scratch
Starting a repository from scratch:
```
cd /path/to/new/repo/

# initiate git 
git init
```

Start a gitignore file. This is where you can specify the files that you don't want git to track. This would be any file that you don't want to be included in the repository, files that are generated automatically, and temporary files.
```
# start a gitignore file
emacs .gitignore
```

Common entries into .gitignore are:
```
*~
.Rhistory
.RData
.Ruserdata
.Rbuildignore
*.RProj
.ipynb_checkpoints
```

## From already existing repository
More often than not, you will be contributing to an already existing repository. You can clone the repository with the link to the github page (you can copy directly from the green dropdown button "code" and choose https).

```
git clone <link to repository>
```

This creates a copy of the repository along with all of its change history.

# Useful git commands
```
git status
```

This tells you what branch you are on (more on git branches below), whether your current branch is ahead, behind, or the same in terms of commits, what files have changed since the last commit, and what files has been staged for commit. An example of what you see with `git status`:

```
$ git status
On branch main
Changes to be committed:
Your branch is up to date with 'origin/main'.
  (use "git restore --staged <file>..." to unstage)

	modified:   file1
	modified:   file2
	modified:   file3
```

Let's break down this message:
`On branch main` you are currently on a branch called `main`.
`Your branch is up to date with 'origin/main'.` Your local branch `main` is tracking the remote branch `origin/main` and the two branches have the same change history
`modified:   file1` Some changes have been made fo file1, but these changes are not yet staged.

If you want to see what changes have been made to a modified, but not yet staged file, use
```
git diff file1
```

To review the commit history:
```
git log
```

To unstage a file
```
git reset HEAD <file>
```

To stop tracking file added to .gitignore
```
git rm --cached <file>
```

To update your local repo with any changes that have occured in the remote repo
```
git fetch
```

check where pull and push is configuration
```
git remote show origin
```

If you have made changes on your current branch but you need to switch branches, you can either stage and commit all changed files. Alternatively if you're not read to commit, you can "stash" your changes and then come back to them later:
```
# stash your changes
git stash

# when you want to come back to your changes
git pop
```

list all local branches
```
git branch
```

delete local branch
```
git branch -D branch_to_be_deleted
```

check what branches are tracking
```
git branch -vv
```

# Staging and committing

Every time you make a change to a file in a directory that is being version controlled by git, git will automatically track the changes. Once you have made changes that you want to log the changes into the change history, you can stage files with:

```
git add file1 file2 file3
```

You can see what changes are about about to be committed with
```
git diff --cached
```

When you want to commit your changes:
```
git commit -m "A brief message of what changes have been made"
```

How often you make commits is a personal preference. Personally, I like keep one type of change per commit. For example, if I'm adding a new function, I'll write and test the function first, then stage all files that pertain to the new function and make a commit that says "added new function X to do XYZ". If I'm debugging an existing function, I'll commit those changes on it's own commit (i.e. "allowing function to handle X error"). Some people prefer to commit more often, and other less often. One way of thinking about it, is to consider what state of the repository you would want to roll back to, in case you even need to go into a git history and restore to a specific version. It's easy to pick a commit in your git history that you want to go back to, but at the same time, you don't want to sift through an unreasonable number of commits to find the version you are looking for.

# Working in branches
Again, there are many different ways of implenting git into your working style, so this a suggustion of one way to work.

## Remote branches
The main branch of the remote repository (the version of your repository on Github) should be the main, distributable version of the repository. This means whatever is in the remote repository should be tested and documented to the best of your ability. As a standard practice, it is not advisable to push directly to the main branch of the remote repository. Instead do the following: 

1. local changes should be pushed to a new remote branch
```
# first check for any updates in remote repo
git fetch

# push local branch to new remote branch
git push -u origin <local_branch>
```
2. create a pull request on github to merge new remote branch into main remote branch
3. the new remote branch is reviewed by other repo contributors
4. new remote branch is merged into the main branch
5. new remote branch is deleted. 

Steps 2-5 is done on the Github page.

While these step may seem cumbersome, contributing changes on branches makes it easier for others to review changes even after the merge has been made. It also makes it easier to roll back to previous versions should it be necessary.

## Local branches
It is also advantageous to work in branches locally, so you can actively work on a pipeline but still have a version of the pipeline that works and can be executed in analysis. I reserve my main local branch to be the same as the remote main branch. To update your main branch based on the remote branch:

```
# first check for any updates in remote repo
git fetch

# switch to main branch if not already on it
git checkout main

# check main branch is tracking remote main
git status

# update main branch
git pull origin main
```

If I want to make a new change to a repo, I will create a new branch that is based off of the remote main branch. Basing the new branch on remote main makes sure you are working on the most up-to-date version, and reduces the chance of merge conflicts when it comes time to merging branches into the remote main.
```
git checkout -b <new_branch> origin/main
```

When I'm done making my changes, I stage and commit my changes, push my changes to a new remote branch, have someone review my changes (though this is not always feasible), merge the new branch into the main branch, then finally update my local main branch.

Notice that there is no need to merge your local branches into main. This is to avoid having multiple "main" versions of the repo, which can create merge conflicts that can be cumbersome to resolve.

# Typical workflow for contributing to a respository
```
# first check for any updates in remote repo
git fetch

# create and switch into new branch based off of remote origin
git checkout -b new_branch origin/main

# make some changes, say, to file1

# stage changes
git add file1

# commit changes
git commit -m "brief description of changes"

# push changes to new remote branch
git push -u origin new_branch
```

* Then on Github, create pull request by clicking on the green "pull request" button. 
* If applicable, suggest someone to review your changes by ticking their name in the list of suggested reviewers. 
* When ready, merge the new branch by clicking the green "merge branch" button. Github will automatically check for any merge conflicts. If there aren't any, it will merge automatically.

```
# locally, switch into main branch
git checkout main

# important! check for updates in the remote repo
git fetch

# pull in new changes
git pull
```

# Resolving merge conflicts
Merge conflicts can be a pain to resolve, particularly because we don't work within a source code editor when working on BMRC. If you're working according to the method outlined above, where new changes are only merged in the remote repo, there is no direct way to edit the changes you're pushing on Github (though Github will show you where the conflicts are happening). What you can do is try to do the branch merging locally, where it will fail, and then you can investigate the merge conflict. To do this:

```
# check for any changes in remote
git fetch

# create and switch into a new branch based on the remote main (or what ever branch you're trying to merge into)
git checkout -b resolve_changes origin/main

# locally merge the branch
git merge branch_with_my_changes
```

The merge will tell you that there is merge conflict in the relevant files. Next open the files where the merge conlict is occuring. The file will have conflict markers `<<<<<<< HEAD`, ` =======`, `>>>>>>> BRANCH-NAME`

The code between `<<<<<<<, HEAD` and `=======` is the code in the base branch (`resolve_changes` in our example). The code between  `=======` and `>>>>>>> BRANCH-NAME` is the code in the merginb branch that is conflicting with the base branch.

For example:
```
If you have questions, please
<<<<<<< HEAD
open an issue
=======
ask your question in IRC.
>>>>>>> branch-a
```

Decide if you want to keep only your branch's changes, keep only the other branch's changes, or make a brand new change, which may incorporate changes from both branches. Delete the conflict markers <<<<<<<, =======, >>>>>>> and make the changes you want in the final merge. In this example, both changes are incorporated into the final merge:

```
If you have questions, please open an issue or ask in our IRC channel if it's more urgent.
```

Then stage the changes
```
git add <file_name>
```

Commit changes
```
git commit -m "Resolved merge conflict by incorporating both suggestions."
```

Now that the merge conflict is resolved, you can push the merged branch `resolve_changes` to a new remote branch and merge again on Github.
```
git push -u origin resolve_changes
```