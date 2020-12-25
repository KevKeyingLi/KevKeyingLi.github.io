# Table of contents
* [7 Database paradigms - Youtube](./Databases.md#7-database-paradigms---youtube)
* [ACID](./Databases.md#ACID)


# ACID

# [7 Database paradigms - Youtube](https://www.youtube.com/watch?v=W2Z7fbCLSTw&ab_channel=Fireship)

## key-value database
redis, memcache

redis, memcache lives in the memory
Pro
* fast, super fast 
Cons
* limited space
* no support for query, joins
Best for:
* caching.
* message queue, pub/sub
* leaderboards
## Wide column/BigTable/Tabular database
Examples
* cassandra, CQL
* HBASE
* BigTable

A wide-column store can be interpreted as a two-dimensional key–value store. 

No schema, so can handle unstructured data

Pro
* schemaless, good for unstructured data
* unlike sql database, it's de-centralized, can scale horizontally
Cons
* no joins allowed

Best for
* scaling a large amount of time-series data
    * data from IOT device, sensor, 
* Historical records(still time series by nature): the sequence of shows you watched on Netflix.
* High-write, low update/read

Generally not for primary app database

## Document oriented database
A more general purposed database
* MongoDB
* fire store
* DynamoDB
* CouchDB

Things are stored as documents, and each document contains key-value pair/JSON. Unstructured, don't require schema. Documents are grouped together as collections
* fields in a collection can be indexed
* collections can be organized into logical hierarchy
* This allows for modelling and retrieving relational data to a pretty significant degree

Tradeoff
Pros:
* schema-less
* relational-ish queries

Cons:
* No joins: so instead of normalizing data into small parts, you are encouraged to store data into single document. This means faster read and slower/more complex write from frontend. 

Far more general purpose than Key-value pair, or wide col database

Best for
* most apps, content management
* games
* IOT
* best place to start
Not ideal for a lot of disconnected/related data that are updated often, like GRAPHS: social media of friend network + comments. Not easily done on a document database at scale.

## Relational database
* MySQL
* SQL Server
* postgre
research: A relational model of data for large shared data banks - E.F.Codd

SQL: structured query language

* SQL database manages data in smallest normal form, requires a schema. So to work with the database, you need knowledge of the schema first.
* ACID compliant: reliable, but less flexible to scale.

> Cockroach DB: modern SQL that designed for scale. 

SQL best for most apps, not ideal for unstructure data and scaling.


## Graph
Data represented as nodes, and relations as edges. 
* neo4j
* dgraph

For example a M2M relationship:
* SQL: need an extra table referencing two sides
* Graph: an edge

Query more concise and readable, and runs faster on large datasets.

Graph database is a good substitute for SQL databases, especially if you run a lot of expensive JOINS

> airbnb

Best for:
Graphs
Knowledge graphs
Recommendation engines

## Search
Full text search engine, based on apache lucene
* elastic
* Solr
* algolia: a cloud version
* meilisearch: a rest based full text search engine

From dev point of view, operation is like document database, documents are added to indexes. But under the hood, it creates indexes for all searchable terms.

Indexing adds a lot of overhead, and could be very expensive to run at scale.

Best for
* search engines
* typeahead search feature for good UX

## Multi model database
* Fuana db
Provides a Graphql interface, and handles data modeling under the hood, it utilizes multiple kinds of models, and frontend dev doesn't need to worry about those.

## Data warehouse
Non-transactions, mainly for analytics
## Time-series database?
