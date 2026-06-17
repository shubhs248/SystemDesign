# Scenario 1 — Design a URL Shortener (like bit.ly / TinyURL)

**The prompt:** design a service that turns a long URL into a short one (e.g. `short.ly/abc123`) and redirects users from the short link to the original.

---

## 📋 Requirements to establish (clarify these out loud)

**Functional**
- Create a short URL from a long URL.
- Redirect a short URL to the original.
- (Optional) custom aliases, expiry, click analytics.

**Non-functional**
- **Very read-heavy** (redirects ≫ creations) — assume ~100:1.
- Redirects must be **fast** (low latency) and **highly available**.
- Short codes must be **unique** and ideally short.

## 🔢 Scale hint
Assume ~100M new URLs/month and ~10B redirects/month. Work out the write QPS, read QPS, and ~5 years of storage. (Don't peek at the solution's numbers yet.)

## 🧠 Think about
- How do you generate a **unique, short code**? (counter+base62? hash? random?)
- What database fits a simple **key → value** lookup at huge read scale?
- Where does **caching** help most?
- What's the **bottleneck**, and how do you scale it?

---

## ✅ Now design it yourself, then compare
Spend ~20 minutes on a whiteboard before reading [`solutions/scenario-1-url-shortener.md`](solutions/scenario-1-url-shortener.md).
