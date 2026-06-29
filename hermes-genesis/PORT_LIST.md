# Port List — from the `symphony` research hub into the Hermes build repo

The research hub is a good *library*. Carry the reusable discipline and assets; leave the framework
and the fork.

## Carry over

| Asset (in `symphony`) | Becomes (in build repo) | Why |
|---|---|---|
| ICM operating model (`docs/systems/icm-operating-model.md`) | Context-engineering discipline: SOUL/AGENTS/policies = static Layer 3; per-task files = dynamic Layer 4 | Same idea Google / Anthropic call context engineering; Hermes already embodies it |
| Governance docs (`docs/governance/*`) | Your `AGENTS.md` constitution + `action_radius` / tool-registry policy | Practical, behavior-changing policy — not theory |
| `research-brief` skill (`.agents/skills/research-brief`) | A Hermes skill | Source-grounded research workflow, directly reusable |
| ICM workspace template (`workspaces/_template-icm/`) | The `/agent` workspace pattern (mission / state / tasks / evidence / decisions / handoff) | Filesystem-as-cognition scaffold |
| Handoff + bus conventions (`docs/memory/*`, `bus/`) | Multi-agent coordination + handoff packets | How agents hand off without losing context |
| Hermes corpus (`docs/library/`) | Reference library (read-only) | The source material; cite, don't rewrite |

## Leave behind

- The upstream **Elixir Symphony** implementation — not yours, not relevant to Hermes.
- The **fork relationship** itself — start clean and private (opsec).
- Any **branded methodology kept for its own sake** — keep only what changes agent behavior.

## Note

Porting = *re-deciding each item is worth it*, not bulk-copying. If an asset does not earn its place
in the build repo, it stays in the library.
