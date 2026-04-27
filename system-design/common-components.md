# Common System Components

Quick reference for common building blocks used in system design.

## Load Balancer

- Routes incoming traffic to available servers.
- Performs health checks; removes unhealthy instances.
- **Layer 4** (transport): routes by IP/TCP — fast, no app-level awareness.
- **Layer 7** (application): routes by URL, headers, cookies — flexible.

## API Gateway

Single entry point for clients. Responsibilities:
- Authentication & authorization
- Rate limiting
- SSL termination
- Request routing
- Response transformation
- **Examples:** AWS API Gateway, Kong, Nginx

## Message Queue / Event Bus

- Kafka: distributed log; high throughput; good for event streaming.
- RabbitMQ: flexible routing via exchanges; good for task queues.
- AWS SQS / SNS: managed; at-least-once delivery.

**Delivery guarantees:**
- At-most-once (fire and forget)
- At-least-once (retry on failure; consumer must be idempotent)
- Exactly-once (hard; Kafka transactions or deduplication)

## Object Storage (Blob Storage)

- Store large unstructured data (images, videos, backups).
- Examples: AWS S3, Google Cloud Storage, Azure Blob.
- Upload pattern: generate **pre-signed URL** → client uploads directly to storage.

## Search

- **Elasticsearch / OpenSearch**: inverted index for full-text search.
- Sync DB → search index via change-data-capture (CDC) or message queue.

## Distributed Cache

- Redis: rich data structures, pub/sub, persistence options.
- Memcached: simple, multi-threaded, no persistence.

## Distributed Lock

- Use Redis `SET NX PX` or Redlock algorithm.
- Use Zookeeper or etcd for stronger guarantees.

## Service Discovery

- Clients find services dynamically (no hardcoded IPs).
- **Examples:** Consul, Eureka, Kubernetes DNS.

## Monitoring & Observability

| Pillar | Tools |
|---|---|
| Metrics | Prometheus, Datadog, CloudWatch |
| Logs | ELK Stack (Elasticsearch + Logstash + Kibana), Splunk |
| Traces | Jaeger, Zipkin, AWS X-Ray |
| Alerts | PagerDuty, Opsgenie |
