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

`spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.4.3 --master local[*] data_stream.py`

We have captured couple screenshots for this project (as they are saved int he Screenshots folder).

They are:

a. kafka-consumer-console-output.PNG

b. progress_report_console_output

c. Spark UI

Here are some of the questions asked in the project:

1. How did changing values on the SparkSession property parameters affect the throughput and latency of the data?

`We have the ability to adjust the number of rows in our batch per second by modifying the processedRowsPerSecond option.  If we want to include more rows in each batch, then we can increase the number, which means higher throughput.`

2. What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?


`In my option, the most efficient SparkSession properties are the following:

spark.default.parallelism
spark.streaming.kafka.maxRatePerPartition

The goal on here is to maximize the processedRowsPerSecond in long run. So, I choose:

spark.default.parallelism
spark.streaming.kafka.maxRatePerPartition
spark.sql.shuffle.partitions

For the parallelism part, the rule of thumb is to set 3 per each CPU core.  If you have a 2 qua-core machine, then you would want to set the parallelsm to 24.

With the spark.streaming.kafka.maxRatePerPartition, we can set the maximum rate for each parition in order to prevent being overwhelm when there is a large amount of unprocessed messages.`
