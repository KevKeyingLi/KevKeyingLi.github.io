# What is Apache Kafka®? (A Confluent Lightboard by Tim Berglund) + ksqlDB
https://www.youtube.com/watch?v=06iRM1Ghr1k&ab_channel=Confluent
## data
Traditional way of thinking with databases: **objects are things**. e.g. person, train, themostat 

New way with Kafka: events -> a structure of a log: an ordered sequence of events that happened.
* Kafka manages logs by **Topic**: an ordered sequence of event that are stored in a durable way.
* **Topics** can be large, can be small, can remember data for a while, or forever.
* Each **event** represents a thing happening in the business
* Kafka encourages to think of events first, things second

## Application
Old way of applications: giant monolithic application that talks to one database.

New way: a lot of smaller applications that are easier to maintain and change

New way with kafka: small applications can read from a Kafka topic, do some processing, and maybe output to another kafka topic. 

With a cluster of kafka topics/streams, we can build new services that analyze these streams

## Four key concepts for basic kafka understanding
* events
* topics
* small services communication by consuming and producing events through topics
* realtime analytics

This is a typical architecture of a system built on kafka

## Kafka connect
Kafka connect is the tool that integrates with non-kafka data sources/systems
* stream data into Kafka-based systems as topics
* stream data out to external systems and storages

Connectors: pluggable modules. declarative way of integrating with data systems

## Kafka streams
Kafka streams: a Java API for data operations on topics: grouping, aggregating, filtering, enrichment

## KSQL by Confluent
A query language for querying topics