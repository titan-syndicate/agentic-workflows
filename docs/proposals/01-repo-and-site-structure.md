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
├── mkdocs.yml                 # MkDocs Material config (theme, palette, nav)
├── .github/
│   └── workflows/             # docs deploy (now) + agentic workflows (LATER)
├── scripts/                   # plain Node data-gathering scripts (LATER)
├── docs/                      # the GitHub Pages site (MkDocs Material)
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

### Generator: MkDocs Material

**Recommendation:** build the site with **MkDocs** + the **Material for MkDocs** theme,
published to GitHub Pages via a GitHub Actions workflow.

Rationale:

- **First-class theming.** Material has native light/dark that follows the visitor's
  `prefers-color-scheme` with a built-in toggle — no JavaScript stylesheet-swapping. This
  is the deciding factor (see the migration note below).
- **Tutorial-shaped.** Left-nav with section index pages, built-in search, and admonitions
  let readers go top-to-bottom **or** jump straight to a topic.
- **Plain Markdown.** Content is Markdown with Material's admonition syntax; nav is declared
  in `mkdocs.yml`.
- **Native-actions build.** Deployed by `.github/workflows/docs.yml` using only first-party
  `actions/*` (checkout, setup-python, upload-pages-artifact, deploy-pages) — consistent
  with the repo's "native actions only" convention. A docs build pipeline is on-theme for a
  repo about GitHub Actions.

!!! note "Migration note"
    The scaffold initially used **Jekyll + Just-the-Docs** (chosen to avoid a build step,
    since GitHub Pages builds Jekyll natively). We migrated to MkDocs Material because
    Just-the-Docs' dark-mode toggle swaps an entire stylesheet via JS and drops the site's
    `baseurl` on a project (subpath) site, so the toggle silently 404'd. Material does
    theming with CSS the right way. The small cost is an explicit build workflow — which is
    a feature, not a burden, for this repo.

Alternatives considered: staying on Just-the-Docs (works once patched, but fiddly theming);
Astro Starlight (excellent, Node-based, heavier setup); hand-rolled HTML (trivial theming
but you lose nav + search as the site grows).

### Information architecture

| Section | Tier | Purpose |
|---|---|---|
| **Home** | Intro | What agentic workflows are, when to use them, how to think about them. |
| **Getting started** | Intro | install → provision token → first run. The "try it" on-ramp. |
| **Concepts** | Intro→Expert | One page each: anatomy, triggers, permissions & safe-outputs, tools & MCP, engines, security model. Summary first, detail below. |
| **Tutorials** | Hands-on | One per built scenario, each a self-contained walkthrough. |
| **Reference** | Expert | Full frontmatter schema, runners & firewall, billing, self-hosted. |

### Audience tiering convention

- A colored **admonition** at the top of each page marks its tier: `!!! info "Intro tier"`
  for foundational pages, `!!! abstract "Expert tier"` for deep ones — so readers know at a
  glance how deep a page goes.
- "Try it yourself" steps use a distinct `!!! example "Try it yourself"` admonition.

## Naming & conventions (summary)

- Workflows: `.github/workflows/<verb-noun>.md` (e.g. `triage-issues.md`), compiled to
  `<verb-noun>.lock.yml`. Both committed.
- Scripts: `scripts/<scenario>/<thing>.js`, plain Node, run via `node`.
- Full standards live in [07 Conventions](07-conventions.md).

## Deliverables (on acceptance)

- [x] Confirm generator choice and site IA (MkDocs Material; this proposal).
- [x] Pages site scaffold committed and building (structure only).
- [x] Build & deploy via GitHub Actions (`.github/workflows/docs.yml`), Pages source set to
      "GitHub Actions".
- [ ] Fill section content as scenarios land.

## Open questions

1. Pin the `actions/*` versions in `docs.yml` to commit SHAs (per our pinning convention),
   or keep major-version tags for a docs CI workflow? Recommendation: SHA-pin in a cleanup
   pass.
2. Custom domain, or the default `titan-syndicate.github.io/agentic-workflows`?
   Recommendation: default for now.
