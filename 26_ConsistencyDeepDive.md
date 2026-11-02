# Consisteny Deep Dive

- Consistency means every user/node stores and read the same data at same time.
- Consistency is very important concept in statefull distrbuted systems  like databases.
- In CAP theoram to achieve consistency we need to leave the availability.
- Because for example there are three nodes A,B,C if the network failure happens and B node loses it's connection between node A and C than node B can't propogate its changes to node A and C.
- So that's for consistency of same data across distrbuted nodes we need to make our server unavailable untill connection reestrablished between node A,B and C.
- There are 2 types of consistency Strong and eventual consistency. In strong consistency each node should return same data after the write.
- The write should be synchrnously updated in replicas nodes.
- It ishould be used in Banking apps.
- Evventual consistency is the consistency in which write is eventually updated on replicas nodes.
- And replicas nodes doesn't return the updated data immediately after the write.
- In this availability is much higher.
- We can use eventaul consistency in social apps.

# CAP does not say that every node must shut down during a network partition.
- Imagine three database nodes, A, B, and C. Node B loses its connection to A and C.

- A and C can still communicate and may form a majority quorum.

- B may reject requests that it cannot safely process.

- A and C can continue serving requests if the database's consistency protocol allows it.

- The goal is to prevent conflicting writes or stale reads that violate the consistency guarantee—not to shut down every server.

- Remember this distinction:

- Strong consistency is a guarantee about data operations. It is not a command to shut down servers.
