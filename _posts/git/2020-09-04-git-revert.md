---
layout: post
title: "Git Revert"
tags: ["git"]
---


# https://ohshitgit.com/

# revert a commit
git commit -m "Something terribly"
git reset --soft HEAD~           # HEAD~ is the parent of HEAD
git add
git commit -c ORIG_HEAD

# While working on "feature" branch, suddenly need to go work on a hotfix
git commit --all --message "Backup my feature work"
git checkout -b hotfix master   # create hotfix branch from master
git checkout feature            # go back to feature
git reset head^

# save your changes without creating a commit
git stash               # save your changes
git checkout branch-B   # Then switch to your other branch
git commit --message "finished with branch-B"
git checkout branch-A   # When you're ready, go back to your original branch
git stash pop           # and unstash your changes:

# git reset
git reset --hard
git checkout HEAD -- <path>
