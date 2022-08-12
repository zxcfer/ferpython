---
layout: post
title: "Git Branching Cheat Sheet"
tags: ["git", "branch"]
---

# Git Branching Cheat Sheet

```bash
git branch          # show current brannch
git show-branch -a  # list all branches
```

* Create and switch to a branch

```bash
git branch iss53        # create new branch
git checkout iss53      # move to new branch
git checkout -b iss53   # in one step
```

* Merging branch into master

```bash
git checkout master
git pull origin master  # in the case you want to update master
git merge iss53
```