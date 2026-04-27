# Databases: SQL vs NoSQL

## SQL (Relational)

**Examples**: PostgreSQL, MySQL, SQLite

| Feature | Notes |
|---|---|
| Schema | Strict, predefined |
| Query language | SQL (joins, aggregations) |
| ACID transactions | ✅ Full support |
| Scaling | Vertical (scale up), read replicas |
| Use cases | Financial systems, ERP, anything requiring complex queries |

### SQL Indexing
- **B-tree index** — default, good for range queries and equality.
- **Hash index** — equality only, faster lookup, no range support.
- **Composite index** — index on multiple columns; column order matters.
- **Covering index** — index contains all columns needed by query.

```sql
-- Composite index: queries on (user_id, created_at) benefit from this
CREATE INDEX idx_user_created ON posts(user_id, created_at);
```

## NoSQL

| Type | Examples | Best For |
|---|---|---|
| Key-Value | Redis, DynamoDB | Session store, caching |
| Document | MongoDB, Firestore | Semi-structured data, catalogs |
| Wide-Column | Cassandra, HBase | Time-series, write-heavy workloads |
| Graph | Neo4j | Social networks, recommendation |

## CAP Theorem

A distributed system can guarantee **at most 2 of 3**:

| Property | Meaning |
|---|---|
| **C**onsistency | Every read receives the latest write |
| **A**vailability | Every request receives a response |
| **P**artition Tolerance | System works despite network partitions |

- **CP** systems: HBase, Zookeeper (consistent but may be unavailable during partition)
- **AP** systems: Cassandra, CouchDB (available but may return stale data)
- SQL databases are typically **CA** (not distributed by default)

## Replication

- **Leader-Follower**: One primary handles writes; replicas handle reads.
- **Multi-Leader**: Multiple nodes accept writes; risk of conflicts.
- **Leaderless**: Any node can accept writes (Dynamo-style, e.g., Cassandra).

## Sharding (Horizontal Partitioning)

| Strategy | How | Trade-offs |
|---|---|---|
| Range-based | Partition by ID range | Risk of hotspots |
| Hash-based | `shard = hash(key) % n` | Uniform distribution; resharding is costly |
| Directory-based | Lookup table maps key → shard | Flexible; lookup table is a bottleneck |

## When to Choose What

| Use SQL when… | Use NoSQL when… |
|---|---|
| Data is relational & structured | Data is unstructured or schema-less |
| Need complex joins / aggregations | Need horizontal scalability |
| Need strong ACID guarantees | Need high write throughput |
| Reads >> Writes | Writes >> Reads |
