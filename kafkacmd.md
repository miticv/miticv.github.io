

# Start zookeeper

(commands are store in `/usr/bin`)
`docker pull confluentinc/cp-zookeeper`   
`docker image inspect confluentinc/cp-zookeeper` (check version)
```powershell
docker run -it confluentinc/cp-zookeeper bash
# zookeeper-server-start /etc/kafka/zookeeper.properties
```

# Start kafka

(commands are store in `/usr/bin`)
`docker pull confluentinc/cp-kafka`
`docker image inspect confluentinc/cp-kafka` (check version)
```powershell
docker run -it confluentinc/cp-kafka bash
# kafka-server-start
```


# Start both with docker-compose

after run docker-compose you can run `docker run -it confluentinc/cp-kafka bash` and then execute kafka producer, consumer commands...

```
#
# docker-compose -f .\kafka-local.yml up
#

version: '3'
services:

  zookeeper-1:
    image: confluentinc/cp-zookeeper:5.1.0
    container_name: zookeeper-1
    ports:
      - "3601:22181"
    volumes:
      - data_zookeeper_1:/var/lib/zookeeper
      - data_zookeeper_1:/etc/zookeeper/secrets
    environment:
      ZOOKEEPER_SERVER_ID: 1
      ZOOKEEPER_CLIENT_PORT: 22181
      ZOOKEEPER_TICK_TIME: 2000
      ZOOKEEPER_INIT_LIMIT: 5
      ZOOKEEPER_SYNC_LIMIT: 2
      ZOOKEEPER_SERVERS: zookeeper-1:22888:23888;zookeeper-2:22888:23888;zookeeper-3:22888:23888
     
    networks:
      - kafka_network

  zookeeper-2:
    image: confluentinc/cp-zookeeper:5.1.0
    container_name: zookeeper-2
    ports:
      - "3602:22181"
    volumes:
      - data_zookeeper_2:/var/lib/zookeeper
      - data_zookeeper_2:/etc/zookeeper/secrets
    environment:
      ZOOKEEPER_SERVER_ID: 2
      ZOOKEEPER_CLIENT_PORT: 22181
      ZOOKEEPER_TICK_TIME: 2000
      ZOOKEEPER_INIT_LIMIT: 5
      ZOOKEEPER_SYNC_LIMIT: 2
      ZOOKEEPER_SERVERS: zookeeper-1:22888:23888;zookeeper-2:22888:23888;zookeeper-3:22888:23888

    networks:
      - kafka_network

  zookeeper-3:
    image: confluentinc/cp-zookeeper:5.1.0
    container_name: zookeeper-3
    ports:
      - "3603:22181"
    volumes:
      - data_zookeeper_3:/var/lib/zookeeper
      - data_zookeeper_3:/etc/zookeeper/secrets
    environment:
      ZOOKEEPER_SERVER_ID: 3
      ZOOKEEPER_CLIENT_PORT: 22181
      ZOOKEEPER_TICK_TIME: 2000
      ZOOKEEPER_INIT_LIMIT: 5
      ZOOKEEPER_SYNC_LIMIT: 2
      ZOOKEEPER_SERVERS: zookeeper-1:22888:23888;zookeeper-2:22888:23888;zookeeper-3:22888:23888
    networks:
      - kafka_network

  kafka-1:
    image: confluentinc/cp-kafka:5.1.0
    container_name: kafka-1
    depends_on:
      - zookeeper-1
      - zookeeper-2
      - zookeeper-3
    ports:
      - "4601:4601"
    volumes:
      - data_kafka_1:/var/lib/kafka/data
      - data_kafka_1:/var/lib/kafka/secrets
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper-1:22181,zookeeper-2:22181,zookeeper-3:22181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://FXWVRN2:4601
      KAFKA_LOG_DIR: /var/lib/kafka/data
      KAFKA_UNCLEAN_LEADER_ELECTION_ENABLE: "false"
#      KAFKA_ZOOKEEPER_SESSION_TIMEOUT_MS: 30000
#      KAFKA_MIN_INSYNC_REPLICAS: 2
#      KAFKA_DEFAULT_REPLICATION_FACTOR: 3
#      KAFKA_LOG_RETENTION_HOURS: 48
#      KAFKA_OFFSETS_RETENTION_MINUTES: 14400
#      KAFKA_MESSAGE_MAX_BYTES: 25000000
#      KAFKA_REPLICA_FETCH_MAX_BYTES: 25485760
    networks:
      - kafka_network

  kafka-2:
    image: confluentinc/cp-kafka:5.1.0      
    container_name: kafka-2
    depends_on:
      - zookeeper-1
      - zookeeper-2
      - zookeeper-3
    ports:
      - "4602:4602"
    volumes:
      - data_kafka_2:/var/lib/kafka/data
      - data_kafka_2:/var/lib/kafka/secrets
    environment:
      KAFKA_BROKER_ID: 2
      KAFKA_ZOOKEEPER_CONNECT: zookeeper-1:22181,zookeeper-2:22181,zookeeper-3:22181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://FXWVRN2:4602
      KAFKA_LOG_DIR: /var/lib/kafka/data
      KAFKA_UNCLEAN_LEADER_ELECTION_ENABLE: "false"
    networks:
      - kafka_network

  kafka-3:
    image: confluentinc/cp-kafka:5.1.0
    container_name: kafka-3
    depends_on:
      - zookeeper-1
      - zookeeper-2
      - zookeeper-3
    ports:
      - "4603:4603"
    volumes:
      - data_kafka_3:/var/lib/kafka/data
      - data_kafka_3:/var/lib/kafka/secrets
    environment:
      KAFKA_BROKER_ID: 3
      KAFKA_ZOOKEEPER_CONNECT: zookeeper-1:22181,zookeeper-2:22181,zookeeper-3:22181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://FXWVRN2:4603
      KAFKA_LOG_DIR: /var/lib/kafka/data
      KAFKA_UNCLEAN_LEADER_ELECTION_ENABLE: "false"
    networks:
      - kafka_network

networks:
  kafka_network:

volumes:
  data_kafka_1:
  data_kafka_2:
  data_kafka_3:
  data_zookeeper_1:
  data_zookeeper_2:
  data_zookeeper_3:

```

