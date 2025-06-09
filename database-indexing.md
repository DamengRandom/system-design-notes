# Database Indexing

## What is indexing?

- Indexing is a technique to speed up database queries.
- It is a data structure that stores a copy of a subset of the data in a database.

## How?

- Choosing the right columns to index (Indexing can improve read performance, but it slows down writes)
- Clustered index: data is ordered to match the index, non-clustered index: index contains pointers to the unordered data

## Technologies:

- B-tree index: most common index type (supports both range and exact match queries), used in MySQL, PostgreSQL, etc.
- Hash index: best for exact match but not for range queries, used in Redis, MongoDB, etc.
