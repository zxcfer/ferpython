---
layout: post
title:  "Setup FastAPI in cPanel managed server"
tags: ["python", "fastapi"]
---

## Bridge API

At this point I am assuming you alredy have a FastAPI application ready to run. Let's say the server python file is `server.py` with the name `app`:

Run `uvicorn` in background.

   ```bash
   nohup uvicorn server:app >fastapi.out 2>fastapi.err &
   ```
 
## cPanel API setup

1. Set cPanel user in `$user` environment variable and domain in `$domain`:

```bash
export user='cpanel_user'
export domain='example.com'
```

2. Create include files [^1]

```bash
sudo mkdir -p /etc/apache2/conf.d/userdata/ssl/2_4/$user/$domain/
sudo touch /etc/apache2/conf.d/userdata/ssl/2_4/$user/$domain/include.conf
sudo mkdir -p /etc/apache2/conf.d/userdata/std/2_4/$user/$domain/
sudo touch /etc/apache2/conf.d/userdata/std/2_4/$user/$domain/include.conf
```

3. Add proxy directives[^2] in `/etc/apache2/conf.d/userdata/std/2_4/$user/$domain/include.conf`:

```bash
ProxyPass /.well-known !
Redirect permanent / https://example.com/
```

4. Add proxy SSL directives[^3] in `/etc/apache2/conf.d/userdata/ssl/2_4/$user/$domain/include.conf`:

```bash
SSLEngine on
SSLCertificateFile /var/cpanel/ssl/apache_tls/example.com/combined
SSLUseStapling off
SetEnvIf User-Agent ".*MSIE.*" nokeepalive ssl-unclean-shutdown
ProxyPass / http://127.0.0.1:8000/
ProxyPassReverse / http://127.0.0.1:8000/
Redirect permanent /example.com /example.com/
<IfModule mod_headers.c>
	Header set Access-Control-Allow-Origin '*'
</IfModule>
```

5. Rebuild Apache conf: 

```bash
sudo /usr/local/cpanel/scripts/rebuildhttpdconf
```

6. Restart Apache: 

```bash
sudo /usr/local/cpanel/scripts/restartsrv_httpd
```

## References 

[^1]: [How to use Apache Includes to add Configuration Directives to a specific domain's VirtualHost](https://support.cpanel.net/hc/en-us/articles/360052925073)
[^2]: [How can I setup a ws proxy for traccar?](https://support.cpanel.net/hc/en-us/articles/1500002918142-How-can-I-setup-a-ws-proxy-for-traccar-)
[^3]: [How do you create an Apache Reverse Proxy with mod_proxy?](https://support.cpanel.net/hc/en-us/articles/1500011220222-How-do-you-create-an-Apache-Reverse-Proxy-with-mod-proxy-)