# Topics

```yaml
#list all topics
kafka-topics --zookeeper FXWVRN2:3601 --list

# create new topic
kafka-topics --zookeeper FXWVRN2:3601 --topic myTopic --create --partitions 3 --replication-factor 3

# show topic details
kafka-topics --zookeeper FXWVRN2:3601 --topic myTopic --describe

#delete topic
kafka-topics --zookeeper FXWVRN2:3601 --topic myTopic --delete # mark it for deletion. It will not work unless: delete.topic.delete=true
```

# Producer
```
# create producer
kafka-console-producer --broker-list FXWVRN2:4601 --topic myTopic

# warning but then create new topic (with defuault num.partitions=1 and repl=1) 
kafka-console-producer --broker-list FXWVRN2:4601 --topic notExistentTopic   

# pass producer property:
kafka-console-producer --broker-list FXWVRN2:4601 --topic myTopic --producer-property acks=all  

```

## Producer with key
```
kafka-console-producer --broker-list FXWVRN2:4601 --topic myTopic --property parse.key=true --property key.separator=,
> key,value
> another key,another value
```

# Consumer
```
# read from when it get started
kafka-console-consumer --bootstrap-server FXWVRN2:4601 --topic myTopic --group my-test-app

# read from begining
kafka-console-consumer --bootstrap-server FXWVRN2:4601 --topic myTopic --group my-test-app --from-beginning 
```
## Consumer with keys

```
kafka-console-consumer --bootstrap-server FXWVRN2:4601 --topic myTopic --from-beginning --property print.key=true --property key.separator=,
```

## Consumer with Consumer groups
will keep track of the offsets, and balance between partitions

```
kafka-console-consumer --bootstrap-server FXWVRN2:4601 --topic myTopic --group my-test-app

# It will not take into account anymore --from-beginning flag
kafka-console-consumer --bootstrap-server FXWVRN2:4601 --topic myTopic --group my-test-app --from-beginning 
```

# Consumer Group

```
#list consumer groups
kafka-consumer-groups --bootstrap-server FXWVRN2:4601 --list

#show group lag, offsets etc.
kafka-consumer-groups --bootstrap-server FXWVRN2:4601 --describe --group my-test-app 
```

# Manage Offsets
 will only work if the group is inactive (meanning no active listeners)
 
```

kafka-consumer-groups --bootstrap-server FXWVRN2:4601 --group my-test-app --topic myTopic --reset-offsets --to-earliest --execute 

# move marker 2 messages for EACH PARTITION!
kafka-consumer-groups --bootstrap-server FXWVRN2:4601 --group my-test-app --topic myTopic --reset-offsets --shift-by -2 --execute  

# move marker 2 messages for partition 0
kafka-consumer-groups --bootstrap-server FXWVRN2:4601 --group my-test-app --topic myTopic:0 --reset-offsets --shift-by -2 --execute 

# move marker to date-time
kafka-consumer-groups --bootstrap-server FXWVRN2:4601 --group my-test-app --topic myTopic --reset-offsets --to-datetime 2018-05-28T23:30:15.000 --execute
```
