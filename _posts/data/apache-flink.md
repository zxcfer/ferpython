---
layout: post
title: "Apache Flink Tutorial"
tags: ["kafka", "streaming"]
---

```bash
mvn archetype:generate \
 -DgroupId=com.mycompany.app \
 -DartifactId=my-app \
 -DarchetypeArtifactId=maven-archetype-quickstart \
 -DarchetypeVersion=1.4 \
 -DinteractiveMode=false

mvn archetype:generate \
-DarchetypeGroupId=org.apache.flink \
-DarchetypeArtifactId=flink-walkthrough-datastream-java \
-DarchetypeVersion=1.13.0 \
-DgroupId=frauddetection \
-DartifactId=frauddetection \
-Dversion=0.1 \
-Dpackage=spendreport \
-DinteractiveMode=false
```