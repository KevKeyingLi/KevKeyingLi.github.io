Kafka reading

## Apache Kafka Needs No Keeper: Removing the Apache ZooKeeper Dependency
https://www.confluent.io/blog/removing-zookeeper-dependency-in-kafka/

> Currently, Apache Kafka® uses Apache ZooKeeper™ to store its metadata. Data such as the location of partitions and the configuration of topics are stored outside of Kafka itself, in a separate ZooKeeper cluster. In 2019, we outlined a plan to break this dependency and bring metadata management into Kafka itself
> 
> 

### why?
the problem is with the concept of external metadata management, not with ZooKeeper itself.
* Having two systems leads to a lot of duplication
    - doubles the total complexity of the result for the operator.
    - unnecessarily steep learning curve 
    - increases the risk of some misconfiguration causing a security breach.
* Storing metadata externally is not very efficient.
    - additional Java processes
    - the data in ZooKeeper also needs to be reflected on the Kafka controller, which leads to double caching
    - Worse still, storing metadata externally limits Kafka’s scalability.
    - Finally, storing metadata externally opens up the possibility of the controller’s in-memory state becoming de-synchronized from the external state. 

More notes:
Kafka, after all, is a replicated distributed log with a pub/sub API on top. ZooKeeper is a replicated distributed log with a filesystem API on top.

### what: KIP-500
#### Handling metadata
In the post-KIP-500 world, metadata will be stored in a partition inside Kafka rather than in ZooKeeper. The controller will be the leader of this partition.

We will treat metadata as a log. Brokers read the tail, and can persist their metadata cache.

#### Controller architecture
A Kafka cluster elects a controller node to manage partition leaders and cluster metadata. 

* controller failover operation: 
    - current: Kafka elects a new controller, it needs to load the full cluster state before proceeding. As the amount of cluster metadata grows, this process takes longer and longer.
    - KIP-500: there will be several standby controllers that are ready to take over whenever the active controller goes away. These standby controllers are simply the other nodes in the Raft quorum of the metadata partition. 
* KIP-500 will speed up topic creation and deletion.
    - Currently, when a topic is created or deleted, the controller must reload the full list of all topic names in the cluster from ZooKeeper.
    - KIP-500: simply involve creating a new entry in the metadata partition, which is an O(1) operation.

Metadata scalability is a key part of scaling Kafka in the future. The authors expect that a single Kafka cluster will eventually be able to support a million partitions or more.


### Roadmap
#### Removing ZooKeeper from Kafka’s administrative tools
Soon, there will be a public Kafka API for every operation that previously required direct ZooKeeper access. We will also disable or remove the unnecessary --zookeeper flags in the next major release of Kafka.
#### Self-managed metadata quorums
Kafka controller will store its metadata in a Kafka partition rather than in ZooKeeper. However, because the controller depends on this partition, the partition itself cannot depend on the controller for things like leader election. Instead, the nodes that manage this partition must implement a self-managed Raft quorum.

[KIP-595: A Raft Protocol for the Metadata Quorum](https://cwiki.apache.org/confluence/x/Li7cC): adapt the Raft protocol to Kafka so that it really feels like a native part of the system
* changing the push-based model described in the Raft paper to a pull-based model, which is consistent with traditional Kafka replication.
* use terminology consistent with Kafka rather than the original Raft paper—”epochs” instead of “terms,” and so forth.
#### KIP-500 mode

When Kafka is run in this mode, we will use a Raft quorum to store our metadata rather than ZooKeeper.
* Much of the work to enable KIP-500 mode will be in the controller. 
* We need to define and implement more controller APIs to replace the communication mechanisms that currently involve ZooKeeper. 

#### Upgrades
Bridge releases are important because they enable zero-downtime upgrades to the post-ZooKeeper world. 

Consider a cluster that is in a partially upgraded state, with several brokers on the bridge release and several brokers on a post-KIP-500 release. The controller will always be a post-KIP-500 broker. In this cluster, brokers cannot rely on directly modifying ZooKeeper to announce changes they are making (such as a configuration change or an ACL change). The post-KIP-500 brokers would not receive such notifications because they are not listening on ZooKeeper. Only the controller is still interacting with ZooKeeper, by mirroring its changes to ZooKeeper.




#### Upgrade
