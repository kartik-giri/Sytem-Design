# What is CDN?
- CDN stands for content delivery network.
- It is used to serve static components or pages like html,jpeg,png,mp4, pdf etc from edge servers of the CDN.
- The CDn caches the static component and pages and for time period stated in TTL and serves direclty to users if cache hits.
- With Blob storage, backend stores blob on blob storage and to serve those blobs fast we can use CDN which will cache the blobs and serve them direclty to users much faster.
User
  ↓
 CDN Edge
  ↓ cache MISS
 S3 / Object Storage
- CDN with Next js static pages. In this we can cache the static pages on CDN and serve the dynamic pages from EC2 -> Nginx -> next.js 
                    CDN
                     │
          ┌──────────┴──────────┐
          ↓                     ↓
    Public/cacheable        Dynamic
        content             content
          ↓                     ↓
      CDN cache          EC2 → Nginx → Next.js
- Edge servers are the server where CDN caches the components.
- Origin server is the server from where content is cached.This is your main web server (e.g., AWS S3).
The CDN fetches content from here if it’s not already cached at the edge server.
- GeoDNS -> CDN uses geoDNS to route users to the neareast edge servers. 

1. CDN = Is the geographically distributed caching/delivery layer that can cache and serve cacheable content closer to users.

# The CDN doesn't understand your Next.js code.
It basically sees:

Request:
GET /

Response:
HTTP 200
Cache-Control: ...
HTML...

and uses its cache rules/headers to determine whether it can cache that response.
