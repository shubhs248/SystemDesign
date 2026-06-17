# Scenario 3 — Design a Highly Available, Scalable Web Application

**The prompt:** design the cloud infrastructure for a web application that must stay up through failures and handle large, variable traffic — the classic "design a resilient, scalable deployment" infra question.

---

## 📋 Requirements to establish

**Functional**
- Serve a web app + API to users.
- Handle a relational data store and static assets.

**Non-functional**
- **High availability** — survive an instance failure *and* a whole availability-zone failure.
- **Scalable** — handle traffic spikes (e.g. 10× during a sale) automatically.
- **No single point of failure** in any tier.
- **Secure** and **cost-aware**; a **disaster-recovery** story.

## 🧠 Think about
- The standard **tiers**: DNS → LB → stateless app tier → database, plus cache, object storage, CDN.
- **Multi-AZ** (and when **multi-region**): what fails over, and how.
- **Autoscaling** the app tier — scale on what signal?
- Why the app tier should be **stateless** (where does session/state go?).
- **Database HA**: primary + standby replica, automated failover, read replicas.
- **DR**: RPO/RTO, backups, failover region.

---

## ✅ Now design it yourself, then compare
Spend ~20 minutes before reading [`solutions/scenario-3-ha-scalable-web-app.md`](solutions/scenario-3-ha-scalable-web-app.md).
