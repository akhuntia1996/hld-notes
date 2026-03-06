# High Level Design Cross Question 
### What if one of Service Crashes ?
- FAULT TOLERACNE
- have multiple instances on load balancer
- do health checks /health
- Auto restart 
- Retries and timeouts

### Distribute traffic b/w service ?
- L4 and L7 LOAD BALANCER

### Reduce DB load ?
- SCALABILITY
- Caching
- Replica
- Async Processing

### What happens when traffic suddenly spikes ?
- ELASTIC SCALING
- Auto scaling of service 
- Rate limiting
- Load balancing
- Aync Processing

### How to avoid single point failure ? // How do we design for high availability?
- HIGH AVALIABILITY
- Multiple service instances
- Multi A-Z deployment (AZ = Avaliblity Zone)
- DB Replication
- Cache cluster

### Increase Read scalability ?
- Caching 
- CDN
- Async Processing
- Rate limiting
- Elastic search for searching
- Separate Read server and upscale

### Increase Write Scalability ?
- Sharding / Partitioning
- Upscale Write Server
- Aync Processing

### DB crashes ?
- DISASTER RECOVERY
- Replication
- Write ahead log for each operation except read
- Snapshot of DB in regular intervals
- backup storage
- Automatic fail over

### Ensure Data consistency ?
- Strong Consistency
- Eventaual Consistency
- CAP Theorm

### Retries and timeouts ?
- Dead letter queues
- Expontials backoffs
- Idempotent APIs

### How to improve availability of our cache?
- Cache - Redis Cluster
    - Sharding
- Replication 
- Consistent hashing
