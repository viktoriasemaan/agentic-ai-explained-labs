# Agentic AI Explained

Welcome! **Agentic AI Explained** is a short-form course on the skills that separate an AI agent *demo* from an agent you can actually run in production: routing each task to the right model, controlling what an agent is allowed to do, capping its spend, governing every call, giving it memory, and measuring whether it is getting better.

**What you get out of it:** hands-on practice with cutting-edge, in-demand skills for building agentic systems — not slides you watch, but things you build and run yourself.

**How it works.** The full course is **10 short lessons**, and each one comes in two parts:

- a **short video** that shows the idea in action, and
- a **written module in this repo** that goes deeper — the concept explained end to end, a lab you run yourself, and a challenge that pushes past what the video shows.

The videos are the fast tour; the guides are where you actually build. Each YouTube short points back here, so every module stands on its own. **The first three lessons are live now**, with more dropping regularly.

<p align="center">
  <img src="./assets/unity-ai-gateway.gif" alt="Animated diagram: every request from users, apps, and agents passes through Unity AI Gateway before reaching models, agents, MCP servers, and tools" width="620">
</p>

## What you need

- **A Databricks workspace.** [Databricks Free Edition](https://www.databricks.com/learn/free-edition) is free and covers most of the course; where a feature needs a paid workspace or is in preview, the guide says so.
- **Omnigent** — the open-source [meta-harness](https://omnigent.ai) the labs are built on. It is free, runs the agents, routes the models, and applies the policies you'll experiment with. [Lesson 1](./01-smart-routing.md) explains exactly what it is; you do not need to know it in advance.
- **Comfort reading code.** The course is written for software developers, solutions architects, and data scientists, and the guides do not simplify away the technical detail.

No prior agent experience required — that is what the course is for.

## The course

Each lesson links to a single guide. Read the guide, run the lab, take the challenge.

| # | Lesson | What you learn to do |
|---|---|---|
| 1 | [Smart Routing](./01-smart-routing.md) | Send every task to the lowest-cost model that can handle it, with the Omnigent intelligent model router |
| 2 | [Agent Policies and Budgets](./02-agent-policies.md) | Cap agent spend, limit repeated tool calls, and gate risky actions behind human approval |
| 3 | [Unity AI Gateway](./03-unity-ai-gateway.md) | Put several model providers behind one endpoint and see spend per model, per user, per tool |

**Lessons 4–10 are coming soon** — agent memory, context curation, guardrails, multi-agent patterns, evaluation and tracing, and governing agents at scale.

## The control layer

A model on its own is not a production system. An agent with real tools and a real budget needs a runtime layer that decides:

- which model handles each task
- what the agent is allowed to do
- when a human has to approve an action
- how much a user, team, agent, or application can spend
- how every model call and tool call is logged and traced

Lessons 1 through 3 build that layer. Lessons 4 through 6 give the agent memory on top of it. Lessons 7 through 10 govern the whole thing.

## Follow the course

New lessons publish on the Databricks YouTube channel:

- **YouTube:** [Databricks](https://www.youtube.com/@Databricks)

<p align="center">
  <br>
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="./assets/databricks-logo-dark.png">
    <img src="./assets/databricks-logo-light.png" alt="Databricks" width="220">
  </picture>
  <br>
  <sub>The labs in this course run on Databricks.</sub>
</p>

## Note

These guides are educational. Product interfaces and preview capabilities change, so check current Databricks and Omnigent documentation before using any example in production.

## License

[MIT](./LICENSE)
