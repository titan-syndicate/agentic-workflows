# Proposal 00 — Overview (Top-Level)

**Status:** DRAFT · **Owner:** @rianfowler · **Repo:** `titan-syndicate/agentic-workflows`

## Context & problem

[GitHub Agentic Workflows](https://github.blog/changelog/2026-06-11-github-agentic-workflows-is-now-in-public-preview/)
(`gh aw`) entered public preview on 2026-06-11. They let teams describe repository
automation in natural-language Markdown and run it as a hardened GitHub Actions workflow
driven by an AI coding agent. The capability is powerful but new, and most engineers'
mental model stops at "Actions = CI." There is no internal, hands-on reference that shows
*what these are good for* and *how to build them well*.

This repo closes that gap. Its single purpose is **adoption and enablement**: give
engineers a guided, try-it-yourself path from "what is this?" to "I shipped one." Cost
governance, org-wide rollout policy, and production hardening are explicitly **later**
concerns.

## Goals

1. **Teach the model.** Explain agentic workflows in terms an Actions-literate engineer
   already understands (triggers, permissions, jobs) and where the new ideas live
   (safe-outputs, engines, the firewall).
2. **Show, don't tell.** Ship a small set of **runnable, idiomatic** example workflows that
   each teach a distinct concept — without one bloated mega-demo.
3. **Lower the activation energy.** A tutorial site people can walk top-to-bottom or skip
   around, plus copy-pasteable starting points.
4. **Stay native and legible.** Favor first-party Actions and plain Node scripts so the
   examples are auditable and don't depend on unverified marketplace actions.

## Audiences

The material is written for two tiers, and every page is tagged so readers self-select:

- **Intro tier** — engineers who use Actions for CI. They get: what agentic workflows can
  do, when to reach for them, and the handful of new concepts that matter. (The site
  landing page and the "what can you use this for" framing target this tier.)
- **Expert tier** — Actions power users and **runner administrators**. They get: exact
  frontmatter syntax, customization, the Agent Workflow Firewall, runner requirements, and
  billing mechanics.

## What we'll build (scenarios)

Three scenario families, each a sub-proposal. We deliberately keep each example **small and
single-purpose** to maximize concepts-taught per unit of complexity.

- **A — Committer insights** ([02](02-committer-insights.md)): the *gather-then-summarize*
  pattern. Node scripts collect contributor activity (PRs, comments, commits, issue status
  changes); the agent fills summary slots in a report template. Safest on-ramp.
- **B — Repository automation** ([03](03-repo-automation-examples.md)): the canonical
  GitHub examples — triage, reporting, docs hygiene — each mapped to one `safe-output`.
- **C — Tool-using agents** ([04](04-tool-using-agents.md)): the *agent-drives-the-tools*
  pattern, including custom MCP servers, with several example shapes.

Plus [05 — Novel use cases](05-novel-use-cases.md): a menu of idiomatic ideas to build next.

## The framing: Continuous AI

GitHub positions agentic workflows as **Continuous AI** — a sibling to CI/CD aimed at the
*subjective, repetitive* work that's painful to express deterministically (triage,
summaries, "is this doc stale?"). We adopt that framing throughout: agentic workflows
**augment** pipelines, they don't replace deterministic build/test/release.

## Scope & non-goals

**In scope (this initiative):** the proposal set, the tutorial site, and a small number of
runnable example workflows targeting the **Copilot engine** on **GitHub-hosted runners**,
with secrets pulled from **repository secrets**.

**Non-goals (deferred, noted as future work):**

- **Cost management.** We document how billing works (AIC, caps, `gh aw logs`/`audit`) for
  awareness, but optimizing or governing spend is a later effort.
- **Live tool-backing infrastructure.** Scenario C documents options for where an agent's
  tools live, but we do **not** stand up a hosted service in this pass — the decision is
  deferred (see [04](04-tool-using-agents.md)).
- **Org-wide rollout / policy.** Enablement first; governance later.
- **Multi-engine depth.** We default to Copilot; other engines are mentioned, not built.

## Success criteria

- A new engineer can read the site and **explain** what an agentic workflow is and when to
  use one.
- A reader can **run** at least one example end-to-end by following a tutorial.
- Each example **teaches a distinct concept** and uses only native actions + plain Node.
- The Pages site builds cleanly and is navigable both linearly and by jumping.

## Proposal map

| Sub-proposal | Decides |
|---|---|
| [01 Repo & site structure](01-repo-and-site-structure.md) | Layout, site IA, generator, tiering. |
| [02 Committer insights](02-committer-insights.md) | Scenario A design. |
| [03 Repository automation](03-repo-automation-examples.md) | Scenario B subset + mapping. |
| [04 Tool-using agents](04-tool-using-agents.md) | Scenario C shapes + test-infra options. |
| [05 Novel use cases](05-novel-use-cases.md) | Backlog of ideas. |
| [06 Secrets & billing](06-secrets-and-billing.md) | Token provisioning + billing primer. |
| [07 Conventions](07-conventions.md) | Engineering standards. |

## Acceptance → work

On acceptance of a sub-proposal, we file a tracking **epic issue** on this repo and break
it into task issues. This overview is accepted when the audiences, scope, and scenario set
above are agreed.

## Open questions for review

1. Is the **three-scenario** set (A/B/C) the right initial breadth, or should we ship A+B
   first and treat C as a fast-follow?
2. **Copilot engine** is our default per current direction — do we also want a single
   Claude-engine example for contrast, or keep that out of scope for now?
3. Any audience beyond the two tiers (e.g. EMs evaluating adoption) we should write for?
