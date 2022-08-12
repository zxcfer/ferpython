---
layout: post
title: "MongoDB CLI Cheat Sheet"
tags: ["database", "mongodb", "CLI"]
---

- Installing mongodb

```bash
sudo apt-get install -y mongodb
sudo service mongodb start
```

- For remote connections add  line to `/etc/mongodb.conf`

```bash
bind_ip = 0.0.0.0
```

# backup/restore
```bash
mongodump --host __HOST__ --port __PORT__ --out dump-2013-10-25/
mongodump --username __USER__ --password "__PASS__"
mongorestore dump-2013-10-25/
```

# Insufficient free space for journal files
# /etc/mongodb.conf
# mongo 3
```bash
storage:
   mmapv1:
      smallFiles: true
# For version 2.6+
storage:
   smallFiles: true
# For version 2.4 and less
smallfiles = true
```

* Export / Import

```bash
mongoexport --host mongodb1.example.net --port 37017 --username user --password pass --collection contacts --out mdb.json
mongoexport -c collection -d database --query '{"field": 1}' > ~/dump.mongo.json		// export to JSON
mongoexport -c collection -d database -o ~/dump.mongo.json								// export to JSON
mongoimport -c collection -f collection.json
```