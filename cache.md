# Cache

## What is cache?

- Cache is a data structure that stores a copy of data in a faster memory (RAM) to avoid expensive disk I/O operations.

## Need to know:

- Need to decide when and how to udpate or remove the outdated data from cache
- Cache hit: means data found in cache, cache miss: means data not found in cache (can be found via `X-Cache` header)
- TTL (Time To Live): Defines how long data stays in the cache before expiring

## Types of cache:

- Browser cache:
  - Store the web contents on user local machine (When user revisiting the site, user can fetch from cache rather than fetching from server again)
  - Use the browser `Cache-Control` header to control the cache (eg: `Cache-Control: max-age=3600`) [how long for the cache to be valid]

- CDN cache:
  - Store the data in the CDN server (eg: Cloudflare, Akamai, etc) [Find the nearest server to the user]
  - Pull & push based CDN
  - Reduce the load of original server
  - Reduce the latency + High availability + Security considerations !!!

- Database cache:
  - Store whether the result of that query has been stored in the cache layer (eg: Redis, Memcached, etc)

- Server cache:
  - Prevent expensive server side operations, (eg: server query the database directly if no cache found, otherwise, server will fetch from cache directly, whihc which is faster) [Server -> (Cache) -> Database]
  
- Eviction policy for database and server cache:
  - LRU (Least Recently Used): remove the least recently used item
  - LFU (Least Frequently Used): remove the least frequently used item
  - FIFO (First In First Out): remove the first item


## Technologies:

- Redis: in-memory data structure store, used as a database, cache, message broker
- CDN (Content Delivery Network): (eg: AWS CloudFront, Cloudflare), cache static content (eg: images, videos, js, css html files) [geographically distributed network of servers that work together to deliver web conten]


## Reverse proxy:

- Reverse proxy: its a type of proxy server, which hide the server side identity and proxy the request to the backend server, client side talk to the proxy server, which is not directly request to the backend server, which protects the server from direct access
- Load balancers: reverse proxy to distribute the traffic to multiple servers (to prevent one server overloaded issue)
- Nginx: open source web server, load balancer, reverse proxy, caching server
