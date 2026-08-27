# 🧠 Agentic AI Explained

A short-form video course on the Data and AI skills moving fastest right now: **model routing, agent governance, guardrails, memory, and running agents in production** on Databricks.

Every lesson pairs a short video with a full written guide in this repo — the concept explained end to end, a lab you run yourself, and a challenge that goes past what the video shows. The videos are the fast version; **these guides are the complete one.** Each YouTube short points back here, so every guide is written to stand on its own.

<p align="center">
  <img src="./assets/unity-ai-gateway.gif" alt="Animated diagram: every request from users, apps, and agents passes through Unity AI Gateway before reaching models, agents, MCP servers, and tools" width="620">
</p>

New lessons drop regularly on the Databricks YouTube channel — ⭐ **star this repo** and subscribe to follow along.

Written for software developers, solutions architects, and data scientists. The guides do not simplify away technical detail.

## 🚀 How to follow along

[Omnigent](https://omnigent.ai) is open source, so most labs cost nothing to run. The Databricks portions run on [Databricks Free Edition](https://www.databricks.com/learn/free-edition) wherever the feature is available there. Where a capability needs a paid workspace or sits in preview, the guide says so.

## 📚 The course

Each lesson links to a single guide. Read the guide, run the lab, take the challenge.

| # | Lesson | What you learn to do |
|---|---|---|
| 1 | [🧭 **Smart Routing**](./01-smart-routing.md) | Send every task to the lowest-cost model that can handle it, with the Omnigent intelligent model router |
| 2 | [🛡️ **Agent Policies & Budgets**](./02-agent-policies.md) | Cap agent spend, limit repeated tool calls, and gate risky actions behind human approval |
| 3 | [🌐 **Unity AI Gateway**](./03-unity-ai-gateway.md) | Put several model providers behind one endpoint and see spend per model, per user, per tool |

🔜 **Lessons 4–10 coming soon** — agent memory, context curation, guardrails, multi-agent patterns, evaluation and tracing, and governing agents at scale.

## 🧱 The control layer

A model on its own is not a production system. An agent with real tools and a real budget needs a runtime layer that decides:

- 🧭 which model handles each task
- 🛡️ what the agent is allowed to do
- ✋ when a human has to approve an action
- 💸 how much a user, team, agent, or application can spend
- 🔎 how every model call and tool call is logged and traced

**Lessons 1 through 3 build that layer.** Lessons 4 through 6 give the agent memory on top of it. Lessons 7 through 10 govern the whole thing.

## 👋 Follow the course

- ▶️ YouTube: <!-- GAP: playlist URL -->
- 💼 LinkedIn: [linkedin.com/in/semaan](https://www.linkedin.com/in/semaan/)
- 📸 Instagram: [@viktoria.semaan](https://www.instagram.com/viktoria.semaan/)

## 📝 Note

These guides are educational. Product interfaces and preview capabilities change, so check current Databricks and Omnigent documentation before using any example in production.

## ⚖️ License

[MIT](./LICENSE)
