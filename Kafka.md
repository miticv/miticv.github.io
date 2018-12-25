
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
