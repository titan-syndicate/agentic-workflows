---
title: Concepts
layout: default
nav_order: 3
has_children: true
audience: intro
---

# Concepts
{: .no_toc }

{: .intro }
> The mental model behind agentic workflows. Each page starts with a plain-English summary
> for the intro tier, then expands into syntax detail for power users.

A workflow file has two halves: **frontmatter** (configuration) and a **natural-language
body** (instructions). These pages break down every part:

- **[Anatomy of a workflow](concepts/anatomy)** — the two halves and the compile step.
- **[Triggers](concepts/triggers)** — `on:` schedules, events, and command triggers.
- **[Permissions & safe outputs](concepts/permissions-and-safe-outputs)** — read-only by
  default, and the gated writes an agent is allowed to make.
- **[Tools & MCP](concepts/tools-and-mcp)** — the GitHub toolset, shell, and wiring up
  custom MCP servers the agent can call.
- **[Engines](concepts/engines)** — choosing Copilot CLI / Claude / Codex and selecting a
  model.
- **[Security model](concepts/security-model)** — sandboxing, the firewall, integrity
  filtering, and the threat-detection job.
