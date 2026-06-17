# Part 2 — Design Scenarios (the classics)

## 🎯 Goal
Practise the framework on three classic prompts. These appear again and again, and each teaches a core idea: **storage + unique IDs** (URL shortener), **algorithms + counters** (rate limiter), and **async fan-out** (notifications).

## 📝 How to use each scenario
1. Open the `scenario-*.md` prompt. Read the requirements.
2. **Design it yourself first** — whiteboard/paper, out loud, ~20 minutes. Apply the [framework](../00-the-framework/README.md).
3. Then open the matching file in [`solutions/`](solutions) and compare.
4. Score yourself: did you clarify requirements, estimate scale, define the data model, scale the bottleneck, and discuss failure modes & trade-offs?

| # | Scenario | Core idea it teaches |
|---|----------|----------------------|
| 1 | [URL Shortener](scenario-1-url-shortener.md) | unique ID generation, read-heavy caching, KV storage |
| 2 | [Rate Limiter](scenario-2-rate-limiter.md) | algorithms, distributed counters, where to enforce |
| 3 | [Notification System](scenario-3-notification-system.md) | queues, fan-out, retries, idempotency |

➡️ Next, the DevOps-flavoured prompts: [Part 3 — DevOps Infra Design](../03-devops-infra-design/README.md).

---

## ⭐ Found this useful?
Please **star** ⭐, **fork** 🍴, and **share** 🔗 this repo on LinkedIn. See [CONTRIBUTING.md](../CONTRIBUTING.md).

Made by **Shubham Sharma** · [GitHub](https://github.com/shubhs248) · [LinkedIn](https://www.linkedin.com/in/shubhs248)
