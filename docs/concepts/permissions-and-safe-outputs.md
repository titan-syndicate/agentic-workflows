# Permissions & safe outputs

!!! info "Intro tier"
    This is the heart of the security model and the part most worth understanding before you
    build anything.

## What this page will cover

- **Read-only by default.** The agent job runs with read permissions. It cannot directly
  write to your repo.
- **`safe-outputs` are the only way to write.** You declare the specific operations the
  agent is allowed to *propose* — e.g. `create-issue`, `add-comment`,
  `create-pull-request`, `add-labels`. These execute in **separate jobs after** a
  threat-detection scan passes.
- **PRs are never auto-merged.** A human reviews and merges.
- **The catalog is large** (~40 output types across issues, PRs, discussions, projects,
  releases, labels, files, security alerts). Common config keys: `title-prefix`, `labels`,
  `max`, `target`, `target-repo`/`allowed-repos`.

### Example
```yaml
permissions:
  contents: read
  issues: read
safe-outputs:
  create-issue:
    title-prefix: "[repo-status] "
    labels: [report]
    max: 1
```

See the full catalog in the [reference](../reference/frontmatter-schema.md).
