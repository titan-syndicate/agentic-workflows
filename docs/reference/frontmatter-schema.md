---
title: Frontmatter schema
layout: default
parent: Reference
nav_order: 1
audience: expert
---

# Frontmatter schema
{: .no_toc }

{: .expert }
> The exhaustive key-by-key reference. This page will mirror the official
> [frontmatter reference](https://github.github.com/gh-aw/reference/frontmatter/) with our
> own annotations and examples.

## What this page will cover

- **Metadata** — `name`, `description`, `emoji`, `labels`, `metadata`.
- **Triggers & conditions** — full `on:` matrix, `if:`, command/label triggers, `roles`,
  `bots`, `reaction`, `stop-after`, skip filters, `manual-approval`.
- **Composition** — `imports` (shared tool/MCP fragments).
- **Permissions** — scopes, `read-all`/`write-all`, `copilot-requests`.
- **Engine** — simple + extended object form, `model`, `max-turns`, auth.
- **Network & security** — `network.allowed`, `strict`, `threat-detection`.
- **Tools** — `github.toolsets`, built-ins, `mcp-servers`.
- **Safe outputs** — the full ~40-type catalog with config keys.
- **Runtime** — `runs-on`, `container`, `services`, `timeout-minutes`, `concurrency`,
  `runtimes`, `cache`, `checkout`.
- **Cost controls** — `max-ai-credits`, `max-daily-ai-credits`.
- **Custom steps** — `pre-agent-steps`, `steps`, `post-steps`, `jobs`.

### Defaults
`timeout-minutes` 20 · `runs-on` ubuntu-latest · `strict` true · `max-ai-credits` 1000 ·
`checkout` true.
