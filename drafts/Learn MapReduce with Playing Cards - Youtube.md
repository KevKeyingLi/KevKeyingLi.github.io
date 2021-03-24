# Learn MapReduce with Playing Cards
https://www.youtube.com/watch?v=bcjSe0xCHbE&ab_channel=JesseAnderson

The key difference of map-reduce on single node vs multiple node is the shuffling magic.

On single node is simple, each type of mapped data are reduced separately

On a node cluster, each node have partitioned groups of data from mapping phase. These data are reorganized between nodes, so each node only need to care about certain groups of data, not all the data. And continues with reduce phase. 
* this also allows potential for replication, in case some nodes fails
* In MapReduce world, we call each group as data with the same key.

Hadoop's MapReduce on HDFS
* breaks large files into smaller chuncks(blocks). think 64kb, or 128kb
* various nodes can operate on different chunks of the same file at the same time. Data is processed and mapped based on keys
* **The magic**: *When finished, all the data is combined based on the key*, and reduced.
* Far more efficient than one node operating on a single file
* scales linearly to the number of nodes
