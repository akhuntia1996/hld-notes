# Twitter 
- Requirements
- Core Entities
- APIs
- Data flow
- High Level
- Deep Dive

## Requirements
### Functional Requirements 
- Login 
- Fetch all the Post that user is following
- Upload a Post
    - Text
    - Image
- Comment on Post
- Like on Post
- User should be able follow or unfollow user

### Non functional Requirements
- Low Latency 
- Avalibility
- Scalable
- Security

## Core Entities
- User, Post, Comment

## APIs
- POST /follow - followerId, followeeId
- GET /timeline/{userid}
- POST /post - 
- POST /comment 
- PUT /like/{postId} , PUT /like/{commentId}

## High Level
- Client - server - DB
- Client = follow(userId) / getTimelinePost() / doPost(Post) / doComment(postId) / doLike(postId) / doLike(commentId)
- Server = all functional Req
- Database
    - All Core Entities

## Deep Dive
- Server
    - Vertical Scaling - Not recommendated 
    - R/W Operations
        - 100M DAU
        - Write Post = 100M DAU * 2 Post a day = 200M Post a day = 200M / 10^5 = 200 Post a sec 
        - Read Timeline = 100M DAU * 10 post a day = 1B Post a day = 1B / 10^5 post a sec = 1K post a sec
        - Read Heavy 
    - Every read should not hit the DB
    - Cache 
        - Cache Aside Strategy - If cache miss, read from DB and update the cache
        - Eviction Policy - LRU 
    - CDN - Optional
    - Separate the Read and Write Server based on the context
        - User server
        - Post server
        - Timeline Server - Can be scaled horizentally 
            - Load balancer 
    - API Gateway 
        - For auth, rate limiting and security
- Database
    - Storage
    - 200M Post a day = 1KB * 200M = 2^11 Bytes = 200 GB * 300 = 6 PB per year
    - Huge data - Shard / Parition the data
    - Partition Key = UserId
    - Distributed PostgresSQL
    - Replication Data Factor = 3
    - Amazon s3 for images

## Other Concpts Used
### Fan Out Approaches
- Push Arch
    - When user post something, it is sent to all its followers Queue
    - Low Latecy 
    - Less read
    - But, if you are celebrity then Post will high time consuming
- Pull Arch 
    - When the user comes online he pull all the feeds from his followers
    - Intaially High Latency 
    - Every time we need to pull to refresh the feed
    - Costly Read
    - May use cache for it.
- Hybrid Approch
    - For Big people, we will use Pull and for other we use Push
- Each User will have queue
    - that queue will hold the data that will shown to the user's feed
    - Push/Pull data will be populated to this queue

## Searching
- ElasticSearch 

## Retweets
- Tweet [T1, null, info...] [T2, T1, info]

### Mutual Friends
- Table - [user, followers1], [user2, follower1]
- Graph DB - NEED TO REASEACH

### Ranking 
- NEED TO REASEARCH MORE
- Shows the feed order

## What if one of Service Crashes ?
- have multiple instances on load balancer
- do health checks /health
- Auto restart 
- Retries and timeouts

## How to improve availability of our cache?
- Cache - Redis Cluster
    - Sharding
- Replication 
- Consistent hashing

## How can we reduce media storage costs?
- Go to object storage instead of DB
- CDN
- Use compression like WebP(for images) and H264/H265 (videos)

## Desgin Recommendation System 
- ANOTHER TOPIC
