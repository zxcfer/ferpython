---
layout: post
title: "PostgreSQL CLI Cheat Sheet"
tags: ["database", "postgres", "sql", "cli"]
---

# PostgreSQL CLI Cheat Sheet

* Install PostgreSQL

```bash
sudo apt-get install postgresql postgresql-client postgresql-contrib
sudo aptitude install postgresql-8.4 postgresql-client-8.4
sudo apt-get install pgadmin3

sudo /etc/init.d/postgresql-8.4 start
sudo /etc/init.d/postgresql restart
sudo /etc/init.d/postgresql reload
```

* Set 'postgres' password and create first database and user

```bash
sudo passwd postgres
su postgres
```

* Finally for connect to the database:

```bash
psql __DATABASE__ -U __USER__ -h 127.0.0.1  -W
```

* Remote access configuration

```bash
sudo vi /etc/postgresql/8.4/main/postgresql.conf
    listen_addresses = 'localhost' ==> listen_addresses = '*' o listen_addresses = '0.0.0.0'
    password_encryption = on ==> password_encryption = on
```

* Config access list in `/etc/postgresql/8.4/main/pg_hba.conf`

```
host  MyDataBase  MyUser  MyIP            255.255.255.0  md5
host  MyDataBase  MyUser  192.168.1.4     255.255.255.0  md5
host  MyDataBase  MyUser  192.168.1.4/24                 md5
host  all         all     0.0.0.0         0.0.0.0        md5
```

* Create user by specialized commands

```bash
createuser -A -d -P -h host -U new_user
dropuser -h __HOST__ -U __USER__

for tbl in `psql -qAt -c "select tablename from pg_tables where schemaname = 'public';" YOUR_DB` ; do  psql -c "alter table \"$tbl\" owner to NEW_OWNER" YOUR_DB ; done
for tbl in `psql -qAt -c "select sequence_name from information_schema.sequences where sequence_schema = 'public';" YOUR_DB` ; do  psql -c "alter table \"$tbl\" owner to NEW_OWNER" YOUR_DB ; done
for tbl in `psql -qAt -c "select table_name from information_schema.views where table_schema = 'public';" YOUR_DB` ; do  psql -c "alter table \"$tbl\" owner to NEW_OWNER" YOUR_DB ; done
```

* Backup full database (compress: -Fc)

```bash
pg_dump -f backup.sql -U $__USER__ -h $__HOST__ -W $__DATABASE__ -p $__PORT__
```

* Retore from compressed dump (-Fc)

```bash
pg_restore -U postgres -W -h 127.0.0.1 -d database database.bkp
```

* Restore from sql

```bash
psql -d database -f backup.sql
```

* Backup database schema

```bash
pg_dump -sv prueba -O > backup.schema.sql
```

* Backup database data

```bash
pg_dump -Fc -f backup.data.dump -a --disable-triggers database
for tbl in `psql -qAt -c "select tablename from pg_tables where schemaname = 'public';" __DATABASE__` ; do  pg_dump --file=$tbl.sql --column-inserts --data-only --table=$tbl __DATABASE__ ; done
```

* LOG: could not translate host name "localhost", service "5432" to address: Name or service not known. Solution, in file `/etc/hosts` add:

```bash
127.0.0.1 localhost localhost.localdomain
```

* Create database and grant access

```bash
sudo -u postgres psql -c "CREATE DATABASE __DATABASE__ WITH OWNER __USER__ ENCODING 'utf-8';"
```

* Add owner to a database

```bash
sudo -u postgres psql -c "ALTER DATABASE __DATABASE__ OWNER TO __USER__;"
```