# Proposal 07 — Engineering Conventions

**Status:** DRAFT · Parent: [00 Overview](00-overview.md)

## Context

Consistent conventions keep the examples auditable, teachable, and safe to copy. These are
the standards every workflow and script in this repo should follow. They encode the
direction set in the overview: **native, legible, single-purpose**.

## 1. Actions & dependencies

- **Native first-party actions only.** Use `actions/checkout`, `actions/setup-node`, and
  the `gh`/`github` tooling. **Avoid unverified marketplace actions.** If a third-party
  action seems necessary, it's a discussion, not a default.
- **Pin everything the compiler doesn't.** `gh aw compile` SHA-pins actions in the
  `.lock.yml`; for any hand-written steps, pin to a SHA too.

## 2. Scripting

- **Plain Node.js**, run with `node script.js`. **No compiled/bundled JS actions** and no
  `action.yml` wrappers — we want readable scripts, not packaged actions.
- **Minimal/zero dependencies.** Prefer Node built-ins and the `gh` CLI over npm packages.
  If a dep is unavoidable, justify it in review and commit a lockfile.
- **Scripts are deterministic and testable.** Data-gathering lives in scripts (not in the
  agent prompt) so it can be unit-tested and reproduced without a model. (See the
  gather-then-summarize pattern in [02](02-committer-insights.md).)

## 3. Workflow authoring

- **One workflow = one purpose = ideally one safe-output.** No kitchen-sink agents.
- **Source + lock both committed.** Edit the `.md`; run `gh aw compile`; commit both the
  `.md` and the generated `.lock.yml`.
- **Least privilege.** Start from read-only `permissions:`; add scopes only to match the
  declared `safe-outputs`.
- **Start conservative, escalate.** New workflows begin with low-risk outputs
  (`add-comment`, `create-issue`); graduate to `create-pull-request` only after the
  behavior is trusted. PRs are never auto-merged.
- **Ground the agent.** Instructions should tell the agent to base claims on repo/script
  data and to **link** every assertion to a PR/issue/file.

## 4. Secrets

- Secrets come from **repository secrets**, never from workflow-level `env:`.
- Use the minimum token scope the `safe-outputs` require (see
  [06](06-secrets-and-billing.md)).

## 5. File & naming layout

```
.github/workflows/<verb-noun>.md          # + <verb-noun>.lock.yml
scripts/<scenario>/<thing>.js
templates/<report>.md                      # report templates with agentic slots
docs/...                                    # site (see 01)
```

- Workflow names are imperative `verb-noun` (`triage-issues`, `daily-repo-status`).
- Each built workflow has a matching **tutorial page** and links back to its proposal.

## 6. Review process

- Treat workflow `.md` files as **code + prompt + permission boundary**. Review changes to
  them as carefully as a Dockerfile or a CI config.
- Keep workflow edits small and intentional; re-compile and review the `.lock.yml` diff.
- The compiler's scanners (actionlint, zizmor, poutine) run at compile time — keep them
  green.

## Deliverables

- [ ] Encode these as a `CONTRIBUTING.md` / repo `CLAUDE.md` once the first examples land.
- [ ] A PR template reminding authors to commit the recompiled `.lock.yml`.

## Open questions
1. Adopt a `CLAUDE.md`/`AGENTS.md` at the repo root to guide *human + agent* contributors,
   in addition to `CONTRIBUTING.md`?
2. Lint/format tooling for the Node scripts (e.g. `node --test` + Prettier), or keep it
   dependency-free and manual?
