---
title: Repository automation
layout: default
parent: Tutorials
nav_order: 2
audience: intro
---

# Repository automation
{: .no_toc }

{: .tryit }
> The bread-and-butter scenarios from GitHub's own examples — triage, reporting, and docs
> hygiene — each kept small and single-purpose.

## What this walkthrough will cover

- **Continuous triage** — label and route new issues (`on: issues`, `add-labels` +
  `add-comment`).
- **Daily reporting** — a scheduled repo-health digest (`safe-outputs: create-issue`).
- **Docs hygiene** — detect README/code drift and open a PR (`create-pull-request`).
- How each maps to a single `safe-outputs` type, and why we keep them separate rather than
  one monolith.
- Try-it steps for each.

Maps to proposal
[`03-repo-automation-examples`](https://github.com/titan-syndicate/agentic-workflows/blob/main/docs/proposals/03-repo-automation-examples.md).
