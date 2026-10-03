# WHat is space and time complexity.
- Time complexisty states that the as the input frows, how does the amount of work done by algorithmn increaes.

- Type os Big O Noation
1. Big O(1) -> constant time. for example ffinding first element of arr.
2. Big O(n) -> The amount of work done by algorithm grows linearly as input inxrease.
For example printing array elements.
3. Big O(n^2) -> states that the time becomes quadratic for example nested loops.
4. Big O(log n) -> O(log n) means the algorithm's work grows logarithmically as the input size increases, usually because the algorithm reduces the problem size by a constant factor (commonly half) at each step.

# What is databse scaling?
- As the users for our app increases it created more load on DB. and the db quiries becomes mucs slower as the data increases.
- we need to scle our db to make our db handle load efficeintly. and we need to scle db gradually for example if we have 10k users there is not point of scaling db for 1 million users.

# What is indexing.
- Before indexing if we want some data. Db will scan the whole db to find that row. Because db does the full db scan the time complexity for that is Big O(n). which will become slower as the data grows.
- But indexing allows the db to directly find the rows which is needed, which is more faster.
- For indexing we need to make the particular column index and than the db will create the copy of index column in ds called B tres and store it. using the B tree data structure db can find specified row in time complexity of O(log n).
- In postgress Primary key is already indexed but for to make any column index we just need to add sinlge line in scheema or sql query and rest will be handled by the DB itself.