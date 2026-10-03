# WHat is space and time complexity.
- Time complexisty states that as the input grows, how does the amount of work done by algorithmn increases.

- Type os Big O Noation
1. Big O(1) -> constant time. for example finding first element of arr.
2. Big O(n) -> The amount of work done by algorithm grows linearly as input inxrease.
For example printing array elements.
3. Big O(n^2) -> states that the time becomes quadratic for example nested loops.
4. Big O(log n) -> O(log n) means the algorithm's work grows logarithmically as the input size increases, usually because the algorithm reduces the problem size by a constant factor (commonly half) at each step.

# What is databse scaling?
- As the users for our app increases it created more load on DB. and the db quiries becomes much slower as the data increases.
- we need to scale our db to make our db handle load efficeintly. and we need to scale db gradually for example if we have 10k users there is no point of scaling db for 1 million users.

# What is indexing.
- Before indexing if we want some data. Db will scan the whole db to find that row. Because db does the full db scan the time complexity for that is Big O(n). which will become slower as the data grows.
- But indexing allows the db to directly find the rows which is needed, which is more faster.
- For indexing we need to make the particular column index and than the db will create the copy of index column in ds called B trees and store it. using the B tree data structure db can find specified row in time complexity of O(log n).
- In postgress Primary key is already indexed but for to make any column index we just need to add single line in scheema or sql query and rest will be handled by the DB itself.

# What is partioning?
- Parititioning spilts the the whole table into smaller sub tables and which can be host on single server.
- The indexing can also become slow if the table becomes much larger. To make the queries faster and scalable we can partion the table and each sub table will have their own index which will make the query much faster.
- the db query syntex will same for multi sub tables as compare to qurying normal table.
- For example, suppose we partition by created_at:
SELECT *
FROM users
WHERE created_at >= '2026-01-01';
- PostgreSQL can determine:
users
├── 2024 partition  ❌ skip
├── 2025 partition  ❌ skip
└── 2026 partition  ✅ search

- Partitioning divides a large table into smaller physical partitions. When a query contains the partition key, PostgreSQL can often skip irrelevant partitions using partition pruning, reducing the amount of data it needs to examine.

# How to partion table.
- Suppose there is table which have become realy large.
- Partition by Range
- CREATE TABLE "User" (
    "id" SERIAL NOT NULL,
    "name" TEXT NOT NULL,
    "email" TEXT NOT NULL,
    "createdAt" TIMESTAMP(3) NOT NULL DEFAULT CURRENT_TIMESTAMP,

    CONSTRAINT "User_pkey" PRIMARY KEY ("id")
) PARTITION BY RANGE ("createdAt");

- Then create partitions:

CREATE TABLE "User_2025"
PARTITION OF "User"
FOR VALUES FROM ('2025-01-01') TO ('2026-01-01');

CREATE TABLE "User_2026"
PARTITION OF "User"
FOR VALUES FROM ('2026-01-01') TO ('2027-01-01');

- indexes:

CREATE INDEX "User_2025_email_idx"
ON "User_2025" ("email");

CREATE INDEX "User_2026_email_idx"
ON "User_2026" ("email");

# WHat is Master Slave Architecture/ Primary + Read Replicas?
- Even after doing the indexing, partitioning and verticaly scaling of db. If the database is struggling because of high read traffic, we can use read replicas to distribute read load." and implement master slave approch.
- In master slave acrhietecture we have have one db server which only perfom the write operations and have multiple slave db servers which only performs read operations. the data replicated from master node to slave nodes async or sync oon the basis of config.
- But what if master node goes down?? Than in that case we can promote the slave/standby node to primary node.

- The primary handles writes:
INSERT
UPDATE
DELETE

Replicas can handle reads:
SELECT

# What is sharding?
- In sharding we first partition the db and than host the sub data set on the server which is called shard.
- We can slit the data on the basis of range and the column which is used for shard is call sahrding key.
- In sharding we have to write the code to route request to the subsequent shard which is have that appropriate range of data.
- The system needs a routing mechanism that maps the sharding key to the appropriate shard. This routing can be implemented in the application, a proxy/router, or handled by the database system.

# Sum up of Database Scaling
After you read the DB Scaling section, let us remember these rules:

1. First, always and always prefer vertical scaling. It's easy. You just need to increase the specs of a single device. If you hit the bottleneck here then only do the below things.
2. When you have read heavy traffic, do master-slave architecture.
3. When you have write-heavy traffic, do sharding because the entire data can’t fit in one machine. Just try to avoid cross-shard queries here.
4. If you have read heavy traffic but master-slave architecture becomes slow or not able to handle the load, then you can also do sharding and distribute the load. But it generally happens on a very large scale.

Single DB
   │
   ▼
Vertical scaling
   │
   ▼
Indexing
   │
   ▼
Partitioning
   │
   ▼
Read replicas
   │
   ▼
High availability / failover
   │
   ▼
Sharding / distributed DB
