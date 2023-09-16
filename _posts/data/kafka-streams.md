---
layout: post
title: "Kafka Streams Tutorial"
tags: ["kafka", "streaming"]
---


* Create a maven project

```bash
 mvn archetype:generate \
 -DgroupId=com.ferpython.com \
 -DartifactId=kafka-streams-tutorial \
 -DarchetypeArtifactId=maven-archetype-quickstart \
 -DarchetypeVersion=1.4 \
 -DinteractiveMode=false
```

* Add the dependency

```xml
<dependency>
	<groupId>org.apache.kafka</groupId>
	<artifactId>kafka-streams</artifactId>
	<version>2.6.0</version>
</dependency>
```

* Add the java file

```java
package com.lostsys.youtube.kafka;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.Properties;
import java.util.regex.Pattern;

import org.apache.kafka.common.serialization.Serdes;
import org.apache.kafka.common.utils.Bytes;
import org.apache.kafka.streams.KafkaStreams;
import org.apache.kafka.streams.StreamsBuilder;
import org.apache.kafka.streams.StreamsConfig;
import org.apache.kafka.streams.kstream.KStream;
import org.apache.kafka.streams.kstream.Materialized;
import org.apache.kafka.streams.state.KeyValueStore;

public class StreamsDemo {

	public static void main(String[] args) {

	       Properties props = new Properties();
	        props.put(StreamsConfig.APPLICATION_ID_CONFIG, "kafka-streams-tutorial");
	        props.put(StreamsConfig.BOOTSTRAP_SERVERS_CONFIG, "localhost:9092");
	        props.put(StreamsConfig.DEFAULT_KEY_SERDE_CLASS_CONFIG, Serdes.String().getClass());
	        props.put(StreamsConfig.DEFAULT_VALUE_SERDE_CLASS_CONFIG, Serdes.String().getClass());

	        final StreamsBuilder builder = new StreamsBuilder();
	        final KStream<String, String> source = builder.stream("test-stream-in");
	        
	        source.flatMapValues(value -> {
	        	ArrayList<String> r=new ArrayList<String>();
	        			
	        	r.add("{ word: '"+value+"', length: "
	        		+value.length()+", words: "+value.split(" ").length+" }");
	        			
	        	return r;
	        	})
	                .to("test-stream-out");

	        final KafkaStreams streams = new KafkaStreams(builder.build(), props);
	        streams.start();
		}	
	
	}
```

https://www.youtube.com/watch?v=Q2w5MDOLRMI&t=902s