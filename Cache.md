# Caching
Refer the HLD notes
https://docs.google.com/document/d/13a_AgbMxF7rwOW-EO_K2GPaRSWPLbm6AkiqGnP6ITnE/edit?tab=t.0

## Where to Cache ? 
- External Caching - Cache near DB
    - Gloabally Shared - Shared across app servers - MOSTLY USED
- InProcess Caching - In Memory in Application servers 
- CDN - cache near location
- Client Side Caching - HTTP Cache, local disk
    - no control, no freshness 
    - APP offline functionally 

## Strategies
- Cache Aside - MOSTLY USED
    - if cache miss, then read for DB
- Write through - Write to cache and DB 
    - No existing tool
    - Spring cache
    - slower writes
    - Dual Write Problem 
- Write behine
    - same as Write through
    - DB update is async
- Read through
    - Same as cache aside
    - If cache miss, update the cache and then give to client

## Cache Eviction Policies
- LRU
- LFU
- FIFO
- TTL

## Deep Dives
- Cache Stamped
    - Populate data miss in cache
    - lot of req to DB
    - 2 Ways to prevent
        - 1st time hit the DB, the wait until Cache has the data
        - For every popular key, refresh the data just before expiry 
- Cache consistency 
    - Stale data in cache
    - new data in DB 
    - Prevention 
        - When new data comes, remove the key from DB
        - Have a TTL and fine with eventual 
- Hot Key
    - More hits on a single key
    - Instead of putting the key in single cache node, put it in multiple node in the cache cluster

## When to bring up cache ?
- read heavy
- expensive DB quries
- low latecy 

## How to introduce cache ?
- find to bottleneck (why you need)
- what to cache in data - cache key
- cache strategy 
- Eviction policy 
- trade offs
