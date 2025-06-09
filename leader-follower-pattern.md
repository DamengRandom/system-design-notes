# Leader-Follower Replication Strategy 

## What is leader-follower pattern?

- A replication strategy:
  - one server is the leader and the others are followers
  - leader handles write operations and followers handle read operations to the database
  - If leader fails, need to elect a new leader from the followers (like Kafka producer leader election)

## Technologies:

- PostgresSQL + MySQL: supports leader-follower pattern (built-in feature)
- MongoDB: Offers automatic failover and replication, single primary node handles writes, others acts secondaries
