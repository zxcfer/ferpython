---
layout: post
title: "Apache Flink Tutorial"
tags: ["elasticsearch", "security"]
---


docker pull ubuntu

```bash
docker run -it -rm ubuntu:latest
apt update && apt install -y vim openjdk-8-jdk wget
cat /etc/hosts
tar -xzf kafka_2.13-3.3.1.tgz
cd kafka_2.13-3.3.1
vim /kafka/config/zookeeper.yml
dataDir=/zookeper
mkdir zookeeper-data
```

Start zookeeper

```bash
bin/zookeeper-server-start.sh config/zookeeper.properties
```

2. Execute commands

```bash
docker run -it -rm ubuntu:latest
apt update && apt install -y vim openjdk-8-jdk wget
cat /etc/hosts 
vim /kafka/config/server.properties
```

change 

```
broker.id=1
log.dirs=/kafka/logs
zookeeper.connect=127.1.1.4:2181
listener=PLAINTEXT://127.17.0.5:9082
```

3. Execute commands

```bash
docker run -it -rm ubuntu:latest
apt update && apt install -y vim openjdk-8-jdk wget
cat /etc/hosts  
vim /kafka/config/server.properties
```

change 

```
broker.id=2
listener=PLAINTEXT://127.17.0.6:9092
log.dirs=/kafka/logs
zookeeper.connect=127.17.0.4:2181
```

start kafka 

```bash
kafka-server-start.sh kafka/config/server
```

4. Create a topic

start kafka in any kafka server (1 or 2)

```bash
./kafka-topics.sh --create \
--bootstrap-server 172.17.0.1:9092 \
--replication-factor 2 \
--partitions 2 \
--topic cluster-test-topic
```

we can check in any server 1 or 2

```bash
./kafka-topics.sh --list --bootstrap-server 172.17.0.1:9092
```


5. Test created topic

```bash
./kafka-console-producer.sh --broker-bootstraop
```

6. Subscribe to topic

```bash
./kafka-console-consumer.sh --bootstrap-server 172.17.0.6:9092 --topic test --from-beginning
```

