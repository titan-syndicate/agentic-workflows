---
title: "04 · Tool-using agents"
parent: Proposals
nav_order: 4
---

# Proposal 04 — Scenario C: Tool-Using Agents

**Status:** DRAFT · Parent: [00 Overview](00-overview.md) · Pattern: *agent-drives-the-tools*

## Context

Scenarios A and B are mostly *one-shot*: gather context, produce an output. The more
distinctive capability of agentic workflows is a **multi-step loop** where the agent
**decides which tools to call**, observes results, and continues — including tools you
expose via **custom MCP servers**. This scenario makes that concrete with several small
examples, and confronts the practical question: *what do the tools actually talk to?*

## What "tool-using" means here

- **Built-in tools** the agent can choose to invoke: the GitHub toolset (search → read →
  act), `bash`, `web-fetch`, `web-search`.
- **Custom MCP servers** (`mcp-servers:`) the agent calls like any other tool. Three
  transports are supported — stdio (a local Node process), http (a service URL), and a
  Docker container:

  ```yaml
  mcp-servers:
    inventory:
      command: "node"
      args: ["scripts/mcp/inventory-server.js"]
      allowed: ["list_items", "get_item"]
  ```

## Example shapes (small, each teaches one thing)

1. **GitHub toolset reasoning loop** — e.g. "find the open issue most likely to be a
   duplicate of #N and explain why," letting the agent search, read several issues, and
   compare. Teaches multi-call tool use with zero extra infra.
2. **Local stdio MCP server** — a ~50-line Node server exposing 2–3 domain tools over
   stdio, backed by a checked-in JSON fixture. Teaches the MCP wiring and tool-filtering
   (`allowed:`) without any hosting.
3. **HTTP MCP server** — the same tools behind an HTTP endpoint, to show the `url:` +
   `headers:` transport and the firewall/egress implications of reaching out.

## The hard part: test infrastructure (decision DEFERRED)

The agent needs *something* to call. We can't easily stand up a real Grafana-style service,
and per the overview this pass keeps infra **abstract**. Options, with tradeoffs:

| Option | What it is | Pros | Cons |
|---|---|---|---|
| **A. In-repo mock MCP + fixtures** | A small Node stdio MCP server reading checked-in JSON. | Zero cost, fully reproducible, runs in the runner, no secrets, no egress. | Not a "real" backend; can't show live/changing data. |
| **B. Cheap live host** | A lightweight service on Fly.io / Render / a small Linode-class VM the agent hits over HTTP. | Demonstrates real egress + auth + the firewall allowlist; closest to production. | Costs money; needs provisioning, a secret, and upkeep; another thing to secure. |
| **C. Ephemeral service in the runner** | Spin the service up as a `services:` container or a background step for the run's lifetime. | No standing cost; "real" HTTP within the run; reachable via `host.docker.internal`. | More workflow complexity; teaches an unusual setup. |

**Recommendation for first build:** **Option A** (in-repo mock) as the default teaching
example, with a clearly-marked **Option C** variant to demonstrate the HTTP transport and
firewall allowlist. **Option B** (a cheap live host) is documented as the "graduate to
production" path but **not provisioned now** — revisit as its own issue if we want a live
demo. If we do, Fly.io's free-tier-ish small machines are the lowest-friction modern
equivalent of "easy like Linode used to be."

## Firewall / egress note (expert)

Any tool that reaches the network interacts with the **Agent Workflow Firewall**, which is
default-deny. HTTP MCP servers and `web-fetch` require an explicit allowlist:

```yaml
network:
  allowed: [defaults, "api.our-service.example"]
```

This is itself a teachable security feature and a reason to prefer in-repo/stdio tools for
the intro examples.

## Concepts this teaches

- One-shot vs. agentic tool-use loops.
- Wiring custom MCP servers (stdio / http / docker) and filtering their tools.
- The firewall's role the moment an agent talks to the network.

## Open questions

1. Approve **A + C** for the first build, defer **B**? (Recommended.)
2. If we ever do **B**, which host — Fly.io, Render, or a small VM — and who owns the bill?
3. A single shared mock domain (e.g. a toy "inventory" service) across examples, or a
   different domain per example?

## Deliverables (on acceptance)

- [ ] `scripts/mcp/<service>-server.js` (stdio) + JSON fixtures.
- [ ] 2–3 `.github/workflows/*.md` tool-using examples (+ locks).
- [ ] Tutorial page contrasting one-shot vs. tool-loop, with the firewall callout.
- [ ] (Deferred) issue to evaluate a cheap live host for a real egress demo.
