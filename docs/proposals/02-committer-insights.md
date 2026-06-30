# Proposal 02 — Scenario A: Committer Insights

**Status:** DRAFT · Parent: [00 Overview](00-overview.md) · Pattern: *gather-then-summarize*

## Context

The safest, most legible way to introduce an agent into a workflow is to do the
**deterministic data-gathering in scripts** and hand the agent only the **subjective
summarization**. This scenario demonstrates that split on a concrete, useful task:
understanding contributor activity on a GitHub project.

It also showcases a pattern teams will reuse constantly — **a report template with
"agentic summary slots"** that scripts populate with data and the agent fills with prose.

## What it does

For a target repository (or GitHub Project), over a configurable window, produce a
**committer activity report**: per contributor, their pull requests, review comments,
commits, and issue status changes — followed by an agent-written narrative of trends,
highlights, and things worth a maintainer's attention.

## Design

### 1. Data gathering (plain Node, deterministic)

A small `scripts/committer-insights/` Node module pulls data via the `gh` CLI / GitHub
REST + GraphQL (no third-party deps):

- **Pull requests** — opened, merged, review turnaround, per author.
- **Review comments** — counts and threads, per author.
- **Commits** — counts, additions/deletions, per author (with merge-commit handling).
- **Issue status changes** — opened/closed/reopened and label transitions, derived from
  **issue timeline events**.

Output: a structured `data.json` the workflow can read. Keeping this in scripts means it's
**testable and reproducible** without the agent.

### 2. Report template with agentic slots

A Markdown template with explicit, named slots, e.g.:

```markdown
# Contributor Report — {{window}}

## By the numbers
{{table: per-committer stats}}     <!-- filled by script -->

## What stood out
<!-- agent: 3–5 bullets on notable trends, surprising contributors, risks -->

## Recommended follow-ups
<!-- agent: concrete, linkable next steps for maintainers -->
```

Scripts fill the deterministic slots; the agent fills the `<!-- agent: ... -->` slots from
`data.json`. This keeps numbers trustworthy and prose useful.

### 3. Workflow sketch (illustrative — not final)

```yaml
---
on:
  schedule: weekly on monday
  workflow_dispatch:
permissions: read-all
network: defaults
engine: copilot
tools:
  github:
    toolsets: [repos, issues, pull_requests]
  bash: ["node", "gh"]
safe-outputs:
  create-issue:
    title-prefix: "[committer-insights] "
    labels: [report]
---

# Committer insights
Run `node scripts/committer-insights/gather.js` to produce `data.json`, then fill the
agentic slots in `templates/committer-report.md` with a concise narrative grounded ONLY in
that data. Link every claim to the relevant PR/issue.
```

## Concepts this teaches

- The gather-then-summarize split and **why** it's the safe on-ramp.
- Reading the GitHub API from a workflow with native tooling.
- Template-slot prompting to keep agents grounded and outputs consistent.
- A read-only workflow whose only write is a single gated `create-issue`.

## Open questions

1. **Target scope** — a single repo, or aggregate across a GitHub **Project**/org? (Project
   aggregation needs broader token scope — see [06](06-secrets-and-billing.md).)
2. Output as a **created issue**, a **discussion**, or an uploaded **artifact**?
3. Window default — trailing 7 days vs. since-last-report (needs `cache-memory`/state)?

## Deliverables (on acceptance)

- [ ] `scripts/committer-insights/gather.js` (+ a tiny unit test of the data shape).
- [ ] `templates/committer-report.md` with slot markers.
- [ ] `.github/workflows/committer-insights.md` (+ compiled lock).
- [ ] Tutorial page walkthrough.
