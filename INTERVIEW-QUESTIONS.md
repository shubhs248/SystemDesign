# 🎤 System Design — Interview Questions & Answers

Short, say-it-out-loud answers to the **conceptual** questions that pepper a design round. Pair these with the worked [scenarios](02-design-scenarios/README.md). Don't memorise word-for-word — understand the trade-off so you can reason live.

> Tip: almost every good answer ends with *"…the trade-off is X vs Y, and I'd choose based on the requirements."*

---

## 🧭 Approach & fundamentals

**Q: How do you approach a system design question you've never seen?**
Clarify requirements (functional + non-functional) → estimate scale → define API + data model → sketch a simple high-level design → deep-dive the hard part → find bottlenecks and scale/harden → recap trade-offs. Requirements drive the design; I don't start with technologies.

**Q: What are functional vs non-functional requirements?**
Functional = *what it does* (shorten a URL, send a notification). Non-functional = *the qualities*: scale, latency, availability, consistency, durability, security, cost. Non-functional requirements usually decide the architecture.

**Q: What's "back-of-the-envelope" estimation and why bother?**
Rough math (QPS = requests ÷ 86,400, storage = items × size × retention) to get the **order of magnitude**. It tells you whether you need caching, sharding, or queues — a design for 10 QPS is very different from 100k QPS.

**Q: Vertical vs horizontal scaling?**
Vertical = a bigger machine (simple, but a ceiling + SPOF). Horizontal = more machines behind a load balancer (near-unlimited, resilient, but adds complexity around state and coordination). Cloud systems favour horizontal.

---

## ⚖️ Consistency, CAP & databases

**Q: Explain the CAP theorem.**
Under a network **partition** you must choose **Consistency** (reads see the latest write, reject if unsure) or **Availability** (always answer, possibly stale). You can't have both during a partition. Most web apps choose AP + eventual consistency; money/inventory leans CP.

**Q: Strong vs eventual consistency?**
Strong = every read sees the latest write (correct, but slower / less available). Eventual = replicas converge over time (fast, available, but you can read stale data briefly). Pick per use case: balances → strong; like-counts/feeds → eventual is fine.

**Q: SQL vs NoSQL — when do you pick which?**
SQL for relationships, transactions (ACID), and ad-hoc queries/joins — but writes are hard to scale. NoSQL for massive scale, high write throughput, flexible schema, and simple access-by-key — at the cost of weaker consistency and no joins. Choose by your **access patterns**.

**Q: What is replication and what's the catch?**
Copying data to multiple nodes (often leader–follower). It scales **reads** and gives HA. The catch is **replication lag** → followers can serve **stale** reads.

**Q: What is sharding, and what can go wrong?**
Splitting data across nodes by a **shard key** to scale writes/storage. Pitfalls: **hot shards** from a bad key, and painful **cross-shard queries/joins**. Choose a key that distributes evenly and matches your main query.

---

## ⚡ Caching & performance

**Q: Why cache, and what's the hard part?**
Caching stores hot data in memory to cut latency and DB load — the biggest win for read-heavy systems. The hard parts are **invalidation** (avoiding stale data) and the **thundering herd** (many cache misses hitting the DB at once).

**Q: Cache-aside vs write-through vs write-back?**
Cache-aside: app reads cache, on miss loads DB and fills cache (most common). Write-through: write cache + DB together (consistent, slower). Write-back: write cache, flush to DB later (fast, risk of loss on crash).

**Q: What is a CDN and when do you use it?**
A network of edge servers that cache static/edge content near users → lower latency + less origin load. Use it for images, video, JS/CSS, and any cacheable read-heavy content.

---

## 📨 Async, queues & reliability

**Q: Why use a message queue?**
To **decouple** producers from consumers and process work **asynchronously**. It buffers spikes, adds resilience (retry failed work), and lets you scale consumers independently. Trade-off: eventual processing and added complexity (ordering, duplicates).

**Q: What does "at-least-once" delivery mean, and how do you cope?**
The same message may be delivered more than once. You cope by making consumers **idempotent** (processing it twice has the same effect as once), often via an **idempotency key**. True exactly-once delivery is generally impossible; aim for exactly-once *effect*.

