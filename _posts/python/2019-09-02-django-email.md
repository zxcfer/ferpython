---
layout: post
title:  "Django Email config"
tags: ["django", "email"]
---

Configuration settings

```py
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_USE_TLS = True
EMAIL_PORT = 587
EMAIL_HOST_USER = '__ACCOUNT__@gmail.com'
EMAIL_HOST_PASSWORD = '__PASSWORD__'
```

The key is the function `send_mail`

```py
from django.core.mail import send_mail
from django.conf import settings

subject = 'Thank you for registering to our site'
message = ' it  means a world to us '
email_from = settings.EMAIL_HOST_USER
recipient_list = ['receiver@gmail.com',]
send_mail( subject, message, email_from, recipient_list )
```
