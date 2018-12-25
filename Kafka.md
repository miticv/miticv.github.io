
# Topic
Is a particular steram of data.
You can have as many topics as you want
Topic is indentified by its name

Topis are split in partitions
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
* At any time ONE broker can be a LEADER  for a given PARTITION   
(Marked as star in the image)
* Only leader can receive data and serve data for a partition!
* Other brokers will synchronize the data
* Each partition has 1 leader and multiple ISR (in-sync replicas)

Example Topic-A with 2 partitions and replication factor of 2

![Brokers](https://github.com/miticv/miticv.github.io/blob/master/Images/Brokers.png)
