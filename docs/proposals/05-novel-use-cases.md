---
title: "05 · Novel use cases"
parent: Proposals
nav_order: 5
---

# Proposal 05 — Novel & Idiomatic Use Cases

**Status:** DRAFT · Parent: [00 Overview](00-overview.md)

## Context

Beyond the three scenario families we plan to build first, agentic workflows enable a
broader design space. This proposal is a **menu** — a backlog of idiomatic ideas to pull
from once the foundations land. Each is annotated with the trigger and safe-output it would
use, and the *design pattern* it exemplifies (GitHub groups these as ChatOps, DailyOps,
DataOps, IssueOps, ProjectOps, MultiRepoOps, Orchestration).

## Candidate use cases

### ChatOps (interactive, command-triggered)
- **`/investigate` an issue** — `slash_command` trigger; the agent reads the issue + linked
  code/logs and posts a root-cause hypothesis as a comment. *(IssueOps + ChatOps.)*
- **`/explain this PR`** — summarize a large diff for reviewers on demand.

### DailyOps (scheduled)
- **Release-notes drafter** — on tag/release, draft notes from merged PRs into a
  `create-pull-request` against `CHANGELOG.md`.
- **On-call digest** — a morning summary of overnight CI failures, new P1 issues, and stale
  PRs, as an issue.
- **Stale-PR nudger** — comment on PRs idle > N days with a concrete next step.

### DataOps (analytics)
- **Dependency-update triage** — when Dependabot opens a PR, the agent assesses changelog
  risk and comments a recommended action. (`bots:` allowlist + `pull_request`.)
- **Flaky-test spotter** — scan recent CI runs for intermittent failures and file an issue
  with the suspects.

### ProjectOps
- **Backlog groomer** — periodically propose `set-issue-field` priorities / milestone
  assignments for review (never auto-applied).
- **Roadmap status update** — `create-project-status-update` summarizing movement on a
  Project board.

### MultiRepoOps / Orchestration
- **Cross-repo docs sync** — when a shared API changes, open PRs updating docs in sibling
  repos (`dispatch-workflow` / cross-repo safe-outputs with a scoped token).
- **Fan-out reporter** — one scheduled workflow that dispatches per-repo report workflows
  and aggregates.

### Quality & security
- **Accessibility review** (à la `accessibility-review.md`) — flag a11y regressions on PRs.
- **Architecture diagram keeper** (à la `archie.md`) — regenerate Mermaid diagrams when
  structure changes.
- **Security-advisory triage** — summarize new advisories affecting the repo's deps.

## How to choose what's next

Prioritize ideas that (a) teach a concept we haven't shown, (b) are useful on *this* repo
(dogfooding), and (c) stay single-purpose. Strong "build next" candidates: **`/investigate`
ChatOps** (new trigger type), **release-notes drafter** (PR-writing on a real artifact), and
**dependency-update triage** (`bots:` + reasoning over external changelogs).

## Deliverables

This proposal produces **no code directly** — it's the backlog. On acceptance, the top 1–3
picks become their own sub-proposals/issues.
