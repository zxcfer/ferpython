---
layout: post
title: "Linux User Management"
tags: ["linux", "user"]
---

- list users

```bash
sudo cat /etc/shadow
sudo users                  # connected ones
cat /etc/passwd | grep ftp  # FTP users
```

- create users

```bash
sudo useradd -s /bin/bash -d /home/__USER__ -m __USER__
sudo passwd __USER__
```

- Add to sudoers with `sudo visudo` then update user:

```bash
__USER__ ALL=(ALL:ALL) ALL
<HOSTs>=(<T>:<COMMAND>)
```

- or just:

```bash
sudo adduser __USER__ sudo
```

- group management

```bash
groupadd -r __GROUP__           # create new group

gpasswd -a __USER__ __GROUP__   # add user to group
gpasswd -d __USER__ __GROUP__   # delete user to group
gpasswd -M u1,u2,.. __GROUP__   # set memebers of a groups

usermod -a -G __GROUP__ __USER__
```

- activar y desactivar root en ubuntu

```bash
sudo passwd root
sudo passwd -l root
```

- set default shell to user

```bash
chsh -s /bin/bash username
```

- SSH login without password

```bash
ssh-keygen -t rsa                            # generate key in your PC
scp ~/.ssh/id_rsa.pub ~/.ssh/authorized_keys # copy public key to authorized_keys in the server
```

- disable password authentication for specific user

```bash
sudo vim /etc/ssh/sshd_config
Match user __USER__
PasswordAuthentication no
```
