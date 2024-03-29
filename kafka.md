## Kafka

```
cd kafka_[version]
```

Start Zookeeper
```
bin/zookeeper-server-start.sh config/zookeeper.properties
```

Start Kafka
```
bin/kafka-server-start.sh config/server.properties
```

Create a topic
```
bin/kafka-topics.sh --create --bootstrap-server localhost:9092 --topic topic-name [--replication-factor 1 --partitions 1]
```

List topics
```
bin/kafka-topics.sh --list --bootstrap-server localhost:9092
bin/kafka-topics.sh --describe --bootstrap-server localhost:9092
```

Start CLI Producer
```
bin/kafka-console-producer.sh --bootstrap-server localhost:9092 --topic topic-name [--group group-name]
```

Start CLI Consumer
```
bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic topic-name [--group consumer-group-name] [--from-beginning]
```

Info
```
bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe [--topic topic-name]
bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe [--group consumer-group-name] [--all-groups]
```

Change
```
bin/kafka-topics.sh --bootstrap-server localhost:9092 --alter [--topic topic-name --partitions 2 --replication-factor 2]
```

### Config

Kafka
```
nano config/server.properties

broker.id=0
default.replication.factor=3
listeners=PLAINTEXT://:9092
offsets.topic.replication.factor=3
transaction.state.log.replication.factor=3
num.partitions=1
log.dirs=/tmp/kafka-logs
```

Zookeeper
```
nano conifg/zookeeper.properties

dataDir=/tmp/zookeeper
```
