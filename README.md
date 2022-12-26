# Install Java
```bash
sudo apt update
sudo apt install openjdk-11-jdk
sudo vim /etc/environment
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64"
source /etc/environment
```


# Download Kafka
```bash
wget https://archive.apache.org/dist/kafka/3.0.0/kafka_2.13-3.0.0.tgz
tar xzf kafka_2.13-3.0.0.tgz
mv kafka_2.13-3.0.0 ~
```


# Starting Kafka


## In one terminal:
```bash
~/kafka_2.13-3.0.0/bin/zookeeper-server-start.sh ~/kafka_2.13-3.0.0/config/zookeeper.properties
```

## In other terminal:
```bash
~/kafka_2.13-3.0.0/bin/kafka-server-start.sh ~/kafka_2.13-3.0.0/config/server.properties
```

# Topics

## Listing topics
```bash
~/kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --list
```

## Creating topics
```bash
~/kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic first_topic --partitions 1 --replication-factor 1
```

```bash
~/kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic second_topic --partitions 3 --replication-factor 1
```

```bash
~/kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic third_topic --partitions 3 --replication-factor 2
```
> this last one will not be created because there is only one broker

```bash
~/kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --create --topic third_topic --partitions 3 --replication-factor 1
```

## Describing topics
```bash
~/kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe --topic first_topic
```

## Deleting topics
```bash
~/kafka_2.13-3.0.0/bin/kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic first_topic
```

# Consumer and producer

## Producer

### Simple producer
```bash
 ~/kafka_2.13-3.0.0/bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first_topic
```

### Producer with ack
```bash
 ~/kafka_2.13-3.0.0/bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first_topic acks=all
```
### Producer with key separator
```bash
 ~/kafka_2.13-3.0.0/bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic first_topic --property parse.key=true --property key.separator=:
```
## Consumer

### Simple consumer
```bash
 ~/kafka_2.13-3.0.0/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first_topic
```

### Consumer from begginer
```bash
 ~/kafka_2.13-3.0.0/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first_topic --from-beginning
```
### Consumer from begginer with key and value fromatter
```bash
 ~/kafka_2.13-3.0.0/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first_topic --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.timestamp=true --property print.key=true --property print.value=true
```
### Consumer with consumer group
```bash
 ~/kafka_2.13-3.0.0/bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic first_topic --group my-first-consumer-group
```

## Consumer Group
### List consumers group
```bash
  ~/kafka_2.13-3.0.0/bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --list
```
### Describing consumers group
```bash
  ~/kafka_2.13-3.0.0/bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe --group my-first-consumer-group
```

## Resetting Offsets
```bash
  ~/kafka_2.13-3.0.0/bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group my-first-consumer-group --reset-offsets --to-earliest --execute --all-topics
```


```bash
  ~/kafka_2.13-3.0.0/bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --group my-first-consumer-group --reset-offsets --shift-by -2 --execute --all-topics
```