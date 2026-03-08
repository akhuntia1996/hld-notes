# Chapter 7 - Transactions
## ACID
- Atomicity = All operation succed or none
- Consistency = One valid state to another with stricly defining rules and contrains
    - Like Order created but user do not exist
- Isolation = Ensure concurrent txn do not interfer
- Durability = Once the txn is completed, the data is not lost

## Problems with concurrent txn
- Dirty Reads
    - Reading uncommited data
    - A changes, B Reads, A rollback
    - B did a dirty read
- Non Repeatable Read
    - Read diff data when read repeatedly
    - A read 100, B update 200, A read again 200
- Phantom Read
    - Read diff when new rows appear

## Isolation Levels
- Read Uncommitted 
    - No prevention
- Read Committed
    - Only committed data can be read
    - Avoid dirty read
- Repeatable read
    - Try non-repeatable reads
    - cache to store the existing values
- Serailzable 
    - Trax behave as they as an one entity
    - slow performance / locking

## 2 approches of concurrent locking
- Locking - Shared and Exclusive
- Multi Version Concurrency Control
    - DB maintains version of data 
    - Less lock on single version of data
    - better read

## Snapshot Isolation
- Periodically, take snapshot 
- avoid diry read and non-repeatable read

## Write Skew Problem
- 2 txn read same row and tries to update
- Both acquire the lock and wait for each other

## Distributed Txn
- Txn on multiple nodes

## 2PC
## Eventual Consistency
- Scalability > strong Consistency 

# Chapter 8 - Distributed Systems
## Concepts
- Unreliable Networks
- Partial Failure
    - Only the part of system may fail
- time out and reties
- Idempotency APIs
- Network Partition 
    - 2 node cannot comm with each other
    - consistency problems
- Unreliable Clocks
    - Not perfectly sync while adding timestamp
    - Use Syncronisation Clocks
        - NTP - Network time protocols
        - small drifts can happen
        - clock can be adjusted forward / backward
    - Logical Clocks
    
