---
layout: post
title: "Oracle Cheat Sheet"
tags: ["database", "Oracle", "SQL"]
---

# Oracle data types

* Detailed https://www.w3resource.com/oracle/oracle-data-types.php
* Compare with SQL Server https://sqlserverrider.wordpress.com/2014/01/26/data-type-mapping-between-sql-server-and-oracle/

```sql
VARCHAR2(size)	-- From 1 byte to 4KB.
NVARCHAR2(size)	-- From 1 byte to 4KB. (National)
CHAR(size)		-- 2000 bytes. Default and minimum size is 1 byte.
NCHAR(size)		-- 2000 bytes. Default and minimum size is 1 byte.
NUMBER(p,s)		-- The precision p can range from 1 to 38. The scale s can range from -84 to 127.
BINARY_FLOAT	-- A 32-bit, single-precision floating-point number data type.			Each BINARY_FLOAT value requires 4 bytes.
BINARY_DOUBLE	-- A 64-bit, double-precision floating-point number data type.			Each BINARY_DOUBLE value requires 8 bytes.
LONG			-- Character data of variable length (A bigger version the VARCHAR2 datatype)			2 Gigabytes
RAW(size)		-- Raw binary data of length size bytes.			Maximum size is 2000bytes
LONG RAW		-- Raw binary data of variable length.			2 Gigabytes.
ROWID			-- Hexadecimal string representing the unique address of a row in its table.			10 bytes
UROWID			-- Hex string representing the logical address of a row of an index-organized table			The maximum size and default is 4000 bytes
```

## Datetime

```sql
DATE		-- from January 1, 4712 BC to December 31, 9999AD.
TIMESTAMP (fractional_seconds_precision)	-- the number of digits in the fractional part of the SECOND datetime field.			Accepted values of fractional_seconds_precisionare 0 to 9. (default = 6)
TIMESTAMP (fractional_seconds_precision) WITH {LOCAL} TIMEZONE		-- As above with time zone displacement value			Accepted values are 0 to 9. The default is 6.
INTERVAL YEAR (year_precision) TO MONTH		-- Time in years and months, where year_precision is the number of digits in the YEAR datetime field.			Accepted values are 0 to 9. The default is 2. The size is fixed at 5 bytes.
INTERVAL DAY (day_precision) TO SECOND (fractional_seconds_precision)	-- Time in days, hours, minutes, and seconds.			day_precision can be 0 to 9. (default = 2)
--	day_precision is the maximum number of digits in ‘DAY’			fractional_seconds_precisioncan be 0 to 9. (default = 6)
--	fractional_seconds_precision is the max number of fractional digits in the SECOND field.			
```

## Binary

```sql
CLOB	-- Character Large Object - 4 Gigabytes
NCLOB	-- National Character Large Object - 4 Gigabytes
BLOB	-- Binary Large Object - 4 Gigabytes
BFILE	-- Pointer to binary file on disk - 4 Gigabytes
```

## Other articles

* https://en.wikibooks.org/wiki/Oracle_Database/SQL_Cheatsheet
* Create a table with pk. https://chartio.com/resources/tutorials/how-to-define-an-auto-increment-primary-key-in-oracle/#adding-a-trigger

