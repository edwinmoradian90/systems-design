# Databases

## SQL

SQL is used to communicate with relational databases. Relational databases store data in a very organized, but also rigid way.

## NoSQL

NoSQL, earning it’s name by being “not only SQL” makes it easier to store all different types of data together. It’s used for its flexibility and therefore speed and scalability in managing large volumes of data.

<br/>

---

<br/>

## Types of NoSQL databases

1. **Key-value**: Data is stored as attribute names or keys with values
2. **Document**: Contains many different key value pairs
3. **Graph**: Used to store data related to connections or networks
4. **Column**: Data is stored as columns instead of rows

Each type of NoSQL database stores data differently and is selected and used in different contexts. For example, graph databases are commonly used in social media.

[A good reference here](https://www.blazeclan.com/blog/dive-deep-types-nosql-databases/)

<br/>

---

<br/>

## CAP

CAP stands for consistency, availability, partition tolerance.

- Consistency -- are all of my nodes always insync and accurate?
- Availablity -- are all non-failing nodes available for querying?
- Partition-tolerance -- will the cluster continue to work despite any number of communication breakdowns between nodes in the system?

The CAP theorem states that in case of a network failure, when a few of the system nodes are down, we have to choose between availability and consistency.

If you choose availability, then your other nodes will pick up the slack when the primary is down, sacrificing consistency.

if you choose consistency, all other nodes must be locked down until the failing node is back online.

if you choose

<br/>

---

<br/>

## ACID

### **What is ACID?**

In database systems, ACID (Atomicity, Consistency, Isolation, Durability) refers to a standard set of properties that guarantee database transactions are processed reliably.

**Atomicity**

Atomicity means that you guarantee that either all of the transaction succeeds or none of it does. You don’t get part of it succeeding and part of it not. If one part of the transaction fails, the whole transaction fails. With atomicity, it’s either “all or nothing”.

**Consistency**

This ensures that you guarantee that all data will be consistent. All data will be valid according to all defined rules, including any constraints, cascades, and triggers that have been applied on the database.

**Isolation**

Guarantees that all transactions will occur in isolation. No transaction will be affected by any other transaction. So a transaction cannot read data from any other transaction that has not yet completed.

**Durability**

Durability means that, once a transaction is committed, it will remain in the system – even if there’s a system crash immediately following the transaction. Any changes from the transaction must be stored permanently. If the system tells the user that the transaction has succeeded, the transaction must have, in fact, succeeded.

<br/>

---

<br/>

### **When is ACID needed?**

When companies want to ensure that only successful transactions are processed. When a database is ACID-compliant, it protects against data corruption, and If a failure occurs before a transaction completes, no data will be changed.

<br/>

---

<br/>

### **ACID in relation to SQL and NoSQL databases**

**SQL**

All of the major relational DBMSs adhere to the ACID principles. They all include features that ensure that the data maintains consistent throughout software and hardware crashes, as well as any failed transactions.

While these characteristics seem obvious for most of the applications, they are **not** suitable for horizontal scaling, high availability, performance and fault tolerance.

**NoSQL**

NoSQL databases are a bit different. NoSQL databases are often designed to ensure high availability across a cluster, which usually means that consistency and/or durability is sacrificed to some degree. However, most NoSQL DBMSs can provide atomicity to some degree.

Most NoSQL DBMS work on a eventually consistent basis, meaning that, data may be out of sync for a time, but it will eventually be in sync.

However, some vendors, such as MarkLogic, OrientDB, and Neo4j offer ACID compliant NoSQL database management systems.

<br/>

---

<br/>

## Base

The BASE systems allow horizontal scaling, fault tolerance and high availability at the cost of consistency. So, if your application requires high availability and scalability, a NoSQL Database built on BASE properties might be suitable.

- **Basically Available**: The system is guaranteed to be available in event of failure.
- **Soft State**: The state of the data could change without application interactions due to eventual consistency.
- **Eventual Consistency**: The system will be eventually consistent after the application input. The data will be replicated to different nodes and will eventually reach a consistent state. But the consistency is not guaranteed at a transaction level.

<br/>

---

<br/>

### **Types of failure**

**Transaction failure**

A transaction failure could occur due to bad input or some other violation of consistency. It could also be due to a timeout or deadlock in the DBMS.

**System failure**

A system failure can be caused by a bug in the DBMS code, an operating system fault, or a hardware failure.

**Media failure**

Media failure refers to the condition of not being able to read from or write to a storage device (such as the hard disc). This could be caused by the media itself, or it could be due to bugs in the operating system.

Media failure is usually quite rare when compared to the other two types of failure.

<br/>

---

<br/>

## Most popular databases

**SQL**

- MySQL
- PostgreSQL
- MariaDB

**NoSQL**

- MongoDB
- Cassandra
- Redis

<br/>

---

<br/>

## When to choose NoSQL

1. Semi-structured or Unstructured data / flexible schema
1. Limited pre-defined access paths and query patterns
1. No complex queries, stored procedures, or views
1. High velocity transactions
1. Large volume of data (in Terabyte range) requiring quick and cheap scalability
1. Requires distributed computing and storage
1. No Data Warehouse, Analytics or BI use cases

## When to choose SQL

1. Consistent data/ACID transactions
1. Complex dynamic queries requiring stored procedures, or view
1. Option to migrate to another database without significant change to existing application’s access paths or logic
1. Data Warehouse, Analytics or BI use case

## Strong consistency

In SQL, strong consistency refers to the idea that all server nodes MUST contain the exact same data. This can only be done by locking down the nodes as they are being updated. Locking nodes in this way prevents concurrent updates in all other nodes, so for a brief moment in time only one of the nodes is allowed to receive an update. This is terrible for social media platforms but great for services dealling with finances, where consistency needs to be air tight.

## Use cases for SQL

In general, if your application needs strong consistency, transactions, or relationships, go for SQL.
Some examples of apps that need strong consistency include:

- Stock trading
- Banking

Some exmaples of apps that generally use relationships:

- Facebook (Meta)
- LinkedIn

[A good reference for more details](https://www.dataversity.net/choose-right-nosql-database-application/)

## Eventual consistency

Unlike SQL databases, NoSQL databases do not have a strict policy about consistency. This is designed with scale in mind. Where a SQL will pause all concurrency updates, NoSQL actively encourages this behavior, allowing all nodes to concurrently update will new data. The idea is that over time all nodes should be consistency, and this behavior is acceptable because a little bit of inconsistency is a fair price to pay for rapid scalibility.

## Cons of SQL

SQL databases have one major limitation: scaling. In order to scale a relational database, you have to shard and replicate to make them run smooth in a cluster, which could require careful planning and a good amount of resources.

## Use case for NoSQL

NoSQL databases are built to scale and can nodes to a cluster very quickly with few hiccups. Besides scale, NoSQL databases also require very little human intervention, which can reduce the manpower required to maintain and scale systems that need to serve millions quickly. There are very good reasons to choose a NoSQL database over a traditional SQL database:

**Handling a large number of read and writes**

NoSQL databases are built to handle a large number of read-write operations. This is because of the 'eventually consistent' model. They can handle big data with minimal latency, so choose NoSQL if you want to scale quickly at the cost of consistency.

**Flexibility with data modeling**

Since there are fewer limitations to building models in a NoSQL database, rapidly developing and changing models on the fly as the requirements of a model become solidified during the development process.

**Data analytics**

NoSQL databases are also a good fit for data analytics because of its ability to handle large numbers of reads and writes.

## Cons of NoSQL

In order to gain much of the scalabilty that NoSQL databases have, some features had to be sacrificed.
Amongs these features, the most critical are consistency and no ACID support for transactions.

**Inconsistency**

Data in NoSQL databases are not normalized, which introduces the risk of being inconsistent. The idea is that 'eventually' data can be normalized over time, but not tackling this issue upfront can present itself as an issue to developer attempting to normalize data at a later time.

**No ACID support for transactions**

A few NoSQL databases claim to support this feature, though they don’t support them at a global deployment level. ACID transactions in these databases are limited to a certain entity hierarchy or a small deployment region where they can lock down nodes to update them.

<br/>

---

<br/>

## When would use both?

The idea of using several distinct persistence technologies such as PostgreSQL or MongoDB is known as 'polyglot persistence'. There are many reasons why a company would choose to do this.

Let's take Meta, formerly Facebook, as an example. There are many complex relationships that exist among users of the platform. For this use case, a relational database would seem to fit the bill.

For frequently accessed data, we would want to implement a cache, so a technology like Redis or Memcached would seem to work well for this use case.

What about analytics? The users of Meta are generating massive amounts of data, for this use case we can use Cassandra or HBase.

Meta is very popular and so it makes sense for the company to run ads, so we're not talking about a payment system, which needs strong consistency and ACID transactions -- relational database it is!

Meta also has a recommendations feed to keep users engaged, for this feature it would likely be best to use a graph database.

What about the search feature that allows users to search for other users, businesses, etc? In this case a document oriented store like Elasticsearch would work best.

<br/>

---

<br/>

## Multimodel database

Mulitmodel databases support many types of models, including many of the ones mentioned eariler. This allows us to leverage different data models from a single api.

**Popular multimodel databases**

- ArangoDB
- CosmosDB
- OrientDB
- Couchbase

<br/>

---

<br/>

## Types of databases

### **Document-oriented database**

Leading type of document-oriented databases are NoSQL.They store data in a document-oriented model in independent documents. The data is generally semi-structured and stored in a JSON-like format. This type of database is easier for developers to use because of the similiarity to the data model of the application code. Document-oriented databases work very well with agile software development methodologies.

**Most popular**

- MongoDB
- CouchDB
- OrientDB
- Google cloud datastore
- Amazon DocumentDB

---

**When to choose document-oriented data (NoSQL)**

1.  While working with semi-structured data and need a flexible schema that will change often
1.  Aren’t sure about the database schema when you start writing the app
1.  Need to scale fast and stay highly available

Typical use cases of document-oriented databases include:

- Real-time feeds
- Live sports apps
- Writing product catalogues
- Inventory management
- Storing user comments
- Web-based multiplayer games

Being in the family of NoSQL databases, document-oriented databases provide horizontal scalability and performant read-writes because they cater to CRUD (Create Read Update Delete) use cases. These include scenarios where there isn’t much complex relational logic involved and all we need is quick persistence and data retrieval.

---

### **Graph database (NoSQL)**

Graph databases are the SQL of the NoSQL world. They are built to store data as nodes/vertices and edges. When SQL is too slow or requires many complex queries, graph databases come in handy. Being part of the NoSQL family, they follow the same principles, so the end result is complex relationships without the latency.

**Adjacency lists and the adjacency matrix**

Graphs are represented primarily as an adjacency list or adjacency matrix. Adjacency Matrix ideally helps figure out queries like if a relationship between two nodes exists, in constant time O(1), though it is a bit space-intensive. If the nodes in a graph contain a lot of edges, we tend to represent it with the adjacency matrix. On the flip side, if the edges are sparse, we represent the graph using the adjacency list.

**A note on speed**

Graph databases are faster than regular SQL databases because how the data is persisted. A SQL database will join tables during the query, which can lead to slow performance for very complex queries. On the other hand, a graph database persists data as a graph with vertices and edges.

**Real world use cases**

One case is Google maps, where nodes represent cities and edges are the roads between these cities. The entire application is one big map that heavily uses graph theory to find the shortest distance between the two places. In graph theory, based on the use case, different algorithms are used to calculate the shortest path between two nodes. A few of the popular ones are Dijkstra’s algorithm, Bellman-Ford algorithm, A\* search algorithm, Floyd–Warshall algorithm, Johnson’s algorithm, and the Viterbi algorithm.

Another case is Google's page rank algorithm, where the web pages are considered as nodes and the links between them are the edges. Moreover, there are weights attached to these edges, granting authority to the most relevant pages.

---

### **Key-value datastore (NoSQL)**

These databases use a simple key-value pairing method to store and quickly fetch the data with minimum latency. Due to this minimum latency, these databases are primary used as caches. There are no query languages required to fetch from the database, making it very fast and simple to use.

**Most popular**

- Redis
- Hazelcast
- Riak
- Voldemort
- Memcached

**When to choose key-value datastores**

When you want to fetch data as really quickly. Key-value stores are built to serve use cases that require super-fast data fetch.

**Use cases**

- Caching
- Persisting user state
- Persisting user sessions
- Managing real-time data
- Implementing queues
- Creating leaderboards in online games and web apps
- Implementing a pub-sub system

---

### **Time-series database**

Time-series databases are specialty databases that are optimized for tracking and persisting data that is continually read and written in the system over a period of time.

**Why use a time-series database**

Time-series databases are great for tracking the behavior of the system as a whole. It allows us to study user patterns, anamolies, and how things change over time. Time-series data is primarily used for running analytics and deducing conclusions. It helps the stakeholders make future business decisions by looking at the analytics results. Running analytics enables us to evolve our product continually. Regular databases are not built to handle time-series data.

**Most popular**

- Influx DB
- Timescale DB
- Prometheus

**When to choose a time-series database**

Choose a time-series database when you need to manage data in real-time, continually over a long period of time.

Some examples:

- Real-time cognitive fraud detection
- Monitor vertical lining green walls and plant installations

---

### **Wide-column database (NoSQL)**

Primary use of wide-column databases are for big data. Wide-column databases are perfect for analytical use cases. They have a high performance and a scalable architecture. Column-oriented databases, or wide-column databases, store data in a record with a dynamic number of columns. A record can hold billions of columns.

**Most popular**

- Cassandra
- HBase
- Google BigTable
- ScyllaDB

**When to choose a wide-column database**

If you need to work with big data. Wide-column databases are built to manage big data, ensuring scalability, performance, and availability.

Some examples:

- Netflix uses Cassandra in the analytics infrastructure
- Adobe and others use HBase for processing large amounts of data
