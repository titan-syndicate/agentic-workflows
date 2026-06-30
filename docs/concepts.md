# Concepts

!!! info "Intro tier"
    The mental model behind agentic workflows. Each page starts with a plain-English summary
    for the intro tier, then expands into syntax detail for power users.

A workflow file has two halves: **frontmatter** (configuration) and a **natural-language
body** (instructions). These pages break down every part:

- **[Anatomy of a workflow](concepts/anatomy.md)** — the two halves and the compile step.
- **[Triggers](concepts/triggers.md)** — `on:` schedules, events, and command triggers.
- **[Permissions & safe outputs](concepts/permissions-and-safe-outputs.md)** — read-only by
  default, and the gated writes an agent is allowed to make.
- **[Tools & MCP](concepts/tools-and-mcp.md)** — the GitHub toolset, shell, and wiring up
  custom MCP servers the agent can call.
- **[Engines](concepts/engines.md)** — choosing Copilot CLI / Claude / Codex and selecting a
  model.
- **[Security model](concepts/security-model.md)** — sandboxing, the firewall, integrity
  filtering, and the threat-detection job.
