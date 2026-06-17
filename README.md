# 🏗️ System Design Practice Lab (for DevOps / SRE)

> A **clone-and-go** lab to get good at system design — the interview round that trips up even strong engineers. A repeatable **framework**, the **building blocks** explained in plain English with their trade-offs, and **worked design scenarios** — both the classic ones *and* the DevOps/infra ones (CI/CD, observability, HA) that you'll actually be asked.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

---

## 🎯 Why this repo?

System design interviews feel scary because they're open-ended — there's no single right answer and no command to run. But there *is* a method. This lab gives you:

- **A framework** you can apply to *any* prompt so you're never staring at a blank whiteboard.
- **The building blocks** (load balancers, caches, databases, queues, CDNs…) with the **trade-offs** interviewers probe.
- **Worked scenarios** — read the prompt, design it yourself, then compare with a full solution (diagram, components, scaling, failure modes).
- **A DevOps/SRE lens** throughout: reliability, scaling, observability, and cost — not just "draw boxes".

> Unlike the other labs, there's nothing to install. Your "tool" here is a whiteboard (or [excalidraw.com](https://excalidraw.com) / paper). The skill is **structured thinking out loud**.

## 🧠 The one habit to build

Great system-design answers are **driven by requirements, not by listing technologies**. Always go: *clarify the problem → estimate the scale → sketch a simple design → then evolve it to meet the numbers, naming trade-offs out loud.* Reaching for "I'd use Kafka and Cassandra" before you know the requirements is the most common way to fail this round.

## 🗂️ What's inside

```
system-design-practice-lab/
├── README.md                       ← you are here
├── CHEATSHEET.md                   ← building blocks + numbers to know + the framework
├── CONTRIBUTING.md
├── INTERVIEW-QUESTIONS.md          ← concept Q&A interviewers actually ask
├── 00-the-framework/               ← how to approach ANY system design question
│   └── README.md
├── 01-building-blocks/             ← LB, cache, DB, sharding, queues, CDN, CAP, scaling
│   └── README.md
├── 02-design-scenarios/            ← classic prompts (with worked solutions)
│   ├── README.md
│   ├── scenario-1-url-shortener.md
│   ├── scenario-2-rate-limiter.md
│   ├── scenario-3-notification-system.md
│   └── solutions/
└── 03-devops-infra-design/         ← the DevOps/SRE-flavoured prompts (your differentiator)
    ├── README.md
    ├── scenario-1-cicd-pipeline.md
    ├── scenario-2-observability-platform.md
    ├── scenario-3-ha-scalable-web-app.md
    └── solutions/
```

## 🚀 Quick start

```bash
git clone https://github.com/shubhs248/system-design-practice-lab.git
cd system-design-practice-lab

# 1. Learn the method
cat 00-the-framework/README.md

# 2. Skim the building blocks
cat 01-building-blocks/README.md

# 3. Pick a scenario, design it on a whiteboard FIRST, then read the solution
cat 02-design-scenarios/scenario-1-url-shortener.md
```

## 🧭 Suggested path (about 3 hours, spread it out)

| # | Part | What you get | Time |
|---|------|--------------|------|
| 0 | [The Framework](00-the-framework/README.md) | a repeatable way to answer any prompt | 25 min |
| 1 | [Building Blocks](01-building-blocks/README.md) | the components + trade-offs you'll combine | 45 min |
| 2 | [Design Scenarios](02-design-scenarios/README.md) | URL shortener, rate limiter, notifications | 60 min |
| 3 | [DevOps Infra Design](03-devops-infra-design/README.md) | CI/CD, observability, HA web app | 60 min |

## 📝 How each scenario works

1. Read the prompt and the **requirements**.
2. **Design it yourself first** — on paper/whiteboard, out loud, for ~20 minutes. *This is the practice.*
3. Then open the matching file in `solutions/` and compare: did you clarify requirements, estimate scale, handle the data model, scale the bottlenecks, and discuss failure modes?
4. Re-do it a few days later — fluency comes from repetition.

---

## 🎤 Prepping for an interview?

Open **[INTERVIEW-QUESTIONS.md](INTERVIEW-QUESTIONS.md)** — the conceptual questions that pepper a design round (CAP, SQL vs NoSQL, caching strategies, idempotency, "how would you scale this?"), in plain English with short answers you can say out loud.

---

## ⭐ Found this useful?

- **Star** ⭐ the repo so more people discover it.
- **Fork** 🍴 it and practise on your own copy.
- **Share** 🔗 it on LinkedIn and tag me — I would love to see your progress.
- **Contribute** 🤝 a new scenario or fix. See [CONTRIBUTING.md](CONTRIBUTING.md).

## 👋 About the author

Made with care by **Shubham Sharma**.

- GitHub: [github.com/shubhs248](https://github.com/shubhs248)
- LinkedIn: [linkedin.com/in/shubhs248](https://www.linkedin.com/in/shubhs248)

## 📜 License

MIT — free to use, fork, teach with, and share. A star ⭐ or a tag on LinkedIn is always appreciated!
