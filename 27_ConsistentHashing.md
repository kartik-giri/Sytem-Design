# What is consistent hashing?
- Consistent Hashing is just the hashing algorithm that tells which data belongs to which node.
- It is very important for statefull distrbuted systems like databases.
- Lets our app is having alot of data incoming and single db server can't handle it.
- We baught 3 db server and split the large dataset into smaller data set and host it on each db server.
- But the question is how do we determinstically distrbute the data over multiple db servers??
- The answer is hash function it is suitable for when we dont scale the number of servers further because if we change the number of server the keys position will change and we have to do large amount data movement.
- In hash function we take module of key % number of servers. And than store the data on the server according to that hash. But if server no changes keys position will change and we need to make large amount of data movement.
- The solution for hash function is consistent hashing in which we take the ip addresses of servers and hash it through the sha128 algo and map the server with that hash on clock from 0 to 128.
- And also hash the keys with sha128 and put the key on the db server which is closer to it clockwise.
- if we change the number of server than we just change those keys we comes between below new server index on clock.

- ![Consistent Hashing](./img/ConsistentHashing.png)

# How consistent hashing works
- Your clock analogy is exactly the right way to think about it. One correction: you don't have to use SHA-128 specifically. You need a consistent hash function that maps both server identifiers and data keys into the same hash space.

- For illustration, imagine a ring with positions from 0 to 127. Real implementations may use a much larger hash space.

1. Step 1: Hash the database servers

Hash each server's identifier, such as its hostname or unique ID, and place it on the ring.

2. Step 2: Hash the data keys

Hash each key, such as user:123, and place it on that same ring.

3. Step 3: Find the owner

- Starting from a key's position, move clockwise until you reach the first server. That server owns the key.

- Conceptual illustration: keys and servers share one hash ring; each key belongs to the next server clockwise.
- For example, suppose the ring has these positions:

DB A at position 20

DB B at position 60

DB C at position 100

- A key hashed to position 75 belongs to DB C, because C is the first server encountered clockwise.

A key at position 35 belongs to DB B.

The actual numeric positions are determined by hashing; these numbers are just illustrative.

3. What happens when you add a server?

This is the most important part.

Suppose you add DB D at position 80.

Before adding DB D

DB B — position 60

Owns keys after position 20 up to 60

DB C — position 100

Owns keys after position 60 up to 100

After adding DB D at position 80

DB B — position 60

Still owns keys in the interval (20, 60]

DB D — position 80

Takes keys in the interval (60, 80] from DB C

DB C — position 100

Keeps keys in the interval (80, 100]

Only the keys in the interval that now belong to DB D need to be reassigned. Keys owned by DB A, DB B, and the remaining keys owned by DB C stay where they are, assuming the existing ring positions don't change.

That's the big advantage: adding a server moves only a portion of the keys rather than potentially remapping most of the dataset.

Removing a server works similarly: its keys are reassigned to the next server clockwise.