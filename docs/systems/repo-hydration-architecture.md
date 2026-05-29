# Repo Hydration Architecture

## Goal

Let any capable agent enter the repository, understand the operating system quickly, and gear up for a long-horizon task without loading the whole repo into context.

## Hydration path

Agents should hydrate in this order:

1. `AGENTS.md` — constitution and safety defaults.
2. `docs/memory/INDEX.md` — current priorities and active threads.
3. `docs/memory/handoff.md` — immediate next actions and blockers.
4. `docs/systems/INDEX.md` — reusable systems and modules.
5. Relevant module docs only.
6. Relevant research briefs only.
7. Source files or implementation areas.

## Information architecture

| Directory | Role | Load policy |
| --- | --- | --- |
| `docs/systems/` | reusable modules and playbooks | read index first, then one module |
| `docs/research/` | source-grounded background research | read only when module links to it |
| `docs/memory/` | current state, handoff, run history | read index + handoff every run |
| `.agents/skills/` | packaged expertise | trigger by task, not by default |
| `.github/` | GitHub-native automation and Copilot config | read when working on GitHub workflows/agents |
| `scripts/` | deterministic local checks | run instead of retyping commands |

## Prompt queue direction

Future prompt-queue entries should be small YAML or Markdown files that point to modules instead of embedding large prompts.

Suggested shape:

```yaml
id: 2026-05-29-example
objective: "Build X"
modules:
  - docs/systems/repo-hydration-architecture.md
  - docs/systems/github-actions-and-supabase-playbook.md
skills:
  - research-brief
validation:
  - ./scripts/check
stop_condition: "PR opened with checks recorded"
```

## Anti-patterns

- Do not create a giant all-purpose MEMORY.md.
- Do not duplicate research into every module.
- Do not let scratch notes become decisions.
- Do not wire live external tools before documenting their safety boundary.
