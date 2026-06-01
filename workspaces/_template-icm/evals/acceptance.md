# Evals — per-stage acceptance checks

> ICM has no eval discipline; this repo adds one. A stage may not advance until its row passes.
> Prefer machine-checkable conditions (Tier 1). Use expert review (Tier 2) only where needed.

| Stage | Acceptance check | Tier |
| --- | --- | --- |
| 01 intake | `output/intake.md` exists and states goal, constraints, stop condition, validation loop | 1 |
| 02 evidence | every claim in `output/evidence.md` has a matching entry in `../provenance.md` | 1 |
| 02 evidence | evidence is separated from claims (no unsourced assertions) | 2 |
| 03 synthesis | `output/result.md` exists; facts/inference/recommendation are separated | 2 |
| 03 synthesis | each consequential choice is logged in `../decisions/` | 1 |
| all | no real secrets present (`scripts/check` is clean) | 1 |

## How to run

- Tier 1 rows should be verifiable by inspection or a script.
- Tier 2 rows require a human (or a separate judge agent) review before sign-off.
