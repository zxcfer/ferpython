---
layout: post
title: "How to send Emails with Python"
tags: ["python", "email"]
---

- Sending a single email without format

```python
import smtplib

sender = 'from@fromdomain.com'
receivers = ['to@todomain.com']

message = """From: From Person <from@fromdomain.com>
To: To Person <to@todomain.com>
Subject: SMTP e-mail test

This is a test e-mail message.
"""

try:
   smtp = smtplib.SMTP('localhost')
   # context = ssl.create_default_context()
   # smtp = smtplib.SMTP_SSL("smtp.gmail.com", 587, context=context)
   # smtp.login("hello@gmail.com", "password")
   smtp.sendmail(sender, receivers, message)         
   print "Successfully sent email"
except SMTPException:
   print "Error: unable to send email"
```

- For sending HTML content, just change the message to:

```python
message = """From: From Person <from@fromdomain.com>
To: To Person <to@todomain.com>
MIME-Version: 1.0
Content-type: text/html
Subject: SMTP HTML e-mail test

This is an e-mail message to be sent in HTML format

<b>This is HTML message.</b>
<h1>This is headline.</h1>
"""
```

* [source](https://realpython.com/python-send-email/)
