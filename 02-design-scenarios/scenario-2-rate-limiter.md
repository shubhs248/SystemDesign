# Scenario 2 — Design a Rate Limiter

**The prompt:** design a service/component that limits how many requests a client can make in a time window (e.g. "100 requests per minute per user/API key"), used to protect an API from abuse and overload.

---

## 📋 Requirements to establish

**Functional**
- Allow or reject a request based on a configurable limit (e.g. N per window per key).
- Return a clear signal when limited (HTTP 429 + `Retry-After`).
- Limits can vary by user/plan/endpoint.

**Non-functional**
- **Very low latency** — it sits on the hot path of every request.
- **Accurate enough** at scale, and works across **many servers** (distributed).
- Highly available; failure shouldn't take down the API.

## 🔢 Scale hint
Imagine a large API: hundreds of thousands of requests/second across many app servers and regions. The limiter must add minimal latency and share state across servers.

## 🧠 Think about
- Which **algorithm**? (fixed window, sliding window log, sliding window counter, token bucket, leaky bucket) — and their trade-offs.
- **Where** do you enforce it? (client, API gateway, per-service, sidecar)
- How do you share counters across servers? (a central store like **Redis**)
- What happens on a **burst** at a window boundary? What if the limiter store is **down** (fail open vs fail closed)?

---

## ✅ Now design it yourself, then compare
Spend ~20 minutes before reading [`solutions/scenario-2-rate-limiter.md`](solutions/scenario-2-rate-limiter.md).
