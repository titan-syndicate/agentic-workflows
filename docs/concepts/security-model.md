# Security model

!!! abstract "Expert tier"
    Defense-in-depth: the agent is sandboxed, network-restricted, and every write is gated.

## What this page will cover

- **Job pipeline**: Pre-Activation → Activation (input sanitization) → **Agent Job
  (read-only)** → **Detection Job** → **Safe-Output Jobs** (separately scoped tokens).
- **Integrity filter** — untrusted GitHub content below `min-integrity`
  (`merged`/`approved`/`unapproved`/`none`) is filtered before the model sees it; public
  repos default to `approved`.
- **Sandboxing** — agent and MCP servers run in isolated Docker containers; secret
  redaction scans artifacts before upload.
- **Agent Workflow Firewall (AWF)** — default-deny network egress with domain/ecosystem
  allowlists (see [runners & firewall](../reference/runners-and-firewall.md)).
- **Threat-detection job** — scans output and patches for prompt injection, secret leaks,
  and malicious diffs; blocks safe outputs on failure. Has its own AIC budget.
- **Protected files** — manifests, `.github/workflows/`, and agent files default to
  `request_review`.
- **Compile-time** — JSON-schema validation, SHA-pinned actions, scanners (actionlint,
  zizmor, poutine).
