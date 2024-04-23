# Snowflake tutorial

```bash
snowsql -a gw43143.switzerland-north.azure -u iwxfer -o log_level=DEBUG
```

* Create database and tables

```sql
CREATE OR REPLACE DATABASE sf_tuts;
SHOW DATABASES;

SELECT CURRENT_DATABASE(), CURRENT_SCHEMA(); -- SF_TUTS | PUBLIC

CREATE OR REPLACE TABLE emp_basic (
  first_name STRING ,
  last_name STRING ,
  email STRING ,
  streetaddress STRING ,
  city STRING ,
  start_date DATE
  );

CREATE OR REPLACE WAREHOUSE sf_tuts_wh WITH
  WAREHOUSE_SIZE='X-SMALL'
  AUTO_SUSPEND = 180
  AUTO_RESUME = TRUE
  INITIALLY_SUSPENDED=TRUE;

SELECT CURRENT_WAREHOUSE(); -- SF_TUTS_WH
```

* Uploading CSV

```sql
PUT file://D:\data\getting-started-snowflake\employees0*.csv @sf_tuts.public.%emp_basic;
PUT file://D:\data\getting-started-snowflake\employees0*.csv @<namespace>.%<table_name>;

LIST @sf_tuts.public.%emp_basic;
```

* Copy into Target

```sql
COPY INTO emp_basic
  FROM @%emp_basic
  FILE_FORMAT = (type = csv field_optionally_enclosed_by='"')
  PATTERN = '.*employees0[1-5].csv.gz'
  ON_ERROR = 'skip_file';
```
