# Install the `gh aw` extension

!!! info "Intro tier"
    Goal: get the `gh aw` CLI working locally so you can compile and run workflows.

## What this page will cover

- Prerequisites: `gh` ≥ 2.0.0, authenticated with `repo` and `workflow` scopes
  (`gh auth login --scopes repo,workflow`).
- Install the extension:

  ```bash
  gh extension install github/gh-aw
  gh aw version
  ```

- Initialize a repo for agentic workflows:

  ```bash
  gh aw init --engine copilot
  ```

- Where things land: workflows in `.github/workflows/*.md`, compiled `.lock.yml` siblings.

➡️ Next: [Provision a token](provision-token.md).
