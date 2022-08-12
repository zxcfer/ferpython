---
layout: post
title: "SSH Cheat Sheet"
tags: ["ssh"]
---

- Install ssh server

```bash
sudo apt-get install openssh-server
sudo vi /etc/ssh/sshd_config
sudo /etc/init.d/ssh restart
```

- Run command on ssh (Secure SHell)

```bash
ssh $__USER__@$__HOST__ command
```

#check network

```bash
netstat -tulpn
```

- Not close SSH

```bash
sudo vim /etc/ssh/sshd_config

TCPKeepAlive no
ClientAliveInterval 30
ClientAliveCountMax 100
```

- SCP with permissions

```bash
scp -p -r $__USER__@$__HOST__:$__SRC__ $__TARGET__
```

- Use key file

```bash
scp -i ~/.ssh/superkey -p 87 $__USER__@$__HOST__:$__SRC__ $__TARGET__
```

- Forward connections to $HOSTNAME:8080 out to $HOST:80

```bash
ssh -g -L 8080:$hostname:80 root@$__HOST__

ssh -L 3333:localhost:3306 __USER__@__REMOTE__
mysql -u __MYUSER__ -p -P 3333 -h 127.0.0.1 
```

- Generate RSA key

```bash
ssh-keygen -t rsa
cat .ssh/id_rsa.pub | ssh __USER__@__REMOTE__ 'cat >> .ssh/authorized_keys'
chmod 700 ~/.ssh
chmod 600 ~/.ssh/authorized_keys
```

## Problem: SSH is slow! ##
- 1. Add this to `/etc/ssh/sshd_config`

```bash
UseDNS no
```

- 2. Already slow? add to `/etc/ssh/ssh_config or ~/.ssh/config`

```bash
GSSAPIAuthentication no
```
