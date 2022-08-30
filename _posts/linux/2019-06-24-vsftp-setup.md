---
layout: post
title: "Setup VSFTP"
tags: ["ftp"]
---


## Install and Setup

```bash
sudo apt-get update
sudo apt-get install vsftpd
sudo cp /etc/vsftpd.conf /etc/vsftpd.conf.orig
```

# Change in `/etc/vsftpd/vsftpd.conf`

```bash
anonymous_enable=NO
local_enable=YES
chroot_local_user=YES
```

# Add to `/etc/vsftpd/vsftpd.conf`

```bash
user_sub_token=$USER
local_root=/home/$USER
pasv_min_port=40000
pasv_max_port=50000
userlist_enable=YES
userlist_file=/etc/vsftpd.userlist
userlist_deny=NO
allow_writeable_chroot=YES
```

# Create a new user with 

```bash
sudo adduser __USER__
chmod a-w /home/__USER__
echo "__USER__" | sudo tee -a /etc/vsftpd.userlist
```

# SSL configuration 

```bash
sudo mkdir /etc/ssl/private
openssl req -x509 -nodes -days 365 -newkey rsa:1024 -keyout /etc/ssl/private/vsftpd.pem -out /etc/ssl/private/vsftpd.pem
```

# location of the RSA certificate to use for SSL encrypted connections.

```bash
rsa_cert_file=/etc/ssl/certs/ssl-cert-snakeoil.pem
```

# location of the RSA key to use for SSL encrypted connections.

```bash
rsa_private_key_file=/etc/ssl/private/ssl-cert-snakeoil.key
```

# Add or edit in `/etc/vsftpd/vsftpd.conf`

```bash
ssl_enable=YES
allow_anon_ssl=NO
force_local_data_ssl=YES
force_local_logins_ssl=YES
ssl_tlsv1=YES
ssl_sslv2=NO
ssl_sslv3=NO
```

## Opening the Firewall 

```bash
sudo ufw status
sudo ufw allow 20/tcp
sudo ufw allow 21/tcp
sudo ufw allow 990/tcp
sudo ufw allow 40000:50000/tcp
sudo ufw status
```
