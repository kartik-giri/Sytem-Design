# What is caching?
- Caching is the process of storing the frequently requested data in the faster data sotrage layer to make request response cycle more faster.
- For example when client send request to server the server read the data from db and compute it on backend before returning to the user. Which in total takes 500ms.
- But if we cache the data in cache than we can reduce the response time drastically like 50ms.

- Caching meand storing the pre computed data in the faster accessible data store like redis to reduce the response time.
- For example- in blog site with caching first user can ask for blog and backend will cache those blogs and for next req backend will return the blogs from the cache to reduce the response time. And when new blog are created we can do the cache invalidation like after 24 hours new cache will be stored and past cache will be removed.

- Benefits:-
1. Reduce the latency.
2. Can handle the more throughput.

# Caching type
1. Client side caching: In this data is stored on client browser or memory cache.
2. Server side cahing: In this data is stored in datastores like redis.
3. CDN: It is used to for static content deilvery like html, css, png, mp4 etc.
4. Application level cache: In this data directly cached on the backend code. It means the application explicitly implements caching logic.

# Cache Hit vs Cache Miss
- This is a very important concept to add to your notes.
- Cache hit
Data exists in the cache:

Client
  ↓
Backend
  ↓
Redis
  ↓
Data found ✅
  ↓
Response

- The backend doesn't need to query the database.

- Cache miss

- Data doesn't exist in the cache:

Client
  ↓
Backend
  ↓
Redis
  ↓
Not found ❌
  ↓
Database
  ↓
Backend
  ↓
Redis ← store data
  ↓
Client

This is commonly called cache-aside / lazy loading.

For example:
```javascript
const cachedBlog = await redis.get(`blog:${id}`);
if (cachedBlog) {
  return JSON.parse(cachedBlog); // cache hit
}

const blog = await db.blog.findUnique({
  where: { id }
});

await redis.set(
  `blog:${id}`,
  JSON.stringify(blog),
  { EX: 3600 }
);

return blog;
```

# What is redis?
1. Redis is an open-source, in-memory data store that supports multiple data structures and can be used as a database, cache, message broker, and for other use cases.

2. In redis data is stored in ram that's why retrieving the data from ram is much faster than retreiving the data from databse disk.

3. In redis we store the data in the form of key - vlaue pair. The key is always string but value can be of any data type like string, set, sorted set, list, hash, streams etc. 
- Redis's basic data values are binary-safe strings (byte sequences), and Redis builds higher-level data structures from them. However, some structures also have non-string metadata such as scores and stream IDs

Thre redis dataypes are :
1. String: In this value is string. we can store string as set user:1 "kartik"
2. List: In this we store the data as the ordered list like lpush jobs "{name:kartik, id:23}".
3. Set: In this we can store collection of elements and each elem should be unique. like SADD notification:1 "hi"
4. Hash: IN this we can store objects as value. Like HSET user:1 name "kartik" HSET user:1 id "23"
5. Sorted set: In this we store the elements which have some weight or score. ZADD leaderboard 100 "Kartik"
6. Streams: append-only sequence of events/messages.
