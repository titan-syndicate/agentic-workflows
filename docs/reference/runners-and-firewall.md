# Runners & the Agent Workflow Firewall

!!! abstract "Expert tier"
    For the people who run the runners. How agentic workflows execute and how their network
    access is contained.

## What this page will cover

- **Runtime model** — agents run inside firewalled Docker containers on Actions runners.
  Default `ubuntu-latest`; `runs-on-slim` (`ubuntu-slim`) for framework/safe-output jobs.
  No special larger runner required; `runs-on` accepts custom/self-hosted labels.
- **Agent Workflow Firewall (AWF)** — egress control via containerization + iptables
  redirect through a Squid proxy. Default-deny; allowlist by domain or ecosystem:

  ```yaml
  network:
    firewall: true
    allowed: [defaults, node, python, "api.example.com"]
  ```

- **MCP gateway** — mediates MCP server egress.
- **Service containers** — `services:` ports bind on the runner host (not the agent
  container); reach them via `host.docker.internal`.
- **Job orchestration** — how the pre-activation, agent, detection, and safe-output jobs
  are scheduled.
