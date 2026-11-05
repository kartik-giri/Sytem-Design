# What is Rate limiter?
- Rate limiter is the mechanism that controls how many req client can send to the server with in a specified period of time.
- In simple words it puts the limit on how frequently users can use the api.

- We need rate limiter because for example:
- In link shotener app we are exposing api to short the link.
- The hacker can create the script which sends 10,000 req in short time to overwhelm our system.
- Which make the system slow.
- Consumes the system resources like storage and processing.
- and makes the genuine users suffer.
![Rate limiter attack](../img/RateLimiterAttack.png)

- The rate limiter keeps the track of requests sent by client in a specified period of time.
- For example we want client to send 5 req per miniute not more than that.
- If user makes req more than upper limit than server needs to return the resp with code 429
![Rate limiter](../img/Ratelimiter.png)


# Let's build it with 6 step framework.

1. CLARIFY:
- Ques-1. How do we identify who is making api call?
        - first way is using which acount is making the req.
        - second which IP is making req.
        - is track which api key the req is carry?

        - if we use IP address then one office with 100s user share single IP address.
        -  And hacker can change there IP address to make the attack.

        - if we use API than only devs can use it. Normal apps users will not be able use it.

        - If we count number of req per account than we can't do anything for anyone who isn't loged in yet.

        - Let's say interviwer tells for loged in user we need to track no of req per account and for non log in users we need to count no of req per IP address.
        log in users - track req per acc
        no log in user - track req per ip address

- Ques-2: What is the limit of req for each user?
        -  let's say 100 per minute per user.
        - How i get to this number? use traffic as the base of these number.

- Ques-3: What should happen if client crosses this limit?
        - reject the req with code 429 and tell user to send req after this much sec. with clear msg.

2. ESTIMATE: 
storage :
- Let's say the count -> time = 50 Bytes
- 50 * 10 million users = 500 MB of storage

- API call rate
- 10 million user * 100 req a day = 1 billion req
- 1 billion /1 lakh = 10,000 req per sec
- in busy time * 3 time = 30,000 req per sec on busy time

3. API
- Rate limiter only needs to check if the req is allowed or not?
- if nor return the resp with 429 code and with small note to retry after these seconds.

- where it should sit?
- it should be between server and client.
- for example in api gateway or middleware
- it sits in the request path between the client and the protected resource.

4. HLD
- ![Simple rate limiter HLD](../img/SImpleRateLImterHLD.png)
- Rate limiter algos
- 1. Fixed window counter:
     - Let's say signle user can send 100 req per minute.
     - This algo dvides the time in minutes and counts the number of req made by each user.
     - User can send only 100 req in a single minute.
     - But the problem with this algo is hard boundaries.
     - the user can send 100 req in last sec of minute window and when minutes changes the counter resets.
     - And user can send another 100 req at the first sec of minute.
     - Now user has made 200 req in just 2 sec which makes sudden burst of req.
     - The main drawback of Fixed Window Counter is the boundary burst problem. 

- 2. Sliding window log:
     - Instead of counting req in fixed window. This algo stores the timestamps of reqs.
     - for example when new req is made it keeps only those req which are made under the last 60 sec. If the total reqs are more than 100 than new req will be blocked.
     - But the draw back is that it stores the timestamp for every req which needs alot of memory.
     - ![Sliding window log](../img/SlidingWindowLog.png)
- 3. Token Bucket algo
     - In this a bucket can hold specific number of token let's say user can make 60 req per minute.
     - The tokens are generated per second in this case 1 token is generated per sec.
     - Each req consumes 1 token.
     - Req will be blocked if there is not tokens left.
     - Req will be allowed once new token is generated.
     - This algo controlls how much burst it wants. 
- We are choosing Token bucket algo because it allows us to controll the burst and bucket already knows how many tokens are left which we can send to the user.
- Each user gets there own bucket.


5. DEEP DIVES:
- What if there are muliple api gatways?
- Than we should store the token bucket in the shares storage like redis.
- Which makes the read write faster.

6. BOTTLENECK:
- 1 redis instance can handle 1 lakh operation per secs.
- Our 35k operaitions comes unders 1 lakh.
- What if redis go down?
- We can let fail open  means every req is handles even if it abuses the system.
- Or we can choose fail closes which make every req blocked until the redis become up and run again.
