# Prequisite knowledge

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

# Most popular databases

## SQL

- MySQL
- PostgreSQL
- MariaDB

## NoSQL

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

[A good reference for more details](https://www.dataversity.net/choose-right-nosql-database-application/)
