# Database Sharding

## What is database sharding?

- Database sharding is a technique to split database into smaller chunks / parts, allow data to be accessed by multiple servers.

## Why use database sharding?

- To improve performance and scalability.
- To improve availability and reliability.
- To improve manageability and maintenance.

## Popular sharding algorithms 

- Range-based sharding: shards are defined by a range of values, eg: user_id from 0 to 1000000
- Module-based sharding: data assigned by a hash key, hard to scale, reshuffle everything after adding/removing shards

## Need to know:

- Sharding key: choosing the right shard key is affacting the data distribution and query efficiency, eg: user_id, bad shard key causes hot shard issue
- Rebalancing: moving data between shards when traffic grows or hardware changes, which is a bit tricky, might cause down time issue 
- Avoid to use joins, transactions or queries across shards, which are quite slow and complex (❌)