**Q: What is idempotency and why does it matter?**
An operation you can safely repeat with the same result. It matters because networks retry — with idempotency keys, retried payments/notifications/writes don't double up.

**Q: How do you make a system resilient to failures?**
Redundancy + multi-AZ (no SPOF), health checks, timeouts, **retries with backoff + jitter**, **circuit breakers**, rate limiting/load shedding, dead-letter queues, and tested backups/DR.

**Q: What's a single point of failure and how do you remove it?**
Any component whose failure takes the whole system down. Remove it with redundancy in every tier (multiple instances/AZs, replicated DB with failover, redundant load balancers).

---

## 🛠️ DevOps / SRE flavour (your edge)

**Q: Rolling vs blue-green vs canary deployments?**
Rolling: replace instances gradually (cheap, brief mixed versions). Blue-green: full new version then switch traffic (instant switch/rollback, 2× resources). Canary: send a small % of traffic, watch metrics, ramp up (safest, needs good metrics/automation). Prod → canary/blue-green.

**Q: How do you roll back a bad deploy quickly?**
Immutable artifacts + declarative deploys → redeploy the previous known-good image/manifest (`kubectl rollout undo`, re-apply previous Helm release, or `git revert` under GitOps). Automate auto-rollback when canary metrics breach thresholds.

**Q: What is GitOps?**
Desired state lives in Git; a controller (Argo CD/Flux) continuously reconciles the cluster to match. Benefits: Git is the audit trail and rollback mechanism, and CI doesn't need cluster credentials (pull-based, more secure).

**Q: Metrics vs logs vs traces?**
Metrics = numbers over time (is it healthy? alert on these). Logs = discrete event records (what exactly happened?). Traces = a request's path across services (why is it slow / where's the time?). Together they're "observability".

**Q: Should you alert on CPU?**
Usually no — alert on **symptoms users feel** (error rate, latency, availability), not raw causes like CPU (high CPU can be harmless). Tie alerts to **SLOs/error budgets** to avoid alert fatigue.

**Q: What are SLI, SLO, and error budget?**
SLI = a measured signal (e.g. % successful requests). SLO = the target for it (e.g. 99.9%). Error budget = the allowed failure (the 0.1%). When the budget burns fast, you slow risky changes and focus on reliability — it makes reliability measurable.

**Q: How do you make a web app highly available?**
Run every tier across multiple AZs behind a load balancer with health checks, keep the app tier **stateless** with autoscaling, and run the database with a standby in another AZ + automated failover. No single point of failure anywhere.

**Q: How do you control telemetry/cloud cost in a design?**
Sample traces (tail-based), reduce/sample logs, keep metric **cardinality** low, use hot/warm/cold **retention tiers** + downsampling, autoscale down off-peak, use CDN to cut egress, and reserved capacity for steady baseline + spot for bursts.

---

## 🧠 Whiteboard prompts (practise out loud, 20 min each)

1. Design a **URL shortener** — focus on unique IDs and read scaling.
2. Design a **rate limiter** — pick an algorithm and make it work across servers.
3. Design a **notification system** — queues, fan-out, retries, idempotency.
4. Design a **CI/CD pipeline** for a containerised service — stages, safe deploys, rollback, security.
5. Design an **observability platform** — three pillars, ingest pipeline, cost/retention.
6. Design a **highly available, autoscaling web app** — multi-AZ, stateless tier, DB failover, DR.
7. Design a **distributed cache** / **news feed** / **chat app** — stretch goals to try after the above.

> For each: clarify → estimate → API/data model → high-level → deep-dive → scale & harden → trade-offs. If you can do that fluently, you'll do well.

---

## ⭐ Found this useful?
Please **star** ⭐, **fork** 🍴, and **share** 🔗 this repo on LinkedIn. See [CONTRIBUTING.md](CONTRIBUTING.md).

Made by **Shubham Sharma** · [GitHub](https://github.com/shubhs248) · [LinkedIn](https://www.linkedin.com/in/shubhs248)
