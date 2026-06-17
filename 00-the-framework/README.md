# Part 0 — The Framework (how to answer ANY system design question)

## 🎯 Goal
Give you a **repeatable method** so you never freeze on a blank whiteboard. The interviewer isn't checking whether you've memorised Twitter's architecture — they're checking whether you can **reason about trade-offs under ambiguity**. A clear method makes that obvious.

---

## 🧠 The mindset
- **It's a conversation, not a monologue.** Think out loud, check in, adjust.
- **There is no single right answer.** There are good trade-offs and bad ones. Your job is to *name* the trade-offs.
- **Requirements drive design.** Never start listing technologies before you know what you're building and for how many users.
- **Start simple, then scale.** A working simple design that you then evolve beats a "web-scale" design you can't justify.

---

## 🪜 The 7 steps

### 1. Clarify requirements (≈5 min) — *don't skip this*
Split into two kinds:

- **Functional** — what the system *does*. ("Users shorten a URL and get redirected." "Users post and read messages.")
- **Non-functional** — the *qualities*: scale (how many users/requests?), latency (how fast?), availability (how much downtime is OK?), consistency (must reads be immediately correct?), durability, security, cost.

Ask questions like: *How many users? Read-heavy or write-heavy? How fast must it respond? Is stale data OK for a few seconds? Global or single region?*

> 🟢 **Why it matters:** the same prompt has wildly different designs at 1k users vs 1B users. Clarifying scope is half the score.

### 2. Estimate the scale (≈3 min)
Back-of-envelope numbers turn vague prompts into concrete constraints:

- **Traffic:** daily active users → requests/day → **QPS** (`requests ÷ 86,400`), and the **read:write ratio** (often 100:1+).
- **Storage:** items/day × bytes/item × retention.
- **Bandwidth:** QPS × response size.

You don't need precision — you need the **order of magnitude** (is it 10 QPS or 100,000 QPS?), because that decides whether you need caching, sharding, queues, etc.

### 3. Define the API and data model (≈5 min)
- **API:** the few key operations (`POST /shorten`, `GET /{code}`). Keeps the design grounded.
- **Data model:** the core entities and their relationships, and the **access patterns** (how will you read/write this?). The access pattern often decides SQL vs NoSQL.

### 4. High-level design (≈10 min)
Draw the boxes and arrows. A typical web system:

```
Client → DNS → Load Balancer → App/Service tier → Database
                                   │
                                   ├── Cache (hot reads)
                                   ├── Queue (async work)
                                   └── Object storage / CDN (files, static)
```

Walk the request path end to end. Keep it simple first — you'll add components as you scale in step 6.

### 5. Deep dive (≈10 min)
Pick the **most interesting / hardest** part and go deep — usually the data store, the hot path, or the tricky algorithm. This is where senior signal shows: how you shard, how you keep the cache consistent, how you generate unique IDs, how you guarantee ordering.

> Let the interviewer steer here. If they poke at a component, follow them.

### 6. Identify bottlenecks, then scale & harden (≈10 min)
Ask: *"Where does this fall over as traffic grows?"* and fix it with the right pattern:

- **Read-heavy** → cache + read replicas + CDN.
- **Write-heavy** → shard + queue/batch writes + maybe NoSQL.
- **Single points of failure** → redundancy, multi-AZ.
- **Spiky load** → autoscaling + queues to absorb bursts.

Then put on the **SRE hat**: timeouts, retries with backoff, circuit breakers, rate limiting, **observability** (metrics/logs/traces/alerts), backups + DR, and **cost**.

### 7. Wrap up (≈2 min)
Recap the design in two sentences, restate the **main trade-offs** you made, and mention **what you'd improve with more time**. This leaves a strong, structured impression.

---

## ⏱️ Time budget (for a ~45-min round)
| Step | Minutes |
|------|---------|
| Clarify requirements | 5 |
| Estimate scale | 3 |
| API + data model | 5 |
| High-level design | 10 |
| Deep dive | 10 |
| Scale & harden | 10 |
| Wrap up | 2 |

## 🚩 Common mistakes (avoid these)
- **Jumping to "I'd use Kafka and Cassandra"** before clarifying requirements.
- **Designing for a billion users** when the prompt implies thousands (over-engineering).
- **Silence** — not narrating your thinking. The interviewer can't read your mind.
- **No trade-offs** — presenting choices as obviously correct instead of "X vs Y because…".
- **Ignoring failure** — a design that only works on the happy path.
- **Forgetting the operational side** — no monitoring, no scaling story, no cost awareness (especially bad for a DevOps/SRE candidate).

## 🗣️ Phrases that signal seniority
- *"Let me clarify the requirements before I design anything."*
- *"At this scale the bottleneck will be writes, so…"*
- *"The trade-off here is consistency vs availability; I'd lean … because …"*
- *"To avoid a single point of failure, I'd run this redundant across AZs."*
- *"I'd alert on the symptom (error rate / latency), not the cause (CPU)."*

➡️ Next: learn the pieces you'll combine — [Part 1 — Building Blocks](../01-building-blocks/README.md).

---

## ⭐ Found this useful?
Please **star** ⭐, **fork** 🍴, and **share** 🔗 this repo on LinkedIn. See [CONTRIBUTING.md](../CONTRIBUTING.md).

Made by **Shubham Sharma** · [GitHub](https://github.com/shubhs248) · [LinkedIn](https://www.linkedin.com/in/shubhs248)
