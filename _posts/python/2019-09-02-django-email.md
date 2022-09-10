---
layout: post
title:  "Django Email configuration"
tags: ["django", "email"]
---

Sending emails is pretty easy with Django, with two steps you are just done: config the email access parameters and call the `send_mail` function.

- SMTP configuration:

```py
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = 'smtp.gmail.com'
EMAIL_USE_TLS = True
EMAIL_PORT = 587
EMAIL_HOST_USER = '__ACCOUNT__@gmail.com'
EMAIL_HOST_PASSWORD = '__PASSWORD__'
```

- The key is the function `send_mail`, look this example:

```py
from django.core.mail import send_mail
from django.conf import settings

subject = 'Thank you for registering to our site'
message = ' it  means a world to us '
email_from = settings.EMAIL_HOST_USER
recipient_list = ['receiver@gmail.com',]
send_mail( subject, message, email_from, recipient_list )
```
