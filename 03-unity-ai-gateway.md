# How do you serve multiple models behind one Databricks endpoint and track their spend?

*Last updated: August 27, 2026*

You create an endpoint in Unity AI Gateway and place several models behind it. Applications call the endpoint name, and the models underneath can be added, swapped, or rebalanced without any application change. Every request through the gateway is logged to Databricks system tables, so spend and usage are queryable per model, per user, and per tool from one place. You can query those tables directly in SQL, ask Genie in natural language, or have Genie build a dashboard.

**Watch the video:** <!-- GAP: video 3 URL -->

**Lesson 3 of 10** in the Agentic AI Explained series.

---

## What this solves

The more AI tools an organization adds, the harder one simple question becomes: how much are we spending, and on what.

A production environment ends up holding frontier models, open weight models, external providers, coding agents, custom agents, MCP servers, enterprise tools, and several teams calling all of it. Without a shared layer, each integration carries its own credentials, access rules, budgets, logs, routing logic, guardrails, and monitoring. Answering the spend question means assembling numbers from every one of them.

A second problem sits alongside it. Models change on a weekly cadence. An application with a model name hard-coded into it has to be edited every time a better option appears, and every application has to be edited separately.

Unity AI Gateway is a runtime control layer in front of models, agents, MCP servers, and tools. Access and spend get defined once in one control plane.

```mermaid
flowchart TD
    A[Users / Apps / Agents] --> B[Unity AI Gateway]
    B --> C[Models]
    B --> D[Tools and MCP servers]
    B -.-> E[(system tables)]
```

<!-- GAP: drop the AI Governance Explained animated GIF here, see assets/README.md -->

---

## Creating a multi-model endpoint

The endpoint is the stable name an application calls. What sits behind it is a configuration detail.

In the demo I created a single endpoint and placed three providers behind it: Gemini, Anthropic, and OpenAI.

| Layer | Changes how often | Who owns it |
|---|---|---|
| Endpoint name | Rarely | Platform team |
| Models behind the endpoint | Weekly or as needed | Platform team |
| Application code | Only on feature changes | Application team |

For the user this is completely seamless. They do not see which model is running underneath. When a new model is released, I update the endpoint, and nothing changes for anyone calling it.

This also gives you a comparison surface. With three providers behind one endpoint, requests distribute across them, and the usage data that comes back tells you which one performs better for your traffic.

---

## Testing the endpoint

I test in the AI Playground with a question simple enough that every model answers it correctly, such as the capital of a country. Running it several times shows the requests distributing across the models behind the endpoint.

The point of a trivial question here is that it isolates the routing behavior. Any variation you see is the endpoint distributing traffic, and none of it is the models disagreeing about the answer.

---

## Where does the usage data land?

Every request that passes through the gateway is logged to Databricks system tables. That is what turns spend from an estimate into a query.

```sql
SELECT
  event_time,
  service_type,
  service_name,
  endpoint_name,
  requester,
  usage.total_tokens AS total_tokens
FROM system.ai_gateway.usage
WHERE requester = current_user()
  AND event_time > now() - INTERVAL 7 DAYS
ORDER BY event_time DESC
LIMIT 50;
```

Verify the current schema in the Databricks documentation before depending on this query in production.

One operational detail worth knowing: ingestion is not immediate. Rows can take an hour or more to land, so a query run seconds after a request may return nothing. When you are demonstrating this, query a window that includes earlier activity.

---

## Asking Genie for the same answer

Because the usage data sits in tables, you do not have to write SQL to work with it. I ask Genie which models I used recently, and it returns the list. I can also ask Genie to build a custom dashboard for my team or for my own use.

The dashboard view gives the breakdown that matters for a budget conversation:

| Dimension | Question it answers |
|---|---|
| Per model | Which models are consuming the budget |
| Per user | Who is generating the traffic |
| Per tool or application | Which workload is responsible |
| Per endpoint | Which access path was used |
| Over time | Whether spend is trending up |

This moves the organization from having a rough idea where AI spend is going to seeing it broken down per model, per user, and per tool in one dashboard.

---

## What else does the gateway control?

Spend visibility is the part that gets attention first. The same layer carries several other controls.

**Access control.** Who can use a model, which endpoint is approved, which team is generating traffic, which credentials are used.

**Budgets and rate limits.** Spend caps and alerts applied at the level that fits the environment, whether that is organization, team, application, agent, or individual user.

**Routing and fallback.** A stable access layer even when the model behind the endpoint changes, which enables traffic splitting, testing a replacement model with no application change, and fallback when a provider is unavailable. Smart routing, covered in Guide 1, sits on top of this model access layer.

**Policies and guardrails.** Runtime evaluation of interactions between agents and models or tools, returning allow, ask, or deny. This matters most for agents, because tool calls create real side effects.

**Tracing and audit.** Which model handled a request, which user or agent generated it, how many tokens were used, what it cost, which tools were called, where latency occurred, and which policy fired.

---

## Unity Catalog and Unity AI Gateway

The two layers do different jobs.

```mermaid
flowchart TD
    A["Unity Catalog<br/>defines what is allowed"] --> B["Unity AI Gateway<br/>enforces it at runtime"]
    B --> C[Model / Tool / Agent]
```

Unity Catalog defines and governs the assets and the permissions across data, models, agents, MCP servers, tools, and skills. Unity AI Gateway applies that governance in the runtime path, on the actual request, and records what happened.

---

## How the first three lessons fit together

```mermaid
flowchart TD
    R[Request] --> A[Agent]
    A --> P["Policies<br/>allow / ask / deny"]
    P --> S["Smart routing<br/>pick the model"]
    S --> G["Unity AI Gateway<br/>govern and observe"]
    G --> M[Model or tool]
```

Smart routing decides which model handles the request. Policies decide what the agent is permitted to do. Unity AI Gateway provides the shared runtime layer for access, spend control, routing, and observability across all of it.

---

## What to watch out for

**System table ingestion lags.** Allow an hour or more before recent activity is queryable.

**Verify the schema.** System table columns can change. Check the Databricks documentation before building a dashboard on top of a query.

**Endpoint changes are silent to callers by design.** That is the benefit, and it also means you should record which models were behind an endpoint during a given period, since the usage tables are what reconstruct that later.

**Some capabilities may be in preview.** Confirm current availability in official documentation before production use.

---

## Try it

1. Create an endpoint in Unity AI Gateway and add two or three models from different providers behind it.
2. Send the same simple question through the AI Playground several times and watch the distribution.
3. Wait for ingestion, then run the query above against `system.ai_gateway.usage`.
4. Ask Genie which models were used recently.
5. Ask Genie to build a dashboard showing cost per model and cost per user.

---

## Related guides

- [Smart routing with Omnigent](./01-smart-routing.md)
- [Policies for agent behavior and spend](./02-agent-policies.md)

---

[← Previous: Policies for agent behavior and spend](./02-agent-policies.md)
