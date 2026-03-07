# Chapter 1 
## Reliability 
- Continues to work correctly even if the things go wrong.
- Type of failure
    - H/W or S/W failure
    - Human error
    - Network Problems
- Solution
    - Redundancy (DB Replication)
    - Fault Tolerance (Multiple Server with Load Balancer)
    - Monitring and Altering
    - Isolation (One server fails should not affect others)

## Scalability 
- Vertical and Horizontal Scaling
- Measure - Req/sec, Read/Write
- Handling Load
    - Load balancer
    - Caching
    - Replication
    - Partitioning / Sharding
- Latency - Time taken in 1 sec
- Throughput - No. of req per sec

## Maintainability
- System should be able operate, understand and modify
- 3 Principles 
    - Operatibity 
        - Monitor, deploy, debug and recover
    - Simplicity
        - simple APIS, modular design, abstractions
    - Evolvebility 
        - new feature, schema changes and scaling needs

# Chapter 3
## How DB stores data ?
- B Tree (Old)
    - Self balancing tree, sorted data, good for search
    - good read performance
    - good for range
    - Postgres SQL
- LSM Tree
    - for distributed txn
    - Like B tree
    - Based on memtable and asnyc with SSTable at disk
    - High R/W
    - Cassendra
- LSM Tree and B Tree are constructed in Memtable in-memory
- SSTable (Sorted string table)
    - immutable
    - sorted by Key
- Compaction
    - When lots of LSM trees are convert to SSTables, lots of data are needed
    - May contains duplicates
    - Process
        - Merge all SSTables
        - Remove old entries
        - Write compaction

** NOTE : Read Heavy + Balanced Data = B Tree **
** NOTE : Write Heavy + Distributed DB = LSM Tree **

## Append Only Log Storage
- Always append logs for when DB changes
- slow
- Solution = Indexing

## Index
- Directly jump to recored
- Index on column
- Trade off
    - slow writes
    - Exta storage

## Bloom Filters
- Probalistic DS
- Just to tell in the key exist or not
