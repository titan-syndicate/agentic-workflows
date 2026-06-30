# Tools & MCP

!!! abstract "Expert tier"
    What the agent can *do* during a run — read the repo, run shell, fetch the web, or call
    your own services over MCP.

## What this page will cover

- **GitHub toolset** — `tools.github.toolsets: [issues, pull_requests, repos, ...]`, with
  `min-integrity` filtering and per-tool `max-calls` limits.
- **Built-in tools** — `bash` (allowlisted commands or wildcards), `web-fetch`,
  `web-search`, `edit`, `playwright`, `cache-memory`.
- **Custom MCP servers** (`mcp-servers:`) — the multi-step "agent uses tools" pattern.
  Three transports:

  ```yaml
  mcp-servers:
    stdio-server:
      command: "npx"
      args: ["-y", "@org/mcp-server"]
      env: { API_KEY: "${{ secrets.API_KEY }}" }
      allowed: ["tool_a", "tool_b"]
    http-server:
      url: "http://localhost:3000"
      headers: { Authorization: "Bearer ${{ secrets.TOKEN }}" }
    docker-server:
      container: "myorg/mcp-image:latest"
  ```

- **Isolation** — MCP servers run in isolated Docker containers; egress is mediated by the
  firewall's MCP gateway. Helpers: `gh aw mcp list|inspect|add`.

This is the concept behind the [tool-using agents tutorial](../tutorials/tool-using-agents.md).
