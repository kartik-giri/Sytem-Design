# What is distributed system?
- The distrbuted system is the system in which muliple independent computer are coneected to each other and comunicate with each other over a single netwrok to complete a certain task.
- The distributed system distrbutes the computation, data or both in certain cases.
- If we want to distribute database. There are 2 ways Replicating and SHarding.
- Replication: In this we replicate the databse copy to the difference node. so load can be transfer and managed efficiently.
- Sharding: In this we split the dataset into smaller sub data set and stored in to different node. so the user req can be route to the node which have that data only.

# What is CAP Theoram?
- CAP Theoram states the very important tradeoff we need to make while creating system. It states that we can only chose between CP or AP
- CAP is made of 3 words.
- C = Consistency, A= Availability, P = Partition Tolerance

1. Consistency -> Means that users/nodes can store and read same data and same time.
2. Availability -> Means all the reqesut will be handled by the server even if it suceeds or fails.
3. Partition Tolerance -> Means System works despite of connection failure between nodes.

# For Example:
1. There are nodes A, B and C in the distrbuted system.
2. Suppose a network partition happens and B losses its communication with node A and C.
3. If we want to allow the users to send request to the system than in that case node B can't propogate it's changes to node A and C. And we acchieve Availability at the cost of Consistency.
4. But if we want consistency in the data between nodes than in that case we make server unavailable and wait until node B cmmunication connection is being fixed. In this case we get consistency at the cost of Availability.

- CP -> IS best for banking apps. where inconsitent data can be serious probem.
- AP - IS best for social media apps. where inconsitency in data doesn't make serious problem