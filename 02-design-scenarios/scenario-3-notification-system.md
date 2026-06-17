# Scenario 3 — Design a Notification System

**The prompt:** design a system that sends notifications to users across multiple channels — **email, SMS, and push** — triggered by events from other services (e.g. "order shipped", "password reset").

---

## 📋 Requirements to establish

**Functional**
- Other services trigger a notification (one event → one or more channels).
- Support email, SMS, push (extensible to more).
- Respect user **preferences** (which channels, opt-outs).
- (Optional) templating, scheduling, delivery status.

**Non-functional**
- **High throughput**, bursty (a marketing blast or an outage can spike volume).
- **Reliable** — don't lose notifications; retry transient failures.
- **Async** — the triggering service shouldn't wait for delivery.
- Avoid **duplicate** sends.

## 🔢 Scale hint
Assume tens of millions of notifications/day with large spikes. Third-party providers (SES, Twilio, FCM) have their own rate limits and can fail.

## 🧠 Think about
- Why is a **message queue** the heart of this design?
- How do you **fan out** one event to multiple channels?
- How do you handle a **provider being down** or rate-limiting you? (retries, backoff, DLQ)
- How do you avoid **duplicate** notifications? (idempotency)
- Where do **user preferences** and **templates** live?

---

## ✅ Now design it yourself, then compare
Spend ~20 minutes before reading [`solutions/scenario-3-notification-system.md`](solutions/scenario-3-notification-system.md).
