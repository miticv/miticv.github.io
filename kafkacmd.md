

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

[kafka-local.yml](https://github.com/miticv/miticv.github.io/blob/master/kafka-local.yml)

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


# Add schema to registry

Run cp-schema-registry container:
```
docker run -it confluentinc/cp-schema-registry:5.1.0 bash
```
Add schema:
```
kafka-avro-console-producer --broker-list FXWVRN2:4601 --topic OmegaExternalEntryPointReceived --property schema.registry.url=http://FXWVRN2:5601 --property value.schema='{"name":"OmegaExternalEntryPointReceived","type":"record","namespace":"Omega","doc":"This is a Avro schema for incoming requests from AMP","fields":[{"name":"Request","type":"string"},{"name":"CorrelationID","type":"string"},{"name":"RequestTimeStamp","type":"string"}]}'
```
