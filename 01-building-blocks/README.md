# Part 1 — Building Blocks

## 🎯 Goal
Understand the components you'll combine in every design — and, more importantly, the **trade-offs** of each. Interviewers don't reward naming a tool; they reward knowing *when and why* to use it.

> Read this once for understanding. In a real interview you won't explain each block in depth — you'll *use* them and justify your choices.

---

## ⚖️ The two ideas everything hangs on

### Scaling: vertical vs horizontal
- **Vertical (scale up)** — a bigger machine (more CPU/RAM). Simple, but there's a ceiling and it's a single point of failure.
- **Horizontal (scale out)** — more machines behind a load balancer. Near-unlimited and resilient, but adds complexity (state, coordination). **Cloud systems favour horizontal.**

### CAP theorem (say this correctly)
When there's a **network partition** (P — unavoidable in distributed systems), you must choose between:
- **C — Consistency:** every read sees the latest write (reject if unsure).
- **A — Availability:** every request gets an answer (possibly stale).

Most web systems choose **AP + eventual consistency** (be available, converge soon). Systems handling money/inventory lean **CP** (be correct, even if it means rejecting).

---

## 🌐 Traffic & networking

### DNS
Turns a name into an IP. Can also do basic routing (geo, weighted). First hop of any request.

### Load balancer (LB)
Spreads traffic across many servers and removes dead ones via **health checks**.
- **L4** (TCP) — fast, dumb. **L7** (HTTP) — can route by path/host, terminate TLS.
- Algorithms: round-robin, least-connections, IP-hash (sticky).
- ⚠️ The LB itself must be **redundant** or it's a single point of failure.

### Reverse proxy / API gateway
Single entry point that handles TLS, auth, routing, **rate limiting**, and request shaping. Trade-off: an extra hop.

### CDN (Content Delivery Network)
Caches static content (images, JS, video) at edge locations near users → lower latency + less origin load. Trade-off: cache invalidation and cost. Great for read-heavy static content.

---

## 💾 Storage & databases

### SQL (relational)
Tables, rows, **ACID** transactions, joins, strong consistency. Best when relationships and correctness matter (payments, orders).
- Scaling reads is easy (replicas); scaling **writes** is hard.

### NoSQL (key-value, document, wide-column, graph)
Flexible schema, horizontal scale, high write throughput. Best for huge scale and simple access patterns (by key).
- Trade-off: weaker consistency, limited joins, you design around **access patterns**.

> **SQL vs NoSQL one-liner:** relationships + transactions + ad-hoc queries → SQL; massive scale + simple key access + flexible schema → NoSQL.

### Replication
Copy data to multiple nodes.
- **Leader–follower:** writes to leader, reads from followers → scales **reads** and gives HA.
- ⚠️ **Replication lag** → followers can serve **stale** reads (eventual consistency).

### Sharding (partitioning)
Split data across nodes by a **shard key** (e.g. user_id) → scales **writes** and storage.
- ⚠️ Pitfalls: **hot shards** (bad key choice), and **cross-shard queries/joins** are painful. Choose the shard key for even distribution and your main access pattern.

### Object storage (e.g. S3)
Cheap, durable storage for files/blobs/backups over HTTP. Not for low-latency key lookups — pair with a DB that stores the metadata/pointer.

### Search index (e.g. Elasticsearch)
Full-text search and secondary lookups. Usually a **secondary** store kept in sync with the source of truth (eventually consistent).

---

## ⚡ Caching

Store hot data in fast memory (Redis/Memcached) to cut latency and DB load. The highest-leverage tool for read-heavy systems.

- **Where:** client, CDN, in front of the DB, or in the app.
- **Read strategy — cache-aside (most common):** app checks cache; on miss, reads DB and populates cache.
- **Write strategies:** write-through (write cache+DB together, consistent, slower) · write-back (write cache, flush later, fast, risk of loss) · write-around (write DB only, avoids caching cold data).
- **Eviction:** LRU/LFU/TTL.
- ⚠️ The hard parts: **invalidation** (stale data) and the **thundering herd** (many misses hit the DB at once → use locks / request coalescing).

---

## 📨 Asynchronous processing

### Message queue (SQS, RabbitMQ, Kafka)
Decouples producers from consumers. Producer drops a message and moves on; consumers process at their own pace.
- **Benefits:** smooths spikes (buffering), resilience (retry failed work), scalability (add consumers).
- **Delivery:** usually **at-least-once** → consumers must be **idempotent** (safe to process the same message twice).
- ⚠️ Consider ordering, duplicates, **dead-letter queues** for poison messages, and backpressure.

### Pub/Sub & streaming
One event delivered to many subscribers (fan-out). **Kafka** adds a durable, replayable log — great for event-driven architectures and analytics pipelines.

---

## 🛡️ Reliability patterns (the SRE lens)

| Pattern | What it does |
|---------|--------------|
| **Redundancy / multi-AZ** | no single point of failure |
| **Health checks** | LB stops sending traffic to dead instances |
| **Timeouts** | don't wait forever on a slow dependency |
| **Retries (backoff + jitter)** | survive transient failures without stampeding |
| **Circuit breaker** | stop hammering a failing dependency; fail fast |
| **Rate limiting / load shedding** | protect the system from overload |
| **Idempotency keys** | make retried writes safe (exactly-once *effect*) |
| **Bulkheads** | isolate failures so one part can't sink the whole ship |

## 📈 Observability (you'll be expected to mention this)
- **Metrics** — RED (Rate, Errors, Duration) for services; USE (Utilization, Saturation, Errors) for resources.
- **Logs** — structured, centralised.
- **Traces** — follow a request across services.
- **Alerts** — on **symptoms** (error rate, latency), not causes (CPU).

## 💡 How to use these in a design
You won't use all of them. The skill is: hit a bottleneck → reach for the *right* block → justify it.
- "Reads are 99% of traffic" → **cache + read replicas + CDN**.
- "Writes are the bottleneck" → **shard + queue**.
- "Can't lose data / must retry safely" → **idempotency + at-least-once queue + DLQ**.
- "Must stay up if a datacentre dies" → **multi-AZ redundancy**.

➡️ Now practise: [Part 2 — Design Scenarios](../02-design-scenarios/README.md).

---

## ⭐ Found this useful?
Please **star** ⭐, **fork** 🍴, and **share** 🔗 this repo on LinkedIn. See [CONTRIBUTING.md](../CONTRIBUTING.md).

Made by **Shubham Sharma** · [GitHub](https://github.com/shubhs248) · [LinkedIn](https://www.linkedin.com/in/shubhs248)
