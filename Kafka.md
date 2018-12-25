
# Topics, partitions and offsets
Is a particular steram of data. You can have as many topics as you want. Topic is indentified by its name

* Topis are split in partitions
* Each partition is ordered
* Each message within a partition gets an incremental id called offest
* Offset only have a meaning for a specific partition   
(offset 3 in partition 0, doesnt represent the same data as offset 3 in partition 1)
* Order is GUARANTEED within a partition (not across partitions)
* Data is kept only for a limited time (default is one week 168 hours)
* Data is immutable (cannot be changed)
* Data is assigned randomly unless a key is provided

![Topics](https://github.com/miticv/miticv.github.io/blob/master/Images/Topics.png)


# Broker

* A kafka clusted is composed of multiple brokers (servers)
* Each broker is identified by its ID (integer)
* Each broker contains certain topic partitions
* After connecting to any broker, you will be connected to whole cluster   
(it is called bootstrap broker, and it can be any)
* Good number to start is 3 brookers (can grow to 100s)

![Brokers](https://github.com/miticv/miticv.github.io/blob/master/Images/Brokers.png)

## Brokers and Topics

Example Topic-A with 3 partitions   
Example Topic-B with 2 partitions   

![BrokersAndTopics](https://github.com/miticv/miticv.github.io/blob/master/Images/BrokersAndTopics.png)

## Topic replication factor

* Topics should have replication factor >1 (usualy 3). This way if a broker is down, another broker can serve the data
Example Topic-A with 2 partitions and replication factor of 2

![BrokersReplications](https://github.com/miticv/miticv.github.io/blob/master/Images/BrokersReplications.png)


## Leader for Partition

* At any time ONE broker can be a LEADER  for a given PARTITION   
(Marked as star in the image)
* Only leader can receive data and serve data for a partition!
* Other brokers will synchronize the data
* Each partition has 1 leader and multiple ISR (in-sync replicas)


# Producers

Producers write data to topics (made out of partitions) and automatically know to which broker and partition to write to. In case of broker failures, producers will automatically recover

**Producers can choose to receive acknowledgment of data writes:**    
* acks=0 : Producer does not wait for acknowledgment (possible data loss)   
* acks=1: Producer will wait for leader acknowledgement (limited data loss)   
* acks=all: Leader + prelicas acknowledgement (no data loss)   

**Producer can choose to send a key with the message (string, number, etc)**   
* key = null: data is sent round robin
* key != null: all messages for that key will always go to the same partition (usefull when you need message ordering)
(We get this guarantee thanks to hashing, and it **depends on number of partitions**)



# Consumers

Consumers read data from a topic (indentified by name). Consumers know which broker to read from. In case of broker failures, consumers know how to recover. Data is red in order within each partition.


## Consumer Groups










