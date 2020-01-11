# SF Crime Statistics with Spark Streaming Project

## Introduction 

This project is aim to build an Apache Spark Structured Streaming analyzer to analyze the San Francisco crime incident.  This is a real-world dataset (extracted from Kaggle).  In order to build this project, we created Kafka server to produce data and ingest data through the Apache Spark Structure Streaming.


## Requirements

* Java 1.8.x
* Scala 2.11.x
* Spark 2.4.x
* Kafka
* Python 3.6 or above

## How to use the application

In order to run the application you will need to start:

1. Zookeeper:

`/usr/bin/zookeeper-server-start config/zookeeper.properties`

2. Kafka server:

`/usr/bin/kafka-server-start config/server.properties`

3. Insert data into topic:

`python kafka_server.py`

4. Kafka consumer:

`kafka-console-consumer --topic "topic-name" --from-beginning --bootstrap-server localhost:9092`

5. Run Spark job:

`spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.3.4 --master local[*] data_stream.py`

We have capture three different screenshots for this project (as they are saved int he Screenshots folder).

They are:

a. kafka-consumer-console-output.PNG

b. progress_report_console_output

c. count_console_output.PNG