---
layout: post
title: "Migrate Master Branch to Main"
tags: ["git"]
---

In order to replace your `master` branch and start using `main` instead. I found this steps be the simplest way to do it:

1. Create the `main` branch locally, taking the history from master

	```bash
	git branch -m master main
	```

2. Push the new local main branch to the remote repo
```bash
git push -u origin main
```
3. Switch the current HEAD to the main branch

```bash
git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main
```

4. Change the default branch on Github/Gitlab to main

5. Delete the master branch on the remote

```bash
git push origin --delete master
```

> Why should I change master to main? [Wikipedia Article](https://en.wikipedia.org/wiki/Master/slave_(technology))