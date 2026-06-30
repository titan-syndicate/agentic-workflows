# Anatomy of a workflow

!!! info "Intro tier"
    Every agentic workflow is one Markdown file with two halves.

## What this page will cover

- **Frontmatter** (YAML between `---`): when it runs (`on:`), what it may touch
  (`permissions`, `safe-outputs`), which engine and tools it uses.
- **Body** (Markdown): the natural-language instructions the agent follows.
- **The compile step**: `gh aw compile` turns the `.md` into a hardened, SHA-pinned
  `.lock.yml`. Both files are committed; the `.lock.yml` is what Actions executes.
- **Why two files**: the `.md` is the human-editable source of truth; the `.lock.yml` is
  the reviewable, audited artifact.

### Minimal example
```markdown
---
on:
  issues:
    types: [opened]
permissions:
  contents: read
  issues: read
safe-outputs:
  add-comment:
engine: copilot
tools:
  github:
    toolsets: [issues]
---

# Triage greeter
Welcome the issue author and suggest the most relevant label. Keep it to two sentences.
```
