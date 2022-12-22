curl http://some.url --output some.file

# Install Java
sudo apt update
sudo apt install openjdk-11-jdk
sudo vim /etc/environment
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
source /etc/environment


# Download Kafka
wget https://archive.apache.org/dist/kafka/3.0.0/kafka_2.13-3.0.0.tgz
tar xzf kafka_2.13-3.0.0.tgz
mv kafka_2.13-3.0.0 ~


# Starting Kafka


## In one terminal:
~/kafka_2.13-3.0.0/bin/zookeeper-server-start.sh ~/kafka_2.13-3.0.0/config/zookeeper.properties

## In other terminal:
~/kafka_2.13-3.0.0/bin/kafka-server-start.sh ~/kafka_2.13-3.0.0/config/server.properties

# Topics

## Listing topics
kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --list

## Creating topics
kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic first_topic --partitions 1 --replication-factor 1

kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic second_topic --partitions 3 --replication-factor 1

kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic third_topic --partitions 3 --replication-factor 2
> this last one will not be created because there is only one broker

kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic third_topic --partitions 3 --replication-factor 1

## Describing topics
kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic first_topic

## Deleting topics
kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic first_topic