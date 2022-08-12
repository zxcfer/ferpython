---
layout: post
title: "Rewriting Git History"
tags: ["git", "history"]
---

# Rewriting Git History

https://backlog.com/git-tutorial/rewriting-history/#git-merge-squash
https://thoughtbot.com/blog/git-interactive-rebase-squash-amend-rewriting-history

## Ammend

* Change comment

```bash
git commit --amend
```

- Change files (add/delete/edit)

```bash
git add README.md config/routes.rb
git rm notes.txt
git commit --amend
```

- change author

```bash
git commit --amend --author="Tute Costa and Dan Croak <tute+dan@thoughtbot.com>"
```

## Interactive Rebase

- change the last 4 commits

```bash
git rebase -i HEAD~4
```

# Squash commits together

- Rebase on top of master

```bash
git remote add upstream  https://github.com/thoughtbot/factory_girl.git
git fetch upstream 
git checkout feature
git rebase upstream/master
git push --force origin feature
```
