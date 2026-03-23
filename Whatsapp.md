# Chatting Application / Whatsapp
- Requirements
- Entities
- APIs
- High Level
- Deep Dive

## Requirements 
### Functional Requirements - User can
- send message to another user
- send message to a group of users
- see if the message is sent and read
- check if another user is online, offline or last seen time
- Send images / files and videos

### Nonfunctional Requirements - System can
- Scalability - Handle large no. of users send multiple messages in single point of time
- Reliability - Even the system is down, the user messages are not lost
- Avaliblity >>> Consistency
    - user should be able to send message at any point of time
    - eventual consistency is acceptable
- Security 
    - Only the sender and receiver user can see the message sent among them.

## Entities
- User
- Group
- Message

## APIs
- CRUD on user
- CRUD on group
- POST /sendmessage - userid, List of fileid, groupid, text

## High Level
- Client - server - DB
- DB
    - User = id, info
    - Conversation - id, type (direct / group)
    - ConversationMember - conversationId, userId (FK)
- Servers
    - Chat Server
        - Responsible to send all kinds of messages
        - When user sends attachement, the file is store in the Blob storage and in the message, the link to the file is shared in the message
        - Also responsible to give the user status
    - R/W Estimation
    - DAU = 100M, Each user = 10 messages
    - Read and write = 100M * 10 = 1B message a day = 1B / 10^5 = 10K message per sec

## Deep Dive
- Server
    - As the server, has lot to responsibility, we should divide it into different servers
    - Message Server - for all message related activities
        - Horizental scale
        - Is Kafka needed for transfering the messages ? NO - high latency
            - Topic for each user - Not possible
        - Need consistenct hashing + Zookeeper ok for multiple servers ? Yes but latency when the servers are added / removed
        - Redis Pub / sub -- RESEARCH
            - Inbuilt support 
        - Need a load balancer
    - Session Server
        - All the user will be connected to server using web sockets 
        - All the info about web sockets are maintained using session server
    - When the user send a message, the message goes and sits in a queue, when the network is connected, it moved to the receivers queue
    - Also, a thread is opened, that is responsible to do all the api calls for the user
