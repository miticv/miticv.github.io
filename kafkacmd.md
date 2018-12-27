

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

```

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
kafka-console-producer --broker-list FXWVRN2:4201 --topic myTopic

# warning but then create new topic (with defuault num.partitions=1 and repl=1) 
kafka-console-producer --broker-list FXWVRN2:4201 --topic notExistentTopic   

# pass producer property:
kafka-console-producer --broker-list FXWVRN2:4201 --topic myTopic --producer-property acks=all  

```

## Producer with key
```
kafka-console-producer --broker-list FXWVRN2:4201 --topic myTopic --property parse.key=true --property key.separator=,
> key,value
> another key,another value
```

# Consumer
```
# read from when it get started
kafka-console-consumer --bootstrap-server FXWVRN2:4201 --topic myTopic --group my-test-app

# read from begining
kafka-console-consumer --bootstrap-server FXWVRN2:4201 --topic myTopic --group my-test-app --from-beginning 
```
## Consumer with keys

```
kafka-console-consumer --bootstrap-server FXWVRN2:4201 --topic myTopic --from-beginning --property print.key=true --property key.separator=,
```

## Consumer with Consumer groups
will keep track of the offsets, and balance between partitions

```
kafka-console-consumer --bootstrap-server FXWVRN2:4201 --topic myTopic --group my-test-app --group=my-test-app 

# It will not take into account anymore --from-beginning flag
kafka-console-consumer --bootstrap-server FXWVRN2:4201 --topic myTopic --group my-test-app --group=my-test-app --from-beginning 
```

# Consumer Group

```
#list consumer groups
kafka-consumer-groups --bootstrap-server FXWVRN2:4201 --list

#show group lag, offsets etc.
kafka-consumer-groups --bootstrap-server FXWVRN2:4201 --describe --group my-test-app 
```

# Manage Offsets
 will only work if the group is inactive (meanning no active listeners)
 
```

kafka-consumer-groups --bootstrap-server FXWVRN2:4201 --group my-test-app --topic myTopic --reset-offsets --to-earliest --execute 

# move marker 2 messages for EACH PARTITION!
kafka-consumer-groups --bootstrap-server FXWVRN2:4201 --group my-test-app --topic myTopic --reset-offsets --shift-by -2 --execute  

# move marker 2 messages for partition 0
kafka-consumer-groups --bootstrap-server FXWVRN2:4201 --group my-test-app --topic myTopic:0 --reset-offsets --shift-by -2 --execute 

# move marker to date-time
kafka-consumer-groups --bootstrap-server FXWVRN2:4201 --group my-test-app --topic myTopic --reset-offsets --to-datetime 2018-05-28T23:30:15.000 --execute
```
