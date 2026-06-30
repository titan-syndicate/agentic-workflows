# Billing & cost

!!! abstract "Expert tier"
    What a run actually costs, the built-in caps, and how to inspect spend. (Cost
    *management* is a future focus for this repo — this page is the primer.)

## What this page will cover

- **Two cost components**: (1) GitHub **Actions minutes** (incl. ~1.5 min runner setup),
  and (2) **AI inference** billed by the engine provider.
- **AI Credits (AIC)** — the primary metric. **1 AIC = $0.01 USD**, computed from model
  pricing and shown in CLI output and the run footer.
- **Default guardrails** — **1000 AIC per run**, **5000 AIC per workflow per day**, and a
  20-minute step timeout. Override with `max-ai-credits` / `max-daily-ai-credits` /
  `timeout-minutes`.
- **Inspecting spend** — `gh aw logs <workflow>` (duration, tokens, AIC, turns),
  `gh aw audit <run-id>`, `gh aw health`.
- **Cost levers** — `skip-if-match`/`skip-if-no-match`, smaller models, scheduled
  batching, `max-turns`.
- **Org billing for Copilot** — admin must enable Copilot CLI org billing; the AIC model
  supersedes the older "premium requests" framing.

!!! note
    The often-quoted "~2 premium requests per run" figure could not be verified against the
    current docs, which express cost in AIC. We'll cite AIC and update if GitHub republishes
    a premium-request mapping.
