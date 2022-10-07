---
layout: post
title: "How to send Emails with Python"
tags: ["python", "email"]
---

```bash
setx AIRFLOW_HOME "D:\bin\airflow"
setx AIRFLOW_VERSION 2.4.1
setx PYTHON_VERSION 3.10
setx CONSTRAINT_URL "https://raw.githubusercontent.com/apache/airflow/constraints-%AIRFLOW_VERSION%/constraints-%PYTHON_VERSION%.txt"

set AIRFLOW_HOME="D:\bin\airflow"
set AIRFLOW_VERSION=2.4.1
set PYTHON_VERSION=3.10
set CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-%AIRFLOW_VERSION%/constraints-%PYTHON_VERSION%.txt"
```


```bash
pip install "apache-airflow==%AIRFLOW_VERSION%" --constraint "%CONSTRAINT_URL%"
airflow standalone
```

Visit localhost:8080 