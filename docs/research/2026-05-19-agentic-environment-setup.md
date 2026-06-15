# Research Brief: Codex Cloud as an Agentic Research and Governance Environment

- Date: 2026-05-19
- Freshness window: Prefer April-May 2026 sources for fast-moving agent tooling.
- Question: How should this Symphony fork be set up as a powerful, source-grounded environment for long-horizon AI research and agent orchestration?
- Decision needed: What repo scaffolding should exist before wiring external tools, Hermes agents, Firecrawl, MCP gateways, and domain-specific trading research?

## Executive summary

This environment can be treated as a durable research-and-build hub if the persistent state lives in files, skills, scripts, and governed external services rather than in chat memory alone. The strongest setup is layered: `AGENTS.md` for policy, repo-scoped skills for repeatable workflows, scripts for deterministic checks, environment variables and secrets for configuration, and MCP/gateway tools for live external capabilities.

The immediate recommendation is to keep Symphony intact, add a repo-level research/governance hub, and use this fork as the operating base until a dedicated repo is justified.

## Source register

| Source | Date | Type | Link / locator | Why it matters |
| --- | --- | --- | --- | --- |
| OpenAI Codex Cloud environments | Current docs accessed 2026-05-19 | Primary docs | https://developers.openai.com/codex/ | Defines setup scripts, env vars, secrets, cache, and cloud task lifecycle. |
| OpenAI Codex Skills docs | Current docs accessed 2026-05-19 | Primary docs | https://developers.openai.com/codex/skills/ | Defines skills, progressive disclosure, repo/user/admin/system skill locations, and best practices. |
| OpenAI Codex MCP docs | Current docs accessed 2026-05-19 | Primary docs | https://developers.openai.com/codex/mcp/ | Defines MCP configuration, env forwarding, HTTP/stdio transports, tool allow/deny lists, and approval modes. |
| OpenAI Codex use cases | Current docs accessed 2026-05-19 | Primary docs | https://developers.openai.com/codex/ | Establishes Codex as useful for data analysis, research, durable goals, skills, and production-system work. |
| OpenAI Codex releases | 2026-05-18 latest release visible | Primary repository release page | https://github.com/openai/codex/releases | Shows active app-server, environment, daemon, plugin, and goal-related development. |
| OpenAI Skills catalog | Current GitHub repo accessed 2026-05-19 | Primary repository | https://github.com/openai/skills | Shows the official skill catalog and installation model. |
| OpenAI Codex MCP + Agents SDK cookbook | Current docs accessed 2026-05-19 | Primary cookbook | https://cookbook.openai.com/ | Demonstrates Codex CLI exposed as MCP for single- and multi-agent workflows with traceability. |
| Firecrawl Hermes guide | 2026-04-24 | Vendor guide | https://www.firecrawl.dev/ | Describes Hermes persistence, Firecrawl backend, MCP extension points, skills, and messaging gateways. |
| Hermes release digest | May 2026 | Release aggregation | `/home/runner/work/symphony/symphony/docs/library/harness-and-long-horizon/deep-research-report-3.md` | Gives recent Hermes v0.12 self-improvement loop and cold-start changes; treat as secondary until verified against upstream commits. |
| Skilldex paper | 2026-04 | Research paper | `/home/runner/work/symphony/symphony/docs/library/harness-and-long-horizon/deep-research-report-3.md` | Frames skills as runtime packages with registries, conformance scoring, skillsets, and MCP support. |
| Confidential computing for agents survey | 2026-05 | Research paper | `/home/runner/work/symphony/symphony/docs/library/harness-and-long-horizon/deep-research-report-3.md` | Frames the threat surface for agents with secrets, memory, peer delegation, MCP/A2A, and exfiltration risks. |

## Claims and evidence

