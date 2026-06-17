# Scenario 2 — Design an Observability / Monitoring Platform

**The prompt:** design a centralised observability platform for a company running many microservices — so engineers can answer "is it healthy?", "what broke?", and "why is it slow?" and get alerted when things go wrong.

---

## 📋 Requirements to establish

**Functional**
- Collect **metrics**, **logs**, and **traces** from many services and hosts.
- Let engineers query/visualise them (dashboards) and **alert** on problems.
- Retain data for a sensible window.

**Non-functional**
- **High ingest volume** (telemetry can dwarf the app's own traffic).
- **Low query latency** for dashboards/investigation.
- **Reliable** — monitoring must stay up when the app is down (it's needed most then).
- **Cost-aware** — telemetry storage gets expensive fast.

## 🧠 Think about
- The **three pillars**: metrics vs logs vs traces — what each is for.
- The pipeline shape: **agent/collector → buffer → storage → query/visualise → alert**.
- Why a **time-series DB** for metrics vs a **search store** for logs vs a **trace store**.
- **Sampling** traces and controlling log volume to manage cost.
- **Retention tiers** (hot/warm/cold) and cardinality pitfalls.
- **Alerting**: on symptoms vs causes; avoiding alert fatigue; SLOs/error budgets.

---

## ✅ Now design it yourself, then compare
Spend ~20 minutes before reading [`solutions/scenario-2-observability-platform.md`](solutions/scenario-2-observability-platform.md).
