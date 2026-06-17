# 📋 System Design Quick-Revision Cheatsheet

One page: the framework, the building blocks, the numbers, and the trade-offs.

## 🧭 The framework (use it every time)
1. **Clarify requirements** (5 min) — functional + non-functional (scale, latency, availability, consistency). Ask, don't assume.
2. **Estimate** (3 min) — users, QPS (reads vs writes), storage, bandwidth. Back-of-envelope.
3. **API + data model** (5 min) — the key endpoints and the core entities.
4. **High-level design** (10 min) — boxes & arrows: client → LB → service → DB/cache/queue.
5. **Deep dive** (10 min) — pick the interesting part and go deep (the data store, the hot path).
6. **Scale & harden** (10 min) — find bottlenecks; add caching, replicas, sharding, queues; discuss failure modes, monitoring, cost.
7. **Wrap up** (2 min) — recap trade-offs and what you'd do with more time.

## 🔢 Numbers worth knowing (back-of-envelope)
| Thing | Rough number |
|-------|--------------|
| L1 cache ref | ~1 ns |
| Main memory ref | ~100 ns |
| SSD random read | ~100 µs |
| Network round trip (same DC) | ~0.5 ms |
| Disk (HDD) seek | ~10 ms |
| Round trip across continents | ~150 ms |
| Reads:writes (typical web) | ~100:1 to 1000:1 |
| 1 day | ~86,400 s (~10^5) |
| Char / number | ~1 / ~4–8 bytes |

**QPS shortcut:** `daily requests / 86,400`. 1M/day ≈ ~12 QPS average; multiply by ~2–3 for peak.

## 🧱 Building blocks (one-liners)
| Block | What it's for | Watch out for |
|-------|---------------|---------------|
| **Load balancer** | spread traffic across servers; health checks | becomes a SPOF (run redundant) |
| **Reverse proxy / API gateway** | TLS, auth, routing, rate limiting | extra hop/latency |
| **Cache** (Redis/Memcached) | fast reads of hot data | invalidation, staleness |
| **CDN** | serve static/edge content close to users | cache-busting, cost |
| **SQL DB** | relational, ACID, joins | scaling writes is hard |
| **NoSQL** | scale, flexible schema, high write | weaker consistency, no joins |
| **Replication** | read scaling + HA | replication lag (stale reads) |
| **Sharding** | scale writes/storage | hot shards, cross-shard queries |
| **Message queue** (Kafka/SQS) | decouple, buffer, async | ordering, duplicates, backpressure |
| **Object storage** (S3) | files, blobs, backups | not for low-latency lookups |
| **Search index** (Elasticsearch) | full-text/secondary lookups | eventual consistency with source |

## ⚖️ The big trade-offs
- **CAP:** under a network partition you choose **Consistency** *or* **Availability**. Most web systems pick AP + eventual consistency; money/inventory leans CP.
- **SQL vs NoSQL:** relational+transactions+joins → SQL. Huge scale, simple access by key, flexible schema → NoSQL.
- **Strong vs eventual consistency:** strong = correct but slower/less available; eventual = fast/available but can read stale.
- **Vertical vs horizontal scaling:** bigger box (simple, limited) vs more boxes (complex, near-unlimited). Cloud favours horizontal.
- **Sync vs async:** sync = simple, user waits; async (queue) = resilient, scalable, eventual.
- **Latency vs throughput:** optimise for one and you often trade the other.

## ♻️ Scaling patterns (apply when you hit a bottleneck)
- **Read-heavy?** → add **caching** + **read replicas** + a **CDN**.
- **Write-heavy?** → **shard** the data; **queue** + batch writes; consider NoSQL.
- **Hot key / celebrity problem?** → dedicated cache, replication, fan-out on write vs read.
- **Spiky traffic?** → **autoscaling** + **queues** to absorb bursts.
- **Avoid SPOFs** → redundancy in every tier, multi-AZ.
- **Idempotency** → make writes safe to retry (idempotency keys) for at-least-once delivery.

## 🛡️ Reliability checklist (the SRE lens — say these!)
- Redundancy + **multi-AZ**; no single point of failure.
- **Health checks**, timeouts, **retries with backoff + jitter**, **circuit breakers**.
- **Rate limiting** & load shedding to protect the system.
- **Observability**: metrics (RED/USE), logs, traces, alerting on symptoms.
- **Backups + tested restores**; a disaster-recovery plan (RPO/RTO).
- **SLOs + error budgets** to make reliability measurable.

---

## ⭐ Found this useful?
Please **star** ⭐, **fork** 🍴, and **share** 🔗 this repo on LinkedIn. See [CONTRIBUTING.md](CONTRIBUTING.md).

Made by **Shubham Sharma** · [GitHub](https://github.com/shubhs248) · [LinkedIn](https://www.linkedin.com/in/shubhs248)