| Claim | Evidence | Confidence | Notes |
| --- | --- | --- | --- |
| Codex cloud environments can install tools, set env vars, and run setup scripts. | OpenAI says environments control what Codex installs/runs, including dependencies, tools, and environment variables. | High | Primary docs. |
| Codex cloud tasks run in containers with repo checkout, setup scripts, optional maintenance scripts, then agent command loops. | OpenAI documents the cloud task lifecycle and notes AGENTS.md is used for project-specific lint/test commands. | High | Primary docs. |
| Codex secrets are intentionally narrower than environment variables. | OpenAI says secrets are additionally encrypted and only available during setup; they are removed before the agent phase. | High | Important for Firecrawl/Hermes/tool credential design. |
| Setup-script `export` is not durable into the agent phase. | OpenAI notes setup scripts run in a separate Bash session; persistent variables should be in environment settings or startup files. | High | Prevents a common setup mistake. |
| Skills are the right unit for packaged expertise. | OpenAI defines skills as instructions/resources/scripts that Codex can use reliably and says skills use progressive disclosure. | High | Primary docs. |
| Too many skills can still create context pressure. | OpenAI caps the initial skills list and shortens descriptions when many skills are installed. | High | Supports a curated skill registry rather than dumping everything in. |
| MCP is the right layer for live external tools. | OpenAI says MCP gives Codex access to third-party tools/context, supports stdio and HTTP, and allows env vars, auth, tool allow/deny lists, and approval modes. | High | Primary docs. |
| Long-horizon work should be goal-driven and verifiable. | OpenAI's use cases include durable goals, scored improvement loops, repeatable operations, and saving workflows as skills. | Medium-high | Official use-case page; exact `/goal` availability depends on client/version. |
| Hermes is plausibly useful as an external persistent agent layer. | Firecrawl describes Hermes as persistent, skill-writing, model-agnostic, MCP-extensible, and able to run on remote VMs via messaging gateways. | Medium | Vendor source; verify upstream before production deployment. |
| Agents with secrets and peer delegation need explicit threat modeling. | A May 2026 survey identifies prompt injection, exfiltration, credential theft, and inter-agent message poisoning as agent-specific risks. | High | Research paper; use for security posture. |

## Analysis

The frontier pattern is not one magic tool. It is a layered harness:

1. **Policy as code**: `AGENTS.md`, workflow docs, and checked-in governance make future agent runs consistent.
2. **Packaged expertise**: skills provide reusable workflows without loading every detail up front.
3. **Deterministic helpers**: scripts reduce repeated fragile shell work.
4. **Live tool access**: MCP servers and gateways expose external systems without baking every API into prompts.
5. **Durable memory**: Git docs, external memory stores, and research artifacts persist across sessions better than chat context.
6. **Verification loops**: tests, trace/eval tools, source registers, and verifier agents reduce hallucination and drift.

The transcript's peer-to-peer agent communication idea fits this model as an advanced pattern, not the first primitive. Use it when agents truly hold different context or authority. For example, a production-sanitizer agent and a dev-reproducer agent benefit from direct two-way communication because neither should fully own the other's context.

## Recommendation

Use this Symphony fork as the initial operating base. Keep upstream Symphony under `elixir/` untouched except when intentionally contributing to it. Add a top-level research hub, governance docs, `.env.example`, repo-scoped skills, and low-risk scripts. Then wire external capabilities in phases:

1. Firecrawl/API research tooling.
2. MCP registry and gateway pattern.
3. Hermes VPS agents with isolated profiles and least-privilege credentials.
4. Domain corpus ingestion and retrieval for Solana data aggregation research.
5. Peer-to-peer agent communication only after logging, redaction, and stop conditions are designed.

## Risks and unknowns

- `/goal` appears in current Codex ecosystem materials, but this cloud session does not expose an interactive Codex CLI binary to me directly. Treat goal mode as a client feature to configure/test in your local Codex app/CLI environment.
- Hermes claims should be verified against the upstream repo before production or trading-adjacent deployment.
- Firecrawl and MCP tools should start read-only. Mutating tools need approvals, logs, and allow lists.
- Trading workflows are financially sensitive. Keep the system as data aggregation and decision support unless/until risk controls are explicit.

## Next actions

1. Add Firecrawl variables in the Codex environment rather than committing secrets.
2. Create a tool registry before wiring 25 MCP servers.
3. Build a Hermes VPS runbook with profiles, systemd/Docker choice, logs, backup, and secrets strategy.
4. Add a domain-specific Solana research corpus structure after you point this repo at your existing materials.
