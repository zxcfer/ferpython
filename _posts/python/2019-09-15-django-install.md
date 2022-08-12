---
layout: post
title: "Installing Django"
tags: ["django", "python", "install"]
---

## mod_wsgi

```bash
sudo apt-get install libapache2-mod-wsgi
sudo a2enmod mod-wsgi #wsgi
sudo /etc/init.d/apache2 restart
```

## native installation in bitnami

```bash
/etc/ld.so.conf.d/libc.conf # add lib-dir /opt/bitnami/common/lib
sudo ldconfig				# update lib-dir in operative system
sudo ./configure --with-apxs=/opt/bitnami/apache2/bin/apxs
make
sudo make install
LoadModule wsgi_module modules/mod_wsgi.so #in httpd.conf
sudo /opt/bitnami/apache2/scripts/ctl.sh start
```

# python virtual_env

```
WSGIPythonHome /home/bitnami/dev/cardgen/cardgen_env

<VirtualHost *:80>
	...

	# django config
	<Directory /home/bitnami/dev/cardgen/src/cardgen>
		Order deny,allow
		Allow from all
	</Directory>
	WSGIScriptAlias / /home/bitnami/dev/cardgen/src/cardgen/wsgi_handler.py

	# static files config
	<Directory /home/bitnami/dev/cardgen/src/cardgen/static>
		Order deny,allow
		Allow from all
	</Directory>
	Alias /static/ /home/bitnami/dev/cardgen/src/cardgen/static/

	# process config (optional)
    WSGIDaemonProcess __project__ user=you group=you processes=1 threads=10
    WSGIProcessGroup __project__

    ...
</VirtualHost>
```

## wsgi_handler.py

```py
import os, sys, site

site.addsitedir('/home/bitnami/dev/cardgen/cardgen_env/lib/python2.6/site-packages')
os.environ['DJANGO_SETTINGS_MODULE'] = 'cardgen.settings'
sys.path.append(os.path.dirname(os.path.abspath(__file__)) + '/..')
sys.path.append(os.path.dirname(os.path.abspath(__file__)))
import django.core.handlers.wsgi
application = django.core.handlers.wsgi.WSGIHandler()
```

## mod_python

* Update `/srv/SaltyCrane/myvirtualdjango.py`

```py
activate_this = "/srv/python-environments/saltycrane/bin/activate_this.py"
execfile(activate_this, dict(__file__=activate_this))

from django.core.handlers.modpython import handler
```

* update `httpd.conf` with:

```
<Location "/">
	SetHandler python-program
	PythonHandler myvirtualdjango
	SetEnv DJANGO_SETTINGS_MODULE iwiwdsmi.settings
	PythonPath "['/srv/SaltyCrane',] + sys.path"
	PythonDebug Off
</Location>
```
