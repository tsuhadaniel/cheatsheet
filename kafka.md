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
bin/kafka-consumer-groups.sh --bootstrap-server localhost:9092 --describe [--group consumer-group-name]
```

Change
```
bin/kafka-topics.sh --bootstrap-server localhost:9092 --alter [--topic topic-name --partitions 2]
```
