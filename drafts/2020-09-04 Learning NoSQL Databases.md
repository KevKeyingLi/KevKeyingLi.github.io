## 1 Overview
### What is NoSQL
NoSQL do not use SQL
* SQL are for relational databases
* relational databases are table-based
* records are stored in rows, and columns represent fields
* SQL query within the tables

NoSQL mroe flexible
* allows definition of fields at record creation
* nested values are common in NoSQL databases, a record could nest hashes, arrays, objects...
* fields/structures are not standardized between records

NoSQL is not new
* Apollo program used NoSQL for space shuttle part inventory
* embedded devices
* early mainframe computers

NoSQL database tradeoffs and limitations
* NoSQL databases will not solve scalability issues. 
* NoSQL provides additional flexibility over relational
* Not limited to SQL language

### NoSQL database types
All NoSQL databases are different, but they fall into a few broad categories
* document store
    - stored in a structured format(xml,json...)
    - organized into "collections" or "databases", allows grouping similar documents.
    - individual documents can have unique structures.
    - Each document usually has a specific key: for quick retrieval
    - ability to query for document by fields inside that document
* key-value store
    - a key for query, and a value associated.
    - drawback: only query by key, not other things(normally)
    - some key-value store let you define more than one key. 
    - sometimes used along side relational database for caching
* BigTable/tabular
    - named after google's BigTable implementation
    - each row have different set of columns
    - designed for large numbers of columns
    - rows are typlically versioned.
* graph databases
    - for data best represented as interconnected nodes
    - e.g. a series of road intersections, or cities.
* object databases
    - tightly integrated with Object Oriented languages.
    - act as a persistence layer: store objects directly
    - you can link objects through pointers

### Exploring NoSQL possibilities
Case study where NoSQL gives advantage
* no need to worry about schema changes, while still be able to index a field: webapp with customizable fields, e.g. an app tracking comments on articles, you can add votes later. 
* Use it as a caching layer for relational databases. And APIs use No-SQL for data.
* store binary files
    - no need to worry about file system permissions.
    - NoSQL databases will frequently extract all the metadata about a file and allow you to query by it.
    - use NoSQL to attach other data to specific files. 
* serve full web applications
    - Your HTML, stylesheets, and JavaScript can be served directly from NoSQL, then you can use the permissions in NoSQL to control who can read and write data.

No matter you use relational database or not, you can always add NoSQL database and take advantage of it. 


## Accessing NoSQL Databases(Installing CoachDB)
Written in Erlang
## Querying Schemaless data(CoachDB)
The teacher uses CoachDB UI: Futon.
### Storing data
* \_id field is auto assigned
* add arbitrary fields with values for a record
* on saving the record a \_rev field is added. which indicates the revision number

### Nesting document data
* assign a JSON object to a field, it stores as a nested object`{"something": "something"}`
* JSON array: `["aaa","bbb"]`

### Retrieving data
For CoachDB, we can retrieve data through HTTP, add `?params=...` for filtering

different url will correspond to different database(table)

### Specifying search criteria
Instead of using SQL, we can use programming language like JavaScript. 

Use `map` function in CoachDB, returns an array of objects, each use some data as a key, and some other data as value

```
function(doc) {
    if (doc.category)
        emit(doc.category, doc)
}
```


### define views
views are just predefined queries that only shows part of the database. 

Or in other words, predefined javascript logic that returns some combination of data.

With the quick http way of retrieving json, defining views are like defining routes for resources.
### Reducing data

define `reduce` function to give a summary of a dataset. Reduce is called once for each key from map function, and some **stat** is returned. 

```
function(key, values, rereduce) {
    return values.length
}
```

when more than one value is returned by `reduce` function, `reduce` is called recursively and `rereduce` is set to `true`: this helps reducing complex nested dataset. 

## CoachDB Applications
### Attaching and retrieving images
This is an example of storing binary files.

saved in `_attachments` field. can save multiple binary files.

can be retrieved through HTTP

### Querying for attachments

```
function(doc) {
    if (doc.\_attachments)
        emit(doc.name, doc_attachments)
}
```

### Deploying applications
* Store HTML, JS, CSS, images and all the resources as attachments
* create certain views for quick access to these resources
* reference each resource by their URL in the web page

