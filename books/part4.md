# Chapter 9 - Consistency
## Consistency Models
- Strong Consistency = Every read return latest committed value
    - more latency 
    - hard to scale
- Eventual Consistency
- CAP

## Linearizability
- Strongest consistency Model
- system behave like a single system model

## Leader Election 
- coodination, txn ordering, conf management
- Usage - kafka, zookeeper, kubernates

## Distributed Locks
- Ensures only one node performs the task

## Concensus Problem
- Multiple Node must agree on single value
- like who is the leader ?
- Paxos Algo
    - All nodes eventually agree on same value
- Raft Algo
- Log Replication 
    - leader send the logs to the followers
    - Followers execute the command in same order
- Fault Toleracne
    - Follows 2f + 1 failures
    - 3 nodes tolerate 1 failure
    - 5 nodes tolerate 3 failures
- Zookeeper
- kafka

# Chapter 10 - Batch Processing
## Data Movement Locality 
- moving data is expensive.
- Move computation to where the data lives

