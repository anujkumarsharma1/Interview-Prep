# Scalability

## Vertical vs Horizontal Scaling

| | Vertical Scaling (Scale Up) | Horizontal Scaling (Scale Out) |
|---|---|---|
| How | Bigger machine (more CPU, RAM) | More machines |
| Limit | Hardware ceiling | Practically unlimited |
| Cost | Expensive (diminishing returns) | Commodity hardware |
| Complexity | Simple | Requires load balancing, coordination |
| Downtime | Usually requires restart | Rolling deployments possible |
| Use case | Databases (initially), legacy apps | Web/app servers, stateless services |

## Load Balancing

Distributes traffic across multiple servers.

**Algorithms:**
- **Round Robin** — requests distributed evenly in order
- **Least Connections** — route to server with fewest active connections
- **IP Hash** — same client always routed to same server (sticky sessions)
- **Weighted Round Robin** — more powerful servers get more traffic

**Examples:** AWS ALB/NLB, Nginx, HAProxy

## Stateless vs Stateful Services

- **Stateless**: No session state stored on server; any server can handle any request.  
  → Easy to scale horizontally.
- **Stateful**: Server holds client state (sessions).  
  → Use sticky sessions or move state to external store (Redis).

## Microservices vs Monolith

| | Monolith | Microservices |
|---|---|---|
| Deployment | Single deployable unit | Independent services |
| Scaling | Scale entire app | Scale individual services |
| Complexity | Simple initially | Complex (networking, observability) |
| Team size | Small teams | Large, distributed teams |
| Latency | In-process calls | Network calls |

## Message Queues

Decouple producers from consumers; enable async processing.

| Tool | Notes |
|---|---|
| Kafka | High-throughput, durable, log-based, replay messages |
| RabbitMQ | Flexible routing, lower latency, message acknowledgments |
| SQS (AWS) | Managed, at-least-once delivery |

**Use cases:** sending emails, processing images/videos, event streaming, fan-out.

## Content Delivery Networks (CDN)

- Cache static assets at edge locations close to users.
- Reduces origin server load and latency.
- **Examples:** Cloudflare, AWS CloudFront, Fastly

## Rate Limiting

Protect services from abuse / DDoS.

| Algorithm | Notes |
|---|---|
| Token Bucket | Allows bursts; tokens replenish at a fixed rate |
| Leaky Bucket | Smooths out bursts; requests processed at fixed rate |
| Fixed Window Counter | Simple; prone to boundary spikes |
| Sliding Window Log | Precise; high memory usage |
| Sliding Window Counter | Approximation; memory efficient |