### Securing CoachDB
No Auth when first start up, open by default, but easily secured.

* create an admin
* configuration -> require\_valid\_user

### Use NodeJS
Host application and connect CoachDB using NodeJS

`cradle` the package that creates database access objects.


## NoSQL Trade-Offs
### Understanding partitioning
Partitioning is one method to help manage large and busy databases.

#### What is Partitioning
Database partitioning is splitting data across multiple database servers. 

Partitioning is always done by consistent method so you always know where the data is. several different methods
* range for sorted records. e.g. A-L, M-Q, R-Z
* list/categories: records from different categories go into different partition
* hashes: function returning a value to determine membership

#### Why Partition
* storage limitations. If you have a very large dataset, that entire set might not fit on one database server.
* performance. When you split the load between partitions, it can make it faster to write to the database.
* availability. Placing your data on separate partitions insures that you're always going to be able to get to the data even if one of the partitions gets busy. 

#### Why not partition
* When your dataset is small, there's no reason to partition. It will only increase the complexity of your database server.

#### Partitioning in relaitonal vs NoSQL
Partitioning in relational databases and NoSQL databases is similar. 

Relational databases can be partitioned horizontally or vertically.
* Horizontal partitioning, which is also known as **sharding**, puts different rows on different partitions.
* Vertical partitioning on the other hand, puts different columns on different partitions. 

Partitioning non-relational databases depends on the database type.
* **Key value** and **document databases** are typically partitioned **horizontally**.
* **tabular databases** can be **horizontally and vertically** partitioned.

Many NoSQL databases are designed with partitioning in mind, however smaller databases may not need partitioning. Understanding how partitioning works is key to making informed decisions about database performance.

### Understanding the CAP theorem
Finding the ideal database for your application is largely a choice between trade-offs. The CAP theorem is one concept that can help you understand the trade-offs between different databases.

The CAP theorem was originally proposed by Eric Brewer in 2000. It was originally conceptualized around network shared data and is often used to generalize the tradeoffs between different databases. 

The CAP theorem centers around three desirable properties;
* consistency is where all users get the same data, no matter where they read the data from
* availability ensures users can always read from and write to the database
* partition tolerance ensures that the database works when divided across network.

The theorem states that at most you can only guarantee two of the three properties simultaneously.
* a **available partition-tolerant(AP)** database or
* a **consistent partition-tolerant(CP)** database or
* a **consistent available(CA)** database.

One thing to note is that not all of these properties are necessarily exclusive of each other. You can have a consistent partition-tolerant database that still has an emphasis on availability, but you're going to sacrifice either part of your consistency or your partition tolerance.


**Relational databases trend towards consistency and availability.** Partition tolerance is something that relational databases typically don't handle very well. Often you have to write custom code to handle the partitioning of relational databases. 

**NoSQL databases on the other hand trend towards partition-tolerance.** They are designed with the idea in mind that you're going to be adding more nodes to your database as it grows.

CouchDB, which we looked at earlier in the course, is an **available partition-tolerant database**. That means the data is always available to read from and write to, and that you're able to add partitions as your database grows.

In some instances, the CAP theorem may not apply to your application. Depending on the size of your application, CAP tradeoffs may be irrelevant. e.g.
> If you have a small or a low traffic website, partitions may be useless to you, and in some cases consistency tradeoffs may not be noticeable. For instance, the votes on a comment may not show up right away for all users. This is fine as long as all votes are displayed eventually.

The CAP theorem can be used as a guide for categorizing the tradeoffs between different databases.


## Other NoSQL DB
### MongoDB

MongoDB is a **document database** that uses **JavaScript**. 

#### Differences from CoachDB
1. Querying for MongoDB is not done over HTTP.
2. There are **native drivers** that are written for each language that you want Mongo. So that way you connect directly to the database rather than incurring the overhead of HTTP connections.
3. Mongo does not have permanent CouchDB-style views that you set up
4. MongoDB only has master/slave replication. You can only write to the master and then that chooses which slave to write to.
 
#### CP
* Mongo is a consistent partition-tolerant database(CouchDB is AP). All users should always get the same data back from MongoDB regardless of when they read it.
* **Documents are partitioned using sharding. Each partition will have a subset of the documents. Shards are created based on the key you choose.** This allows you to customize how Mongo partitions the database.

