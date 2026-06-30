# Agentic Workflows

A hands-on **enablement and documentation** repository for
[GitHub Agentic Workflows](https://github.blog/changelog/2026-06-11-github-agentic-workflows-is-now-in-public-preview/)
(`gh aw`) — AI-powered repository automations authored in Markdown and run as GitHub
Actions.

This repo exists to help engineers **adopt** agentic workflows: understand what they are,
when to reach for them, and how to build them — with worked examples and a tutorial-style
documentation site.

> **Status:** Proposal phase. The example workflows are not built yet — we're aligning on
> scope first. See [`docs/proposals/`](docs/proposals/) for the plan.

## What's here

| Path | What it is |
|------|------------|
| [`docs/proposals/`](docs/proposals/) | The proposal set: a top-level vision plus focused sub-proposals for each scenario we'll build. Start at [`00-overview.md`](docs/proposals/00-overview.md). |
| `docs/` (site) | A Jekyll + Just-the-Docs tutorial site, published via GitHub Pages. Walk it top-to-bottom or skip to a topic. |
| `.github/workflows/` | *(Coming later)* The compiled agentic workflows. |
| `scripts/` | *(Coming later)* Plain Node.js data-gathering scripts used by the workflows. |

## Documentation site

Once published, the tutorial site lives at:
**https://titan-syndicate.github.io/agentic-workflows/**

It's written for two audiences:
- **Intro tier** — engineers who already use GitHub Actions for CI and want to know what
  agentic workflows can do and how to think about them.
- **Expert tier** — Actions power users and runner administrators who need exact syntax,
  customization, and infrastructure detail.

## Conventions

- Workflows favor **native first-party Actions** (`actions/*`) and the `gh`/`github` CLI —
  no unverified marketplace actions.
- Scripting is **plain Node.js** run with `node` (no compiled/bundled JS actions).
- Secrets come from **repository secrets**; the site documents how to provision the
  required token.

## License

[MIT](LICENSE)
