# Self-hosted runners

!!! abstract "Expert tier"
    Considerations for running agentic workflows on your own infrastructure rather than
    GitHub-hosted runners.

## What this page will cover

- Pointing a workflow at self-hosted runners via `runs-on:` labels.
- Container + Docker requirements the AWF depends on (the firewall assumes a container
  runtime and iptables/proxy capability).
- Network posture — reconciling the Agent Workflow Firewall's default-deny egress with
  your own proxy/egress controls.
- Secret handling and isolation expectations on shared self-hosted fleets.
- When self-hosting is worth it (data residency, custom toolchains) vs. the simplicity of
  GitHub-hosted runners.

!!! note
    Lower priority for the initial examples (we target GitHub-hosted runners first), but
    captured here because runner admins will ask.
