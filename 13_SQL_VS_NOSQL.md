# What is ACID?
- The transaction is the group of db operations which should be taken as the single logical unit.
- ACID has 4 properties that makes db transaction relible.
- ACID is made up of 4 words.
- A -> Atomcity
- C -> Consistency
- I -> Isolation
- D -> Durability

1. Atomcity -> treat the txs as on all or nothing unit. if the single operation of db tx is being failed than whole tx is being rolled back.
2. Consistency -> Means db txs takes db from one valid state to another. Txs should follow all the db constraints, invariants, rules etc.
3. Isolation -> all the concurrent txs should be executed seprately from each other. to prevent data correuption.
4. Durability -> Means after commiting the txs the data in db should persist even after server crash.

# SQL vs NOSQL
1. SQL - The sql db stands for Structured Query Language db. the sql db follows the strict rows and columns scheema.
- the data in sql db is stored in rows and columns tables whcih follow strick scheema and relationship among tables.
- Scheema is implemented on the db level.
- For example mysql. postgressql etc
- The sql db is mostly scaled vertically but we can also horizontally scaled the sql db as our app grows.
- But sharding in sql db can be very complex operation to do because we implement very complex queries in sql like join from differnt shard can be very complex.
- We should use sql/relational db where we want structured data, complex relationships, transactions, constraints, and strong data integrity like backing apps.

2. NOSQL - The NOSQL db is the non-sequential db in which we can store data more felxibily and the scheema is not implemented at the db level.
- The data is more flexible in NOSQL DB which can lead to inconsistent db some time.
- NOSQL db is usually scaled horizontally means adding more machines in the db cluster.
- NOSQL db should be used in the cases where inconsisteny in data doesn't lead to catostrohic stituation for example social media apps.