---
layout: post
title: "Use Multiple SSL Keys with Git"
tags: ["git"]
---

# multiple keys

Edit file `~/.ssh/config `

```bash
host wordpress
          user git
          hostname bitbucket.org
          port 22
          identityfile /home/ec2-user/.ssh/id_rsa
host search3
          user git
          hostname bitbucket.org
          port 22
          identityfile /home/ec2-user/.ssh/id_rsa_search3
```

Then clone as usually, but using the host you defined in the previous file:

```bash
git clone search3:iwxfer/search3.git
````

* ref: https://superuser.com/questions/232373/how-to-tell-git-which-private-key-to-use