---
title: Your first run
layout: default
parent: Getting started
nav_order: 3
audience: intro
---

# Your first run
{: .no_toc }

{: .tryit }
> Author a tiny workflow, compile it, commit, and watch it run.

## What this page will cover

1. **Author** `.github/workflows/hello.md` — minimal frontmatter (`on:`, `permissions`,
   `safe-outputs: add-comment`) plus a one-paragraph instruction.
2. **Compile**: `gh aw compile hello` → produces `hello.lock.yml`.
3. **Commit both files** to the default branch.
4. **Run it**: `gh aw run hello` (or trigger its event), then inspect with
   `gh aw logs hello` and `gh aw audit <run-id>`.
5. **Read the output**: where the agent's comment/issue shows up, and how the
   threat-detection + safe-output jobs gate the write.

{: .note }
> `gh aw trial <workflow> --dry-run` lets you test in a throwaway/private repo before
> committing to a real one.
