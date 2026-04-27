# System Design Interview Framework

## Step-by-Step Approach (45-minute interview)

| Time | Step |
|---|---|
| 0–5 min | Clarify requirements & constraints |
| 5–10 min | Estimate scale (users, QPS, storage) |
| 10–15 min | Define APIs and data models |
| 15–30 min | High-level design (draw boxes & arrows) |
| 30–40 min | Deep dive into components |
| 40–45 min | Identify bottlenecks & trade-offs |

## Step 1 — Clarify Requirements

Ask before designing:
- What are the core features? (MVP only)
- Read-heavy or write-heavy?
- How many users? Daily active users (DAU)?
- Expected latency SLAs?
- Consistency requirements (strong vs eventual)?
- Availability requirements (99.9% = 8.7 h/yr downtime)?

## Step 2 — Estimate Scale

| Metric | Rule of Thumb |
|---|---|
| 1 million DAU × 10 requests/day | = 100 QPS |
| 1 KB per request × 100 QPS | = 100 KB/s = ~8 GB/day |
| 1 server handles | ~1,000–10,000 QPS (depends on type) |

```
QPS = (DAU × actions_per_day) / 86,400 seconds
Peak QPS ≈ 2–3× average QPS
Storage per year = daily_writes × record_size × 365
```

## Step 3 — API Design

Define clear REST endpoints or RPC methods:
```
POST /api/v1/tweets          → create tweet
GET  /api/v1/tweets/{id}     → get tweet
GET  /api/v1/feed            → get home timeline
```

## Step 4 — High-Level Design

Key components to consider:
- **Client** (mobile / web)
- **CDN** — static assets, caching
- **Load Balancer** — distribute traffic, SSL termination
- **API Gateway** — rate limiting, auth, routing
- **Application Servers** — stateless, horizontally scalable
- **Cache** (Redis / Memcached) — read throughput
- **Database** (SQL / NoSQL) — persistent storage
- **Message Queue** (Kafka / RabbitMQ) — async processing
- **Object Storage** (S3) — images, videos
- **Search** (Elasticsearch) — full-text search

## Step 5 — Deep Dive Topics

- **Database schema** and indexing strategy
- **Caching strategy** (cache-aside, write-through, TTL)
- **Sharding** (horizontal partitioning by user_id, hash, range)
- **Replication** (leader-follower, read replicas)
- **Consistency** model (CAP theorem trade-offs)

## Step 6 — Bottlenecks & Trade-offs

Always discuss:
- Single points of failure and how to eliminate them
- Trade-off between consistency and availability
- How to handle hotspot / celebrity problem
- Cost vs performance trade-offs
