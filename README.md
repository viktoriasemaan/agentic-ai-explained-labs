# Agentic AI Explained

A short-form video course on the Data and AI skills moving fastest right now: model routing, agent governance, guardrails, memory, and running agents in production on Databricks.

Every lesson is a short video paired with a written guide here, a lab you run yourself, and a challenge that goes past what the video shows. The videos are the fast version. This repo is where you actually build it.

The full course lives in one playlist on the Databricks YouTube channel. New lessons drop regularly, so subscribe and stay tuned.

Written for software developers, solutions architects, and data scientists. The guides do not simplify away technical detail.

<p align="center">
  <img src="./assets/unity-ai-gateway.gif" alt="Animated diagram: every request from users, apps, and agents passes through Unity AI Gateway before reaching models, agents, MCP servers, and tools" width="620">
</p>

## How to follow along

Omnigent is open source and available at [omnigent.ai](https://omnigent.ai). The Databricks portions run on [Databricks Free Edition](https://www.databricks.com/learn/free-edition) wherever the feature is available there. Where a capability needs a paid workspace or sits in preview, the guide says so.

## The course

| # | Lesson | What you learn to do | Guide | Lab | Video |
|---|---|---|---|---|---|
| 1 | Smart Routing | Send every task to the lowest cost model that can handle it, with the Omnigent intelligent model router | [Read](./01-smart-routing.md) | [Lab](./01-smart-routing.md#your-lab) | <!-- GAP --> |
| 2 | Agent Policies and Budgets | Cap agent spend, limit repeated tool calls, and gate risky actions behind human approval | [Read](./02-agent-policies.md) | [Lab](./02-agent-policies.md#your-lab) | <!-- GAP --> |
| 3 | Unity AI Gateway | Put several model providers behind one endpoint and see spend per model, per user, per tool | [Read](./03-unity-ai-gateway.md) | [Lab](./03-unity-ai-gateway.md#your-lab) | <!-- GAP --> |
| 4 | Agent Memory | Give agents working, episodic, semantic, and procedural memory | Coming soon | Coming soon | Coming soon |
| 5 | Memory Scaling | Distill long histories into a knowledge store agents can retrieve from | Coming soon | Coming soon | Coming soon |
| 6 | Curating Agent Context | Build the context an agent sees from governed enterprise data | Coming soon | Coming soon | Coming soon |
| 7 | AI Guardrails | Run PII, unsafe content, and prompt injection checks on every call | Coming soon | Coming soon | Coming soon |
| 8 | Multi-Agent Patterns | Pick an architecture for agents that work together | Coming soon | Coming soon | Coming soon |
| 9 | Evaluation and Tracing | Measure whether an agent is actually getting better | Coming soon | Coming soon | Coming soon |
| 10 | Governing Agents at Scale | Bring agents, tools, and memory under Unity Catalog | Coming soon | Coming soon | Coming soon |

<!-- GAP: confirm lesson titles 4 through 10 and swap in the video URLs as each drops -->

## The control layer

A model on its own is not a production system. An agent with real tools and a real budget needs a runtime layer that decides:

- which model handles each task
- what the agent is allowed to do
- when a human has to approve an action
- how much a user, team, agent, or application can spend
- how every model call and tool call is logged and traced

Lessons 1 through 3 build that layer. Lessons 4 through 6 give the agent memory on top of it. Lessons 7 through 10 govern the whole thing.

## Follow the course

- YouTube: <!-- GAP: playlist URL -->
- LinkedIn: [linkedin.com/in/semaan](https://www.linkedin.com/in/semaan/)
- Instagram: [@viktoria.semaan](https://www.instagram.com/viktoria.semaan/)

## Note

These guides are educational. Product interfaces and preview capabilities change, so check current Databricks and Omnigent documentation before using any example in production.

## License

[MIT](./LICENSE)
