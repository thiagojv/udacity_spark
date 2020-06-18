# udacity_spark
Udacity - SF Crime Data Project Files

### Dependencies
- JDK 1.8
- Scala 2.11.12
- Kafka 2.3.0
- Spark - 2.4.3 with Hadoop 2.7

### Requirements
findspark
pyspark
python-dateutil
pathlib
kafka

### Starting Kafka
/opt/kafka_2.11-2.3.0/bin/zookeeper-server-start.sh /vagrant/udacity_spark/config/zookeeper.properties
/opt/kafka_2.11-2.3.0/bin/kafka-server-start.sh /vagrant/udacity_spark/config/server.properties

### Starting Producer
cd /vagrant/udacity_spark
python kafka_server.py

### Starting Consumer
cd /opt/kafka_2.11-2.3.0
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic com.udacity.sfpd.calls --from-beginning

### Spark Submit
spark-submit --packages org.apache.spark:spark-sql-kafka-0-10_2.11:2.4.5 --master local[*]  /vagrant/udacity_spark/data_stream.py

### Questions

1 - How did changing values on the SparkSession property parameters affect the throughput and latency of the data?

| id | spark.default.parallelism | spark.sql.shuffle.partitions | processedRowsPerSecond | inputRowsPerSecond |
| -: | ------------------------: | ---------------------------: | ---------------------: | -----------------: |
|  1 |                         2 |                            1 |                     13 |                  1 |
|  2 |                        10 |                            1 |                    248 |                 23 |
|  3 |                        10 |                           10 |                    121 |                 25 |
|  4 |                        10 |                           20 |                     82 |                 23 |
|  5 |                        20 |                           10 |                    125 |                 22 |

Increasing parallelism to 10 gets a higher throughput with 248 rows/sec.
Increasing partitions to 10 get the lowest latency with 25 rows processed per second.
Increasing more parallelism or partitions, like to 20, decreased both throughput and latency.


2 - What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?

In this case, the most optimal results I get was in test 2 where I get the higher throughput and the second higher latency.
spark.default.parallelism = 10
spark.sql.shuffle.partitions = 1