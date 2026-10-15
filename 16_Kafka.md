# What is Kafka?
- Kakfka is used as message stream.
- Apache Kafka is a distributed event-streaming platform. It stores events in topics, lets producers publish them, and lets consumers read and process them. Events can remain available for replay according to the topic's retention settings.
- Kafka has high throughput but lesser storage than DB. we use kafka becuase db throughput is very low and if we large number of operation per second on db the db can go down. So that'w why we use kafka to do large number of operaion per second.
- In kafka data can stored by multiple types of consumers and data is not deleted after consumed my consumer.
- The kafka have topic  where we push out data and topic data can be partitioned in to multiple partitions for parallelism. The one partition can be consumed by only one consumer where as one consumer can consume multiple partitons.
- for example there are 4 partitons and 2 consumer gorups first group have 4 consumers and 2nd consumer group have 2 consumers.The 2st consumer group with 4 consumers eill get 1 partition each and 2nd consumer with 2 consumers will get 2 partions each.
- If there are more consumers in comsumer group than partitions than that extra consumer will sit idle.
- The kafka does auto/self balancing for consumers and partitons.

# Kafka Internals
1. Producer: Publishes messages to Kafka. As for sending email, the producer can send {“email”, “message”} to the Kafka.
2. Consumer: Subscribes to Kafka topics and processes the feed of messages.
3. Broker: Kafka server that stores and manages the topics.
4. Topic: A category/feed name to which records are published.
sendEmail can be a topic.
writeLocationToDB can be a topic.
Let’s take the analogy of a Database:
Broker = Database Server
Topics = Tables
6. Partition: Each topic is divided into partitions for parallelism. Partition is similar to sharding in DB Tables. On what basis do we do partition? For that, we have to decide and code it ourselves.
Suppose, for our sendNotification topic, we partition it based on location. North Indian’s data goes to Partition 1, and South Indian’s data goes to Partition 2.
7. Consumer Groups: When we make a consumer that subscribes to a topic, we have to assign a group to the consumer. Each consumer within a group does one type of processing from a subset of partitions.
Ex: For video processing, as we saw earlier, we can have two consumer groups. One consumer group is for video transcoding, and the other consumer group is for caption generating.


# Docker cmd to run kafka.
docker run -d \
  --name kafka \
  --network kafka-net \
  -p 9092:9092 \
  -e KAFKA_NODE_ID=1 \
  -e KAFKA_PROCESS_ROLES=broker,controller \
  -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092,CONTROLLER://0.0.0.0:9093 \
  -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://localhost:9092 \
  -e KAFKA_CONTROLLER_LISTENER_NAMES=CONTROLLER \
  -e KAFKA_LISTENER_SECURITY_PROTOCOL_MAP=CONTROLLER:PLAINTEXT,PLAINTEXT:PLAINTEXT \
  -e KAFKA_CONTROLLER_QUORUM_VOTERS=1@localhost:9093 \
  -e KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR=1 \
  -e KAFKA_TRANSACTION_STATE_LOG_MIN_ISR=1 \
  -e KAFKA_TRANSACTION_STATE_LOG_REPLICATION_FACTOR=1 \
  -e KAFKA_GROUP_INITIAL_REBALANCE_DELAY_MS=0 \
  apache/kafka:latest