#### Organization and querying
* structured around: databases/collections/records.
   - A single database is intended for a single application.
   - Collections are then used to organize records that are similar to each other.
   - Each individual record can have a different structure but you still use collections to organize them.
* The JavaScript-based querying that Mongo offers is **somewhat similar to SQL**. Even though the querying is somewhat similar to SQL,
* MongoDB still has a **schema-free** structure. Individual records can have different field sets. 
* MongoDB allows you to define MapReduce functions just like CouchDB does.

#### Summary
While MongoDB is a document database with some things in common with CouchDB, it ultimately differs in the way you connect, the way it partitions data, and the way you run queries.

### Cassandra
Cassandra is an available partition-tolerant database originally developed by Facebook. 

* querying not done over HTTP
* each language has a native driver that you use to connect directly to Cassandra.
* Storage-wise Cassandra is a cross between a key/value store and a tabular database. 

#### AP
Cassandra is an available partition-tolerant database.
* You should always be able to read from and write to Cassandra.
* Hardware nodes can be added to Cassandra with no added downtime.
* The consistency of the data in Cassandra can be adjusted but it comes at the expense of the availability of the data.
 
#### Organization and querying
* each key maps to one or more columns
* columns can be grouped into column families
* its own query language(CQL), similar to SQL. The query language is specifically designed for
    - column groups
    - the adjustable consistency of Cassandra
 
#### Summary
Cassandra is very different when compared to CouchDB. It is a cross between a key/value store and a tabular database with adjustable consistency. The structure is oriented around columns in column groups. However, like CouchDB, it is an available partition-tolerant database where new hardware nodes can be added easily.



### Riak

Riak is a document database that is very similar to CouchDB.
* Connections to Riak are done over HTTP. 
* written in Erlang, a fault-tolerant language where code can be changed without stopping the system.
 

Differences between Riak and Couch. 
* You can write MapReduce functions but you can write them in Erlang as well as JavaScript in Riak
* Riak is designed primarily to work on Mac, Linux and other similar systems. You cannot run Riak easily on Windows.

#### AP
Riak is an **available partition-tolerant** database. You should always be able to read from and write to Riak, and hardware nodes could be added easily. 

#### Organization and query
* The structure of Riak is along the lines of bucket/key/value.
    - Buckets organize documents 
    - use the key of a document to retrieve it.
* The query syntax for Riak is the same as the Lucene full-text search engine. Like many other NoSQL databases, you can define MapReduce function pairs.
* you can use **key filters** with Riak. Key filters allow you to pick up records with keys matching a certain criteria. This way you can search for specific documents without having to analyze the contents of the document.
 
#### Summary
Riak is very similar to CouchDB but there are a few things that set it apart. Riak allows you to use Lucene syntax and also allows you to filter keys before searching the document contents.


### Redis
Redis and CouchDB are very different databases. While Redis and CouchDB do not use SQL for querying, the similarities end there. 

* Querying for Redis is not done over HTTP. You must use native drivers that are written for each language you want to use.
* Redis is a **key/value store**, unlike CouchDB which allows you to find a document and query against the contents of that document.
* It is designed primarily to work on Mac and Linux. It does not have Windows support
* Redis uses **master/slave replication**.

#### CP
Redis is a consistent partition-tolerant database.
* Each user should always get the same data back from Redis.
* It's possible to write directly to a slave in Redis but this violates the consistency principle of Redis. Rather than synchronizing data the way the CouchDB does, data is replicated to multiple slaves in Redis.


#### Organization and query
* Queries in Redis are done primarily by key.
* Although Redis is a key/value store, if you have your data stored as a hash in Redis, it is possible to get individual hash values.
* The values stored in Redis do not have to be strings, unlike many other key/value stores.
* Redis provides you with **lists**, **hashes** and **sets** as ways of storing data within the value.
    - Lists are **lists of strings** 
    - hashes are further key/value pairs that can be nested.
    - Sets on the other hand are a series of non-repeating values.


Redis is a key/value store that has little in common with CouchDB, the partitioning access and structures are all different. Although you can get specific values from hashes in Redis, querying is done primarily by supplying keys.