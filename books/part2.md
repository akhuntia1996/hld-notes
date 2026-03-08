# Chapter 4
## Encoding
- Conveting to steam of data for data transmission 
- Used for data movement across network, storage and message queues

## Data encoding formats
- Language Specific Formats
    - Java Serailzation and Python Pickle 
    - tightly coupled with languages
- Text based formats
    - JSON, XML
- Binary Encoding Format
    - Protocol Buffers, Arvo, Thrift

## Schema Registry

# Chapter 5 
## Why Replication ?
- Scalability
- Reliability
- Fault Tolerance
- Avaliablity 
- Geographical Distribution

## Terminologies
- Primany / Leader = Write Operation
- Replica / Followers = Copy Data
- Replication Lag = Time taken to replicate
- Failover = make replica to primary 

## Types of replication
- Leader based replication
- Sync and Async Replication

## Handling Replication Lag
- Read from leader
- Read after write consistency
- Monotonic Read - Ensure user never sees older data than before
- Consistenct prefix read - Ensure data in corrected order

## Multiple Leader Replication (For Multi Region)
- Multiple Leader writing to multiple replica
- at end they sync
- CONFLICTS
- Write Conflict Resolution
    - Last write wins

## Leaderless Replication (For highly available DB)
- R/W to Replicat
- Each replica gossip with each other to nearest node
- Eventually, all node will know about all other nodes
- Condition for consistency
    - R + W > N
- Read Repair
    - Client reads multiple replicas
    - Newest value identified
    - Outdated replicas updated
- Anti Entropy
    - Async to replica

# Chapter 6
## Why Partition ?
- More write throughput
- More storage limits
- Query Performance

Refer to https://docs.google.com/document/d/13a_AgbMxF7rwOW-EO_K2GPaRSWPLbm6AkiqGnP6ITnE/edit?tab=t.0
