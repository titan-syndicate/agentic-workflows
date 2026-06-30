---
title: Committer insights
layout: default
parent: Tutorials
nav_order: 1
audience: intro
---

# Committer insights
{: .no_toc }

{: .tryit }
> Gather contributor activity with plain Node scripts, then let the agent turn the raw
> data into a readable narrative.

## What this walkthrough will cover

- The **gather-then-summarize** pattern: deterministic data collection (scripts) feeding a
  subjective summary (agent) — the safest way to start.
- A Node script (`scripts/`) that pulls, per committer: PRs opened/merged, review comments,
  commits, and issue status changes, via the `gh` CLI / GitHub API. Zero/minimal deps.
- A **report template** with explicit *agentic summary slots* (`<!-- agent: trends -->`)
  the workflow fills in.
- Frontmatter: scheduled trigger, `permissions: read-all`, `safe-outputs: create-issue`
  (or `create-discussion`).
- Try-it steps + what "good output" looks like.

Maps to proposal
[`02-committer-insights`](https://github.com/titan-syndicate/agentic-workflows/blob/main/docs/proposals/02-committer-insights.md).
