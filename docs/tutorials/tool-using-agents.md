# Tool-using agents

!!! abstract "Expert tier"
    Beyond one-shot summarization: workflows where the agent calls **tools** in a multi-step
    loop, including custom MCP servers you provide.

## What this walkthrough will cover

- The difference between *gather-then-summarize* and *agent-drives-the-tools*.
- Several example shapes:
  - GitHub toolset in a reasoning loop (search → read → act).
  - A **custom MCP server** (small Node stdio server) exposing domain tools.
  - An HTTP MCP server the agent queries.
- **Test infrastructure options** (decision deferred — see proposal): in-repo mock MCP +
  canned data, a cheap live host, or an ephemeral service started in the runner.
- Firewall/egress implications of letting an agent call out.

Maps to proposal
[`04-tool-using-agents`](https://github.com/titan-syndicate/agentic-workflows/blob/main/docs/proposals/04-tool-using-agents.md).
