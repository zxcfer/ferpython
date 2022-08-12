---
layout: post
title: "Migrate Master Branch to Main"
tags: ["git"]
---

# Migrate master branch to main

1. Create main branch locally, taking the history from master

    git branch -m master main

2. Push the new local main branch to the remote repo (GitHub) 

    git push -u origin main

3. Switch the current HEAD to the main branch

    git symbolic-ref refs/remotes/origin/HEAD refs/remotes/origin/main

4. Change the default branch on GitHub to main

5. Delete the master branch on the remote

    git push origin --delete master