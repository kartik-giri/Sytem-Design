# Questions I should i ask before deisgn any system.

1. How many users and how fast they are growing?
- A photo app with 1000 users and 50,000 users are completely differnce systems in 50,000 users photo app we need to deal with load bal, replicas, sharding, caching etc.
- For example at this point our app has 10,000 users and doubling every month and eventaully it will hit million in few months so we should design our app according to million users.

2. IS the app read heavy or right heavy?
- For example in photo app the users reads 1000s of photos every day but post around 2 or 4 photos per day. so our app is read heavy and we should focus more on optimizing the read feed. 

3. What data can we can never afford to lose and what data we can afford to lose?
- For example we can't afford to lose users uploaded photos.
- But we can lose likes counts for few seconds. 
- Knowing the differnce tells us to when durability matters and where not.


4. How mcuh latency I can afford?
- What should be latency of important components.
- Opening the feed should be instant under 200 ms.
- But uploading photo can take 2 or 3 seconds.
- Knowing this tell us to which components we should focus more to make latency low.

5. What does it cost?
- Every replica of db, every extra server, caching will cost real money.
- The right design is the one which meets top 4 ques with least money.

# Interview Byte 2
# At end analyse what these questions gave us. Before designng anyhting always ask these 5 ques it tells us why this app needs it and what it will cost.
# Also asks these ques to interviwer and on these basis of answers create your functional or non-functional reqs.

# What is a constraint?
- A constraint is a limitation or boundary that your system must work within.
- When an interviewer asks you to design a system, you rarely get unlimited resources. You have to consider the number of users, budget, latency, data size, technology choices, and other limitations.

For example, imagine you're designing Inkflow.
- 10,000 users can be online simultaneously.
- Each board supports up to 50 concurrent editors.
- Drawing updates should reach collaborators within 150 ms.
- The system must preserve saved board data after a server crash.
- You have a limited infrastructure budget.
These are constraints or requirements that influence your architecture.
Types of constraints

1. Scale constraints
How many users, requests, connections, or documents must the system handle?
Example: 10,000 concurrent WebSocket connections.


2. Performance constraints
How quickly must the system respond?
Example: 95% of drawing updates arrive within 150 ms.


3. Data constraints
How much data is stored, how fast does it grow, and how much can be lost during a failure?
Example: board state must persist, and acknowledged edits must survive an application-server crash.


4. Business and technology constraints
What budget, deadlines, existing infrastructure, or technology requirements must you respect?
Example: the team already uses Next.js, PostgreSQL, Redis, and WebSockets.