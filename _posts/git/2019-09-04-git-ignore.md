---
layout: post
title: "Git Ignore Tutorial"
tags: ["git", "ignore"]
---

# Ignoring files

- Create a file in the root directory called `.gitignore`
- then add ignore restrictions like: `*.log db/schema.rb`
- If you want a `log/` directory, but want to ignore all the files in it: `log/*`
- Then add an empty .gitignore in the empty directory: `touch log/.gitignore`
- Lines beginning with `!` are exceptions `!.gitignore`
