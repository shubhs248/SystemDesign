# 🤝 Contributing

Thanks for thinking about helping out! This is a learning project, so contributions of every size are welcome — even fixing a typo.

If this repo helped you, the easiest way to support it is to **star** ⭐ it, **fork** 🍴 it, and **share** 🔗 it on LinkedIn so others can find it too.

## Ways you can help

- **Fix something** — a typo, a broken link, or a number that's wrong.
- **Add a scenario** — a new design prompt with a worked solution (classic or DevOps/infra flavoured).
- **Improve a solution** — add a missing trade-off, failure mode, or a clearer diagram.
- **Improve the wording** — explanations should be plain and interview-ready.

## Style for new scenarios

Keep the established shape:

- A **prompt file** (`scenario-*.md`) with: the problem, functional + non-functional requirements, a scale hint, and a "design it yourself first" nudge.
- A **solution file** in `solutions/` with: requirements recap, estimates, API/data model, a high-level diagram (Mermaid + an ASCII fallback), a deep dive, how it scales, failure modes, and trade-offs.
- Use **Mermaid** for diagrams (renders on GitHub) and keep an ASCII version too.
- Drive the design from **requirements**, and always name **trade-offs** — that's the skill being taught.

## How to contribute (step by step)

1. **Fork** this repo to your own GitHub account.
2. **Clone** your fork:
   ```bash
   git clone https://github.com/<your-username>/system-design-practice-lab.git
   cd system-design-practice-lab
   ```
3. **Create a branch**:
   ```bash
   git switch -c add-chat-system-scenario
   ```
4. **Make your change** and proof-read it.
5. **Commit** and **push**, then open a **Pull Request**.

## Checklist before you open a PR

- [ ] The prompt states clear functional + non-functional requirements.
- [ ] The solution clarifies requirements, estimates scale, and names trade-offs.
- [ ] Diagrams render (Mermaid) and have an ASCII fallback.
- [ ] Plain, simple English.
- [ ] If you added a new part, you linked it from the main `README.md`.

## Code of conduct

Be kind and helpful. Assume good intent and keep feedback friendly.

---

Made by **Shubham Sharma** · [GitHub](https://github.com/shubhs248) · [LinkedIn](https://www.linkedin.com/in/shubhs248)
