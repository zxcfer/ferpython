---
layout: post
title: "MySQL Scripts"
description: "Database full dump and table sizes summary."
tags: ["database", "sql", "mysql"]
---

## All databases dump

```bash
HOST=localhost
USER=__USER__
PASS=__PASS__
BACKUP_DIR=__OUTDIR__

if [ ! -d $BACKUP_DIR ]; then
  mkdir -p $BACKUP_DIR
fi

MYSQL_DBS=$(mysqlshow -h $HOST -u $USER -p$PASS | awk ' (NR > 2) && (/[a-zA-Z0-9]+[ ]+[|]/) && ( $0 !~ /mysql/) { print $2 }');

for DB in $MYSQL_DBS ; do
  echo "* Backuping MySQL data from $DB@$HOST..."
  mysqldump -h $HOST -u $USER -p$PASS $DB > $BACKUP_DIR/mysql_$DB.sql
done
```

## Tables size in MB

```sql
SELECT table_schema "table",
   Round(Sum(data_length + index_length) / 1024 / 1024, 1) "DB Size in MB"
FROM   information_schema.tables
GROUP  BY table_schema;
```