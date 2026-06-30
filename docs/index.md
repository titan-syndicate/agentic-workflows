# GitHub Agentic Workflows

A practical guide to **GitHub Agentic Workflows** (`gh aw`) — AI automations you write in
Markdown and run as GitHub Actions.

[Get started](getting-started/install.md){ .md-button .md-button--primary }
[Browse the concepts](concepts.md){ .md-button }

!!! info "Intro tier — for engineers who use Actions for CI"
    This page is for engineers who already use GitHub Actions for CI and want to understand
    what agentic workflows are and when they're worth reaching for. No agent-building
    experience assumed.

## What is an agentic workflow?

If you've written a CI workflow, you already know 80% of the shape. A normal GitHub Actions
job runs **deterministic steps** you spell out — `npm test`, `docker build`, deploy. An
**agentic** workflow hands part of the job to an AI coding agent and describes the goal in
**plain language** instead of exact commands:

- You author a Markdown file in `.github/workflows/` with **YAML frontmatter** (when it
  runs, what it's allowed to touch) and a **natural-language body** (what you want done).
- You compile it with `gh aw compile` into a hardened `.lock.yml` — an ordinary Actions
  workflow — and commit both files.
- On its trigger, the agent reads your instructions, looks at the repo, reasons, and
  produces a **gated output**: a comment, a label, an issue, or a pull request.

GitHub frames this as **Continuous AI** — the sibling of CI/CD for the *subjective,
repetitive* tasks that are painful to express as deterministic scripts. It augments your
pipelines; it doesn't replace them.

## What can you use them for?

A good rule of thumb: **if the repetitive work can be described in words, it might be a fit.**
Common patterns:

| Pattern | Example |
|---------|---------|
| **Triage** | Summarize, label, and route new issues as they're opened. |
| **Reporting** | Post a daily/weekly repo-health digest as an issue. |
| **Docs hygiene** | Notice when code drifts from the README and open a PR to fix it. |
| **CI doctoring** | When a build fails, diagnose the likely cause and comment on the PR. |
| **Code simplification** | Periodically refactor and open small, reviewable PRs. |
| **Data gathering** | Aggregate contributor activity and summarize the trends. |

## How to think about them (before you build)

A few considerations that matter more here than in normal CI:

- **Default to read-only.** Agentic workflows run with read permissions by default. Any
  *write* must be declared as a **safe output** (e.g. `create-issue`, `add-comment`,
  `create-pull-request`). PRs are **never auto-merged** — a human stays in the loop.
- **Treat the Markdown as code.** It's a prompt *and* a permission boundary. Review changes
  to it the way you'd review a Dockerfile.
- **Start low-risk, escalate.** Begin with comments and reports; graduate to PR-creating
  workflows once you trust the behavior.
- **Cost is real but bounded.** Runs consume Actions minutes plus model inference. There
  are per-run and per-day caps, and you can inspect spend with `gh aw logs` / `gh aw audit`.
  (See the [billing reference](reference/billing.md).)
- **Specificity is a dial.** "Improve the software" and "Add tests for the auth module,
  targeting untested branches" are both valid — pick the altitude that fits the task.

## Where to go next

1. **[Getting started](getting-started.md)** — install `gh aw`, provision a token, run your
   first workflow. *(Intro)*
2. **[Concepts](concepts.md)** — frontmatter, triggers, permissions, safe-outputs, tools/MCP,
   engines, and the security model. *(Intro → Expert)*
3. **[Tutorials](tutorials.md)** — work through real scenarios end-to-end. *(Hands-on)*
4. **[Reference](reference.md)** — full schema, runner infrastructure, the Agent Workflow
   Firewall, and billing. *(Expert)*

!!! note
    This site is part of the [`titan-syndicate/agentic-workflows`](https://github.com/titan-syndicate/agentic-workflows)
    enablement repo. The example workflows are being scoped now — see the
    [proposals](proposals.md).
