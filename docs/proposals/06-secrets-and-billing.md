# Proposal 06 — Secrets, Tokens & Billing

**Status:** DRAFT · Parent: [00 Overview](00-overview.md)

## Context

Every example needs credentials, and readers will ask "what will this cost?" This proposal
defines what the **site** must teach about provisioning a token and about billing — framed
for **adoption**, not cost governance (which is deferred). Our engine default is **Copilot**;
secrets are pulled from **repository secrets**.

## Part 1 — Tokens & secrets

### Two distinct credentials
1. **GitHub API access** — to read the repo and apply safe-outputs. Default is the
   workflow's built-in `GITHUB_TOKEN`, scoped by `permissions:`. A custom fine-grained PAT
   is only needed for **cross-repo** writes or **org Projects** (wired via
   `tools.github.github-token` or a dedicated safe-output token like
   `GH_AW_WRITE_PROJECT_TOKEN`).
2. **AI engine access (Copilot)** — one of:
   - **Org billing**: an org admin enables *"Allow use of Copilot CLI billed to the
     organization,"* and the workflow requests `copilot-requests: write` in `permissions:`.
     No PAT needed.
   - **Fine-grained PAT** stored as the `COPILOT_GITHUB_TOKEN` repo secret.

### PAT provisioning (what the site documents step-by-step)
- GitHub → Settings → Developer settings → **Fine-grained personal access tokens**.
- **Resource owner:** `titan-syndicate`; **Repository access:** only this repo.
- **Repository permissions** — grant the minimum the declared `safe-outputs` require:
  - `Contents: Read` (most), `Read/Write` for `create-pull-request`/`push-to-branch`.
  - `Issues: Read/Write` for `create-issue` / `add-comment` / `add-labels`.
  - `Pull requests: Read/Write` for PR safe-outputs.
  - `Discussions: Read/Write` for `create-discussion`.
- For CLI auth generally: `gh auth login --scopes repo,workflow`.

### Storing the secret
```bash
gh aw secrets set COPILOT_GITHUB_TOKEN          # or: gh secret set COPILOT_GITHUB_TOKEN
```

{: .warning }
Never place secrets in workflow-level `env:` — those values are exposed to the model. Use
the secret mechanisms above; the threat-detection job also scans for accidental leaks.

### Other engines (for reference)
`ANTHROPIC_API_KEY` (Claude), `OPENAI_API_KEY` (Codex), `GEMINI_API_KEY` (Gemini). Not used
by our default examples but documented for readers who switch engines.

## Part 2 — Billing primer (awareness, not governance)

A run has **two cost components**:
1. **GitHub Actions minutes** — standard Actions billing, including ~1.5 min of runner
   setup per job.
2. **AI inference** — measured in **AI Credits (AIC)**. **1 AIC = $0.01 USD**, shown in CLI
   output and the run footer.

**Built-in guardrails** (overridable in frontmatter):
- **1000 AIC per run** (`max-ai-credits`).
- **5000 AIC per workflow per day** (`max-daily-ai-credits`).
- 20-minute step timeout (`timeout-minutes`).

**Inspecting spend:** `gh aw logs <workflow>` (duration, tokens, AIC, turns),
`gh aw audit <run-id>`, `gh aw health`.

**Org Actions billing note (secondary use case):** when billed to an org, Copilot CLI usage
must be enabled by an admin, and AIC consumption rolls up to the org. We surface this so
adopters know the knob exists; **optimizing** org spend is out of scope for now.

{: .note }
**Verification caveat:** older write-ups mention "~2 premium requests per run." The current
`gh aw` docs express cost in **AIC**, and we could not verify the premium-request figure. The
site will cite **AIC** and add a premium-request mapping only if GitHub republishes one.

## What the site must contain (deliverables)

- [ ] A "Provision a token" page (already stubbed) with the click-path and minimum-scope
      table above.
- [ ] A "Billing & cost" reference page (already stubbed) with the AIC model, caps, and
      `gh aw logs`/`audit` walkthrough.
- [ ] A short org-billing callout, clearly marked secondary.

## Open questions
1. Default to **org billing** (`copilot-requests: write`, no PAT) or the **`COPILOT_GITHUB_TOKEN`
   PAT** path in the primary tutorial? (PAT is more self-contained for a reader without org
   admin; org billing is cleaner long-term.)
2. Do we want a `cost-tracker`-style example workflow later, or keep billing doc-only?
