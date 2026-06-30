# Provision a token & set the secret

!!! info "Intro tier"
    Agentic workflows need credentials for two things: the **GitHub API** (to read the repo
    and apply safe outputs) and the **AI engine** (to do the reasoning). This page covers
    both for the **Copilot engine**, which is our default.

## What this page will cover

### Engine credential (Copilot)
Two supported paths:
- **Org billing** — an org admin enables *"Allow use of Copilot CLI billed to the
  organization"*, and the workflow requests `copilot-requests: write` in `permissions:`.
- **Fine-grained PAT** — store a token as the `COPILOT_GITHUB_TOKEN` repository secret.

### GitHub API token
- Default: the workflow's built-in `GITHUB_TOKEN`, scoped by `permissions:`.
- Custom: a fine-grained PAT wired via `tools.github.github-token: ${{ secrets.MY_PAT }}`
  — needed for cross-repo writes or org Projects (e.g. `GH_AW_WRITE_PROJECT_TOKEN`).

### Minimum scopes
Grant only what the declared `safe-outputs` require — e.g. `issues: write` for
`create-issue`, `pull-requests: write` for `create-pull-request`.

### Setting the secret
```bash
gh aw secrets set COPILOT_GITHUB_TOKEN
# or
gh secret set COPILOT_GITHUB_TOKEN
```

!!! warning
    Never put secrets in workflow-level `env:` — those values are exposed to the model. Use
    the secret mechanisms above.

➡️ Next: [Your first run](first-run.md).
