# Proposal 03 — Scenario B: Repository Automation Examples

**Status:** DRAFT · Parent: [00 Overview](00-overview.md)

## Context

GitHub's own
[guide](https://github.blog/ai-and-ml/automate-repository-tasks-with-github-agentic-workflows/)
presents a family of "Continuous *" automations. Rather than build all of them (or one
monolith), we ship a **balanced subset** that each teaches a different trigger + safe-output
combination, then list the rest as "also possible."

**Principle:** one workflow = one job = one safe-output type. Small, single-purpose
workflows are easier to review, cheaper to run, and clearer to teach than a kitchen-sink
agent.

## The full menu (from GitHub's examples)

| Pattern | Trigger | Primary safe-output |
|---|---|---|
| Continuous **triage** | `issues: [opened]` | `add-labels` + `add-comment` |
| Continuous **reporting** | `schedule` | `create-issue` |
| Continuous **docs** | `push` / `schedule` | `create-pull-request` |
| Continuous **simplification** | `schedule` | `create-pull-request` |
| Continuous **test improvement** | `pull_request` | `create-pull-request` |
| Continuous **CI hygiene** | `workflow_run: [completed]` | `create-issue` / `add-comment` |

## What we'll build first (recommended subset)

Three, ordered by escalating risk — matching the "start conservative, escalate" guidance:

### B1 — Continuous triage *(comment + label; low risk)*
Label and welcome new issues. Teaches event triggers, the GitHub toolset, and **two**
safe-outputs working together.

```yaml
on:
  issues:
    types: [opened, reopened]
permissions: { contents: read, issues: read }
engine: copilot
tools: { github: { toolsets: [issues, labels] } }
safe-outputs:
  add-labels:
    allowed: [bug, enhancement, question, docs, "area/*"]
    max: 3
  add-comment:
```

### B2 — Daily repo-status report *(creates an issue; low risk)*
A scheduled maintainer digest. Teaches scheduled triggers and `create-issue`. Mirrors
GitHub's canonical `daily-repo-status` example.

```yaml
on: { schedule: daily, workflow_dispatch: {} }
permissions: read-all
safe-outputs:
  create-issue:
    title-prefix: "[repo-status] "
    labels: [report]
```

### B3 — Docs drift → PR *(opens a PR; medium risk)*
When code changes, check whether the README still matches and open a **small** PR if not.
Teaches `create-pull-request`, `protected-files`, and why PRs are never auto-merged.

```yaml
on: { push: { branches: [main] } }
permissions: { contents: read }
safe-outputs:
  create-pull-request:
    title-prefix: "[docs] "
    labels: [documentation]
```

> CI hygiene (`ci-doctor`-style, reacting to `workflow_run` failures) is a strong **B4
> stretch goal** — it's a great demo but needs a failing workflow to react to, so we'd add
> a deliberately flaky example CI job to trigger it.

## Concepts this teaches

- The spread of trigger types (event, schedule, push, workflow_run).
- Mapping intent → the right `safe-output`, and combining outputs.
- Risk laddering: comment → issue → PR.
- Keeping workflows single-purpose instead of monolithic.

## Open questions

1. Build **B1–B3** now and treat **B4 (CI hygiene)** as a fast-follow? (Recommended.)
2. For B3, scope to README only, or any `docs/**` drift?
3. Should triage labels be repo-configurable via a checked-in config file?

## Deliverables (on acceptance)

- [ ] `.github/workflows/{triage-issues,daily-repo-status,docs-drift}.md` (+ locks).
- [ ] A tutorial page covering all three with try-it steps.
- [ ] (Stretch) flaky-CI example + `ci-doctor`-style workflow.
