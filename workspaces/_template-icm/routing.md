# Routing (ICM Layer 1) — "Where do I go?"

> Maps event/task classes to the stage that handles them. Keep stable. Each stage loads only its own
> `CONTEXT.md` plus the references that stage names — never the whole repo.

## Stage pipeline

| # | Stage | Handles | Reads (L3) | Writes (L4) |
| --- | --- | --- | --- | --- |
| 01 | `stages/01-intake/` | Frame the task, restate the goal, list constraints and the stop condition | `_config/`, `references/` | `output/intake.md` |
| 02 | `stages/02-evidence/` | Gather sources; record each in `provenance.md`; separate evidence from claims | `_config/policy.md`, `references/` | `output/evidence.md` |
| 03 | `stages/03-synthesis/` | Produce the artifact; pass `evals/acceptance.md`; record decisions | prior `output/`, `_config/` | `output/result.md` |

## Routing rules

- Advance to stage N+1 only after stage N passes `evals/acceptance.md`.
- A human reviews each stage's `output/` between stages (ICM is human-in-the-loop by design).
- If a stage produces a claim with real-world stakes, write it to `claims/` and its support to
  `evidence/`; only promote to `decisions/` after verification.
