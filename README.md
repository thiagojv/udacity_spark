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

How did changing values on the SparkSession property parameters affect the throughput and latency of the data?

Setting `maxRatePerPartition` to 100, incresead `processedRowsPerSecond` from 36 to 175

What were the 2-3 most efficient SparkSession property key/value pairs? Through testing multiple variations on values, how can you tell these were the most optimal?