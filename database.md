# Database Design

## Types of database:

- Relational database:
  - MySQL, PostgreSQL, Oracle, SQL Server, etc
  - Store data in tables, each table has a primary key
  - Use SQL to query the data
  - Use JOIN to query the data across multiple tables
  - Use transactions to ensure data consistency
  - Use indexes to improve query performance
  - primary & foreign key relationship
  - ACID properties: Atomicity, Consistency, Isolation, Durability

- Non-relational database:
  - MongoDB, Redis, Cassandra, etc
  - Does not have primary & foreign key relationship
  - Saved data as key-value pairs, JSON format
  - Simple queires, compared with relational database, which is more complex

- In-memory database:
  - Redis, Memcached, etc
  - Store data in memory, which is faster than disk
  - Use key-value pairs, JSON format
  - primarily for caching, session management, real-time data processing, etc
  

## Database scaling:

- Vertical scaling:
  - Increase the resources of the existing server
  - Increase the CPU, memory, disk, etc
  - Upgrade the network

- Horizontal scaling:
  - Add more servers to the cluster
  - Add more nodes to the cluster
  - Database Sharding: split the data into multiple shards, each shard is a part of the data
  - Replication: copy the data to multiple servers, so it will be highly available to the end users
    - Master-Slave replication: one master server (for write operation), multiple slave servers, which is used for read scalability
    - Master-Master replication: multiple master servers, which is used for read & write scalability

## Database performance:

- Caching: performance improvement by storing frequently accessed data in memory
- Indexing: performance improvement by creating indexes on the columns that are frequently used in queries
- Query optimization: eg: minimize the number of joins, minimize the number of scans, minimize the number of disk I/O, etc

## Database security:

- Authentication: eg: username & password, JWT token, OAuth, etc
- Authorization: eg: RBAC, ABAC, etc
- Encryption: eg: AES, RSA, etc
- Data sanitization: eg: SQL injection, XSS, etc
