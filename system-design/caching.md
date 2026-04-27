# Caching Strategies

## Why Cache?

- Reduce database load
- Lower latency (memory vs disk)
- Handle traffic spikes

## Common Caching Technologies

| Tool | Type | Notes |
|---|---|---|
| Redis | In-memory, persistent | Supports rich data types (lists, sorted sets) |
| Memcached | In-memory only | Simple key-value, multi-threaded |
| CDN (CloudFront, Cloudflare) | Edge caching | Static assets, geographic distribution |
| Browser cache | Client-side | HTTP cache headers (ETag, Cache-Control) |

## Cache-Aside (Lazy Loading) — Most Common

```
Read:
  1. Check cache
  2. Cache HIT → return cached value
  3. Cache MISS → query DB, store in cache, return value

Write:
  1. Update DB
  2. Invalidate (delete) the cache entry
```
✅ Only caches data that is actually read  
❌ Cache miss causes extra latency; risk of stale data

## Write-Through

```
Write:
  1. Write to cache AND DB simultaneously
```
✅ Cache is always up to date  
❌ Extra write latency; caches data that may never be read

## Write-Behind (Write-Back)

```
Write:
  1. Write to cache immediately
  2. Async write to DB later
```
✅ Low write latency  
❌ Risk of data loss if cache crashes before DB write

## Cache Eviction Policies

| Policy | Description |
|---|---|
| **LRU** (Least Recently Used) | Evict the least recently accessed item (most common) |
| **LFU** (Least Frequently Used) | Evict the least accessed item overall |
| **FIFO** | Evict the oldest item |
| **TTL** (Time-to-Live) | Expire items after a fixed duration |

## Cache Problems

| Problem | Description | Solution |
|---|---|---|
| **Cache Stampede** | Many misses hit DB at once | Mutex lock or probabilistic early expiry |
| **Cache Penetration** | Querying for non-existent keys bypasses cache | Cache null results; use Bloom filter |
| **Cache Avalanche** | Many keys expire simultaneously | Randomize TTLs |
| **Hot Key** | Single key receives too many reads | Replicate hot keys across multiple cache nodes |

## Redis Data Structures

| Structure | Use Case |
|---|---|
| String | Simple key-value, counters |
| Hash | User profiles, settings |
| List | Recent activity, message queues |
| Set | Unique visitors, tags |
| Sorted Set (ZSet) | Leaderboards, rate limiting |
| Bitmap | Feature flags, presence |
