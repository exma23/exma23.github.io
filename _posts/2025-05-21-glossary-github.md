---
layout: post
title: Github (part 1)
subtitle:
categories: fundamental CS
author: tangha1004
tags: [code tips]
---

GIT commands in one place
CREATE
Clone an existing repository: git clone
Create a new local repository: git init

LOCAL CHANGES
Changed files in your working directory: git status
Changes to tracked files: git diff
Add all current changes to the next commit: git add .
Add some changes in to the next commit: git add -p
Commit all local changes In tracked files: git commit -a
Commit previously staged changes: git commit
Change the last commit: git commit --amend

COMMIT HISTORY
Show all commits. starting with newest: git log
Show changes over time for a specific file: git log -p
Who changed what and when in : git blame

BRANCHES & TAGS
List all existing branches: git branch -av
Switch HEAD branch: git checkout
Create a new branch based on your current HEAD: git branch
Create a new tracking branch based on a remote branch: git checkout - -track
Delete a local branch: git branch -d
Mark the current commit with a tag: git tag

UPDATE and PUBLISH
List all currently configured remotes: git remote -v
Show Information about a remote: git remote show
Add new remote repository, named remote: git remote add
Download all changes from but don't integrate into HEAD: git fetch
Download changes and directly merge/integrate into HEAD: git pull
Publish local changes on a remote: git push
Delete a branch on the remote: git branch -dr
Publish your tags: git push --tags

MERGE & REUSE
Merge into your current HEAD: git merge
Rebase your current HEAD onto : git rebase
Abort a rebase: git rebase - -abort
Continue a rebase after resolving conflicts: git rebase - -continue
Use your configured merge tool to solve conflicts: git mergetool
Use your editor to manually solve conflicts and (after resolving) mark tile as resolved: git add
git rm

UNDO
Discard all local changes in your working directory: git reset -hard HEAD Discard local changes in a specific file: git checkout HEAD
Revert a commit (by producing a new commit with contrary changes): git revert
Reset your HEAD pointer to a previous commit and discard all changes since then: git reset --hard
Preserve all changes as unstaged changes: git reset
Preserve uncommitted local changes: git reset - - keep