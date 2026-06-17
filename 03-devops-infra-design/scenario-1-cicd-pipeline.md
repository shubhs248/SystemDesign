# Scenario 1 — Design a CI/CD Pipeline

**The prompt:** design the end-to-end pipeline that takes a developer's code commit and safely gets it into production — for a team shipping a containerised microservice to Kubernetes many times a day.

---

## 📋 Requirements to establish

**Functional**
- On every commit/PR: build, test, and produce a deployable artifact (container image).
- Deploy to environments (dev → staging → prod) with appropriate gates.
- Safe **rollback** when a release goes bad.

**Non-functional**
- **Fast feedback** (developers shouldn't wait long for CI).
- **Safe** deploys (catch bad releases before/while they reach users).
- **Secure** (secrets, image scanning, least privilege).
- **Repeatable & automated** (no manual "click to deploy" steps).

## 🧠 Think about
- The **stages**: lint → build → test → scan → package → deploy. What runs on a PR vs on merge to main?
- **Deployment strategies**: rolling, blue-green, canary — trade-offs?
- How do you **roll back** quickly?
- Where do **secrets** live, and how do you keep the pipeline secure (image scanning, signed images, least-privilege runners)?
- How do you make CI **fast** (caching, parallelism)?
- **GitOps** (pull-based) vs push-based deploys?

---

## ✅ Now design it yourself, then compare
Spend ~20 minutes before reading [`solutions/scenario-1-cicd-pipeline.md`](solutions/scenario-1-cicd-pipeline.md).
