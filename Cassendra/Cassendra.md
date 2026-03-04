# Cassendra
- NoSQL DB
- KeySpace = Database
- Table, Row, Columns
- Each row can have different set of columns
- SCALABLE, AVALIABLE AND FAULT TOLERANCE

## Scalability 
- Data is stored in distributed nodes
- New data is stored base on Partition Key
- PRIMARY KEY = Parition Key + Clustere Key
- Cluster Key shows how the data is stored in a node
- Hash the userId (example for partition key) to find which node to go to.
- Consistenct Hashing

## High avalibility and Fault tolerance
- Dont have a leader or a co-odinator
- then how to know which node is added or dropped ?
- GOSSIP protocol
- Each node talks to few nearst node to know their status
- like isAlive, list of dead nodes, etc
- Eventually, all the node will have this data for all other nodes

## CAP Theorom
- More Avalibility than conssistency
- Tunable Consistency 
    - ONE - only replicated to one node - fast but weekest
    - QUORUM - Majority Node - balanced
    - ALL - all nodes replicated

## Write Request
- 1st writen to Memtable in RAM
- Once it is full, it is flushed in SSD Table in Disk
- All req are written to Commit Log file in Disk

## Read Request
- 1st check the memtables
- Then SSD tables
- Contains bloom fliters + Index to make it faster

## Data modeling 
- No normalization - No Join, No FK
- Query Driven
- RDBMS = Entity Driven

## When to Use ?
- high write throughput
- It can't have strong consisitency 
