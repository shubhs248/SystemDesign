# 🖼️ Diagram Gallery

Rendered versions of every diagram in this lab in **light + dark** — handy for quick reference, slides, or **LinkedIn posts**. They adapt to your GitHub theme below; grab the files directly for use elsewhere.

- **PNG** (light + `-dark`) — drop straight into LinkedIn/slides.
- **SVG** (light + `-dark`) — crisp at any size for docs/websites.
- **Source** — editable Mermaid bodies in [`src/`](src). Re-render from the repo root with `render-diagrams.ps1`.

> The diagrams also render live (as Mermaid) inside the lab's section pages on GitHub. These image files are the brand-styled, theme-adaptive versions for use outside GitHub.

## 🎨 Colour legend
Every diagram uses the same scheme so component types are obvious at a glance:

| Colour | Means | Examples |
|--------|-------|----------|
| 🔵 Cyan | **Client / caller** | users, calling services |
| 🟢 Teal | **Edge / networking** | DNS, CDN, load balancer, API gateway |
| 🟢 Emerald | **Compute** | app servers, services, workers |
| 🟠 Amber | **Datastore** | databases, caches, object storage |
| 🔴 Rose | **Messaging** | queues, topics |
| ⚪ Slate | **External provider** | SES, Twilio, FCM, third-party APIs |

---

## The lab at a glance

### Learning path
<picture><source media="(prefers-color-scheme: dark)" srcset="01-learning-path-dark.png"><img alt="Learning path" src="01-learning-path.png"></picture>

### The 7-step framework
<picture><source media="(prefers-color-scheme: dark)" srcset="02-framework-7-steps-dark.png"><img alt="The 7-step framework" src="02-framework-7-steps.png"></picture>

### Anatomy of a typical web system
<picture><source media="(prefers-color-scheme: dark)" srcset="03-web-system-anatomy-dark.png"><img alt="Anatomy of a typical web system" src="03-web-system-anatomy.png"></picture>

---

## Classic design scenarios

### URL shortener
<picture><source media="(prefers-color-scheme: dark)" srcset="04-url-shortener-dark.png"><img alt="URL shortener architecture" src="04-url-shortener.png"></picture>

### Rate limiter
<picture><source media="(prefers-color-scheme: dark)" srcset="05-rate-limiter-dark.png"><img alt="Rate limiter architecture" src="05-rate-limiter.png"></picture>

### Notification system
<picture><source media="(prefers-color-scheme: dark)" srcset="06-notification-system-dark.png"><img alt="Notification system architecture" src="06-notification-system.png"></picture>

---

## DevOps / infra design

### CI/CD pipeline
<picture><source media="(prefers-color-scheme: dark)" srcset="07-cicd-pipeline-dark.png"><img alt="CI/CD pipeline" src="07-cicd-pipeline.png"></picture>

### Observability platform
<picture><source media="(prefers-color-scheme: dark)" srcset="08-observability-platform-dark.png"><img alt="Observability platform architecture" src="08-observability-platform.png"></picture>

### Highly available, scalable web app
<picture><source media="(prefers-color-scheme: dark)" srcset="09-ha-scalable-web-app-dark.png"><img alt="Highly available, scalable web app" src="09-ha-scalable-web-app.png"></picture>

---

## 🔄 How to re-render these

The source diagrams are plain-text [Mermaid](https://mermaid.js.org/) bodies in [`src/*.mmd`](src) (no theme — the brand teal light/dark themes are injected at render time). From the repo root:

```powershell
# renders every lab's diagrams in light + dark, PNG + SVG
powershell -NoProfile -ExecutionPolicy Bypass -File .\render-diagrams.ps1 -Force
```

No install needed — it uses the free [Kroki](https://kroki.io) service. You can also paste any `src/*.mmd` (plus a theme) into the [Mermaid Live Editor](https://mermaid.live).

---

Made by **Shubham Sharma** · [GitHub](https://github.com/shubhs248) · [LinkedIn](https://www.linkedin.com/in/shubhs248)
