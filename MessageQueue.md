# Message Queue
- Decouples Producer and consumer and let them scale
- Consumer send acknowledge when he process the message, until then the message stays on queue
- Diff MQs process consumer 
    - Kafka - only one per consumer
    - Amazon SQS - for 30s the message is invisible after consumer take it for processing. After 30s, it is visible again for aother comsumers
- Consumer process the message but did not ack
    - Message might be processed multiple time but should not
    - Use delivery garentees
        - At least once - Idompotent - process same again will give same response - MOST FOR INTERVIEWS
        - at most once - fire and forget
        - exactly once - only once - not possible

## When to use message queue ?
- Async 
- Decoupling 
- Busty Traffic
- Reliability 

## Deep Dive
- Parition for diff workers
- Consumer group for handling multiple partition
- Hot Partition Keys = Even distribution
- Procuder >> Consumer
    - Autoscaling 
    - Back presser the producer - slow down the producer and retry again - IMPORTANT
    - Set alters
- Dead letter queue - store unprocessed message for later process or debugging
- When queue goes down ?
    - Replicte to diff broker (kafka)
