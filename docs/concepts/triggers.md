# Triggers (`on:`)

!!! info "Intro tier"
    When does the agent wake up? Same `on:` model as Actions, plus a few agent-specific
    forms.

## What this page will cover

- **Scheduled** — cron, or natural-language (`schedule: weekly on monday`,
  `daily around 14:00`); the compiler scatters times to avoid thundering herds.
- **Event-driven** — `issues`, `pull_request`, `issue_comment`, with `types` and label
  filters.
- **Workflow completion** — `workflow_run` (e.g. react to a failed CI run, like
  `ci-doctor`).
- **Command triggers** — `slash_command` (e.g. `/investigate` in a comment) and
  `label_command` (apply a label to fire).
- **Manual** — `workflow_dispatch` with typed `inputs`.
- **Guardrails on triggers** — `roles:` (restrict who can invoke), `bots:` allowlist,
  `reaction:`, `stop-after:` deadlines, and `skip-if-match` / `skip-if-no-match` to avoid
  redundant runs.

See the [frontmatter schema](../reference/frontmatter-schema.md) for the exhaustive list.
