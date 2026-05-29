# Research Brief: Copilot for Eclipse, Repo Hydration, and Frontier Agentic Scaffolding

- Date: 2026-05-29
- Question: What should this repo borrow from Copilot for Eclipse, Eclipse governance, GitHub Actions, and Supabase-style backend workflows?
- Decision needed: Which reusable systems should be added now without waiting for the incoming user research folder?

## Executive summary

The highest-leverage finding is that Copilot for Eclipse is converging on the same primitives this repo is already building around: agent mode, custom agents, isolated subagents, planning, MCP, and skills. The stronger move is not to clone Eclipse. It is to borrow the ecosystem pattern: governed platform, explicit roles, extension points, public resources, and review gates.

This repo should become a **hydration platform**: an agent reads a small index, chooses a module, loads only relevant research, executes with scripts/workflows, and writes memory back in a structured run log.

## Source register

| Source | Date accessed | Why it matters |
| --- | --- | --- |
| GitHub Copilot for Eclipse repository | 2026-05-29 | Shows current Eclipse plugin capabilities: completions, next-edit suggestions, agent mode, MCP, custom agents, isolated subagents, Plan Agent, and skills language. |
| GitHub Copilot feature matrix | 2026-05-29 | Confirms which capabilities are supported across IDEs; Eclipse currently supports agent mode, custom agents, MCP, and workspace indexing. |
| GitHub Copilot SDK custom agents docs | 2026-05-29 | Describes custom agents with their own prompts, tool restrictions, optional MCP servers, isolated sub-agent execution, and per-agent skills. |
| GitHub Copilot agent skills docs | 2026-05-29 | Defines skills as folders of instructions/scripts/resources and notes project-scoped `.agents/skills`. |
| Eclipse developer tools page | 2026-05-29 | Frames Eclipse as an ecosystem around developer tools, cloud tools, Open VSX, and IDE governance. |
| Eclipse Project Handbook | 2026-05-29 | Provides durable governance ideas: public resources, roles, review gates, due diligence, and project lifecycle. |
| GitHub Actions docs | 2026-05-29 | Defines repo-native automation for CI/CD and custom workflows. |
| Supabase docs | 2026-05-29 | Shows CLI, migrations, GitHub Actions deployment, and self-hosted/managed tradeoffs for future memory backend. |

## Capability translation

| Found capability | Portable repo pattern |
| --- | --- |
| Custom agents | Maintain role/profile modules for researcher, planner, builder, verifier, archivist. |
| Isolated subagents | Keep task-scoped run logs and role-scoped context bundles. |
| Plan Agent | Require run contracts and plans before long-horizon implementation. |
| MCP | Keep a governed tool registry and gateway pattern. |
| Skills | Package repeatable expertise as `.agents/skills/*`. |
| Eclipse governance | Use a constitution, public memory, roles, review gates, and due-diligence policies. |
| GitHub Actions | Make checks run without manual prompting. |
| Supabase | Future external memory backend with migrations and provenance tables. |

## Pushback / correction

The direction is right, but the repository should not become a warehouse of every cool agent prompt or framework. The better architecture is a curated systems catalog:

- research stays first class but behind indexes;
- systems are promoted only when they have evidence and a validation path;
- live tools are added behind safety boundaries;
- memory is structured as run logs + decisions, not one global blob.

## Applied now

- Added `docs/systems/INDEX.md`.
- Added a Copilot/Eclipse capability map.
- Added a repo hydration architecture.
- Added a GitHub Actions + Supabase playbook.
- Added GitHub-native Copilot instructions.
- Added a GitHub Actions workflow to run `./scripts/check`.

## Next recommendations

1. Extend `scripts/memory-check` to validate handoff/index consistency, not just run-log headings.
2. Add `docs/prompts/queue/` with a YAML task spec once we decide the queue schema.
3. Add `supabase/schema.md` and migrations only after the memory backend table model is accepted.
4. Add agent profile files once we choose which runtime should consume them: Codex, Copilot SDK, Hermes, or a neutral format.
