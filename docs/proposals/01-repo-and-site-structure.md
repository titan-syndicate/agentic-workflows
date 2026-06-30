# Proposal 01 — Repo & Site Structure

**Status:** DRAFT · Parent: [00 Overview](00-overview.md)

## Context

Before writing examples, we fix the repo layout, the documentation site's information
architecture, and the conventions that keep both legible as they grow. Getting this right
early avoids churn later.

## Repo layout

```
agentic-workflows/
├── README.md                  # what this repo is; points to site + proposals
├── LICENSE                    # MIT
├── .github/
│   └── workflows/             # agentic workflow .md + compiled .lock.yml (LATER)
├── scripts/                   # plain Node data-gathering scripts (LATER)
├── docs/                      # the GitHub Pages site (Jekyll + Just-the-Docs)
│   ├── _config.yml
│   ├── index.md               # landing / "what & why" (intro tier)
│   ├── getting-started/       # install → token → first run
│   ├── concepts/              # frontmatter, triggers, safe-outputs, tools/MCP, engines, security
│   ├── tutorials/             # one per built scenario (try-it-yourself)
│   ├── reference/             # expert tier: schema, runners/firewall, billing, self-hosted
│   └── proposals/             # THIS folder
```

The `.github/workflows/` and `scripts/` trees are stubbed in the proposals now and filled
when each scenario is built.

## Documentation site

### Generator: Jekyll + Just-the-Docs

**Recommendation:** publish from `main` `/docs` using **Jekyll** with the
**Just-the-Docs** remote theme.

Rationale:

- **Native build, no custom Action.** GitHub Pages builds Jekyll itself (via
  `jekyll-remote-theme`), so there's no build pipeline for us to own or secure — consistent
  with our "native and legible" principle. *(This is a site theme, not a workflow action,
  so it doesn't conflict with the "native actions only" rule that governs the example
  workflows.)*
- **Tutorial-shaped.** Left-nav, built-in client-side search, and ordered/nested pages let
  readers go top-to-bottom **or** jump straight to a topic — exactly the "work through it
  but skip around" experience we want.
- **Low ceremony.** Content is plain Markdown with light front matter.

Alternatives considered: bare Jekyll default theme (weaker nav/search), a SPA docs
framework like Docusaurus (needs a Node build + deploy Action — more surface), hand-rolled
HTML (most control, most maintenance). Just-the-Docs is the best fit for a docs/tutorial
site with minimal upkeep.

### Information architecture

| Section | Tier | Purpose |
|---|---|---|
| **Home** | Intro | What agentic workflows are, when to use them, how to think about them. |
| **Getting started** | Intro | install → provision token → first run. The "try it" on-ramp. |
| **Concepts** | Intro→Expert | One page each: anatomy, triggers, permissions & safe-outputs, tools & MCP, engines, security model. Summary first, detail below. |
| **Tutorials** | Hands-on | One per built scenario, each a self-contained walkthrough. |
| **Reference** | Expert | Full frontmatter schema, runners & firewall, billing, self-hosted. |

### Audience tiering convention

- Every page declares `audience: intro` or `audience: expert` in front matter.
- A colored callout badge at the top of each page (`{: .intro }` / `{: .expert }`) makes
  the tier visible at a glance, so a CI-familiar reader knows when a page is going deep and
  an expert knows when a page is foundational.
- "Try it yourself" steps use a distinct `{: .tryit }` callout.

## Naming & conventions (summary)

- Workflows: `.github/workflows/<verb-noun>.md` (e.g. `triage-issues.md`), compiled to
  `<verb-noun>.lock.yml`. Both committed.
- Scripts: `scripts/<scenario>/<thing>.js`, plain Node, run via `node`.
- Full standards live in [07 Conventions](07-conventions.md).

## Deliverables (on acceptance)

- [ ] Confirm generator choice and site IA (this proposal).
- [ ] Pages site scaffold committed and building (DONE this pass — structure only).
- [ ] Enable GitHub Pages from `main` `/docs`.
- [ ] Fill section content as scenarios land.

## Open questions

1. Publish from `main /docs` (simplest) vs. a dedicated `gh-pages` branch? Recommendation:
   `main /docs`.
2. Custom domain, or the default `titan-syndicate.github.io/agentic-workflows`?
   Recommendation: default for now.
