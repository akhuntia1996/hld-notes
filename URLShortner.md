### This File contains the HLD Interview Guide and URLShortner 
# URL Shortner
- Requirements
- Entities
- APIs
- Data Flow
- High Level (Satisfying Functional Req)
- Deep Dive (Satisfying Non Functional Req)

## Requirements
### Functional Requirements (Define that User can and User will)
- Create a short URL from the long URL
    - give his own alias for short URLs
    - Set his own expiry date for his URLS
- Redirect to the long URL when he used the short URL

### Non Functinal Requirements (Define what system should do)
- Use CAP Theorom
    - Partition Tolerance is always ON
    - We have choose among Avalibility and Consistency
    - Consistency = Read same data after every write, other wise throw error
    - Avalibility = Always able to read some data
- Need Avalibility = Let user wait if the shortner is begin processed
- Low latency = for new short url creation and shorturl lookup 
- Scalability = Ask the interviewer first
    - 100M DAU

** We dont need to do Back Of Envolope Estimation right now. We can do them if needed when while deep dive design **

## Core Entities
- LongURL
- ShortURL
- User

## APIs
- POST /shortUrl 
- GET /{shortUrl}

## High Level
- ONLY FOR FUNCTIONAL REQUIREMENTS
- Client -> Server -> DB
- Client = getShortUrl(longUrl) & redirect(shorUrl) 
- Server = create a shortUrl and lookup for long url
- DB = UrlTable -> userId, longUrl, shortUrl / alias, expiry date, creation date
- How to URLs are shorterned ?
    - Take the prefix for long URLs - not recommended
    - Base62 Approach
        - Can have collisiions
        - Retry
        - Need lookup DB
    - Hashing Approch
        - MD5 Algo
        - Can have collisions
        - Retry
        - Need Lookup DB
    - Counter
        - Always Unique
        - No need to lookup DB

## Deep Dive 
- SCAN THROUGH ALL THE COMPONENETS AND CHECK HOW IT CAN BE SCALABLE
- Client - No needed
- Server 
    - 1st option is vertically scaled - not recommended
    - R/W estimation
    - 100M DAU = 10^8 daily = 10^8 / 10^5 sec = 1000 req per sec (Read, if 1 user req per user)
    - Read Heavy
    - We can divide the server into 2 parts - Read Service and Write Service
    - Read Server can autoscaled when required using AWS EC2 instance, and dropped when the req become less than 20%
    - Add a load balancer to send requests in read servers
    - Add a API gateway to request to read/write servers
    - NOTE ::: As the logics in read and write have less logic to make it into diff servers.
- Database
    - Cache before read server before hitting the DB
    - Write server directly write to DB
    - DB can be sharded or partitioned internally
        - Key can be location key
    - Storage Estimation
    - 1B URLS = 10^9 * (7 chars) = 7B chars = 7GB - not required sharding
- Counter Service
    - Another MS, bit of latency for each counter
    - For each write server, get a range for counter like 1-10K for server 1
    - These counter server can be handled by zookeeper
