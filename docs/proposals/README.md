---
title: Proposals (folder index)
nav_exclude: true
search_exclude: true
---

# Proposals

This folder holds the proposal set for the `agentic-workflows` enablement repo. It starts
with a **top-level proposal** and branches into focused **sub-proposals**, each sized to
become one (or a few) GitHub issues once accepted.

## How to read this

Start with [`00-overview.md`](00-overview.md) — it frames the why, the audiences, the
scope, and links out to everything else. Then read whichever sub-proposals are relevant to
you.

## Reading order

| # | Proposal | What it decides |
|---|----------|-----------------|
| 00 | [Overview](00-overview.md) | Vision, audiences, scope, success criteria, non-goals. **Read first.** |
| 01 | [Repo & site structure](01-repo-and-site-structure.md) | Repo layout, the Pages tutorial site IA, generator choice, audience tiering. |
| 02 | [Committer insights](02-committer-insights.md) | Scenario A — gather contributor data with scripts, summarize with the agent. |
| 03 | [Repository automation examples](03-repo-automation-examples.md) | Scenario B — triage, reporting, docs hygiene (a balanced subset of GitHub's examples). |
| 04 | [Tool-using agents](04-tool-using-agents.md) | Scenario C — multi-step tool use and custom MCP servers; test-infra options. |
| 05 | [Novel use cases](05-novel-use-cases.md) | Idiomatic ideas to consider building next. |
| 06 | [Secrets & billing](06-secrets-and-billing.md) | PAT provisioning, repo secrets, org Actions billing primer. |
| 07 | [Conventions](07-conventions.md) | Engineering standards for the repo (native actions, plain Node, compile flow). |

## Status

All proposals are **DRAFT** pending review. Legend: `DRAFT` → `ACCEPTED` → `ISSUES FILED`.

| Proposal | Status |
|----------|--------|
| 00 Overview | DRAFT |
| 01 Repo & site structure | DRAFT |
| 02 Committer insights | DRAFT |
| 03 Repository automation | DRAFT |
| 04 Tool-using agents | DRAFT |
| 05 Novel use cases | DRAFT |
| 06 Secrets & billing | DRAFT |
| 07 Conventions | DRAFT |

## From proposal to work

Once a proposal is **accepted**, we file tracking issues on this repo (one epic per
sub-proposal, broken into tasks). Until then, nothing here is built — these documents are
the plan, not the implementation.

## Source of truth for syntax

Technical claims about `gh aw` syntax are drawn from the official docs
(https://github.github.com/gh-aw/) and GitHub's announcement/guide posts. Where a detail
could not be verified, it is flagged inline (see especially the billing notes in `06`).
