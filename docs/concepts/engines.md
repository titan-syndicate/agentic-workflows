# Engines

!!! abstract "Expert tier"
    The `engine:` key selects which coding agent drives the workflow. We default to Copilot;
    the model is pluggable.

## What this page will cover

- **Supported engines**: `copilot` (default), `claude`, `codex`, `gemini` (plus
  experimental `crush`, `opencode`, `pi`).
- **Simple vs extended form**:

  ```yaml
  engine: copilot
  # or
  engine:
    id: copilot
    model: gpt-5
    version: latest
    max-turns: 20
  ```

- **Credentials per engine** — Copilot: `copilot-requests: write` or
  `COPILOT_GITHUB_TOKEN`; Claude: `ANTHROPIC_API_KEY`; Codex: `OPENAI_API_KEY`; Gemini:
  `GEMINI_API_KEY`.
- **Turn / continuation budgets** — `max-turns`, `max-continuations`, per-tool `timeout`.
- **When to switch** — cost vs. capability tradeoffs; smaller models for high-frequency
  workflows (see [billing](../reference/billing.md)).
