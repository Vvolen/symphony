# ICM Operating Model (repo adaptation)

- Status: active
- Use when: standing up any long-horizon, multi-stage workflow in this repo, or deciding where a
  piece of context belongs.
- Source of truth: `docs/research/2026-06-01-icm-filesystem-as-cognition.md` and
  `docs/library/icm/` (ICM_deep_dive, Files_grow_on_trees).

## What this is

ICM (Interpretable Context Methodology, arXiv:2603.16021) organizes an agent's work as
**filesystem structure** instead of framework code: numbered stage folders plus plain-Markdown
context files. This module adapts ICM's *load-bearing* parts to this repo and adds the layers ICM
deliberately omits (evals, evidence/claim separation, provenance, policy).

We treat ICM as the **inner harness** (how a single agent loads its slice of context) and Symphony +
this governance hub as the **outer harness** (orchestration, memory, handoff, policy).

## The layer model

| Layer | Question | In this repo | Changes per run? |
| --- | --- | --- | --- |
| 0 — Identity | "Where am I?" | `AGENTS.md`, `docs/library/context/MASTER_CONTEXT.md` | No |
| 1 — Routing | "Where do I go?" | `docs/systems/INDEX.md`, `docs/memory/INDEX.md`, a workspace `routing.md` | No |
| 2 — Stage contract | "What do I do here?" | `stages/NN-name/CONTEXT.md` (inputs, process, outputs) | No |
| 3 — Reference (the *factory*) | "What rules apply?" | `docs/governance/`, `docs/library/`, workspace `_config/` + `references/` | No |
| 4 — Working artifacts (the *product*) | "What am I working with?" | workspace `stages/NN-name/output/` | **Yes** |

**The one rule that carries the method:** keep Layer 3 (constraints to obey) structurally separate
from Layer 4 (material to transform). Most failures come from collapsing the two into one mega-prompt.

## What is load-bearing vs decorative

Load-bearing (keep): the Layer 3/4 split; each stage loads only what it needs (~2–8k tokens);
every intermediate output is an editable file; explicit stage contracts; human review between stages.

Decorative (taste): numbered folder names; Markdown specifically (JSON/YAML are fine); the exact
"five layers" framing; the `CLAUDE.md` filename (we use `AGENTS.md` for cross-tool portability).

## The five-rung ladder (where work sits)

1. Files as storage → 2. Files as memory → 3. **Files as context routing (ICM)** →
4. Files as control plane (stage contracts, eval gates, policy-as-code) →
5. Files as separated epistemic categories (evidence ≠ claim ≠ decision ≠ hypothesis).

ICM is rung 3. This repo targets rungs 4–5 because its north-star use cases are concurrent and
adversarial.

## What we add on top of ICM (non-optional)

ICM has no eval, governance, or provenance discipline. A filesystem-backed agent with no evals
writes confident nonsense to disk and the next agent reads it as truth ("durable garbage", see
`docs/library/icm/Files_grow_on_trees.txt`). So every ICM workspace here also carries:

- `evals/` — acceptance checks per stage, machine-checkable where possible.
- `evidence/` vs `claims/` vs `decisions/` — separated epistemic categories for stakes-bearing work.
- `provenance` — append-only log of any externally retrieved content; retrieved content is untrusted
  and must never merge with system instructions (memory-poisoning defense).
- policy-as-code — allowlists/thresholds expressed as Layer 3 constraints.

## How to use it

1. Copy `workspaces/_template-icm/` to `workspaces/<your-workflow>/`.
2. Fill `identity.md` (L0) and `routing.md` (L1) once.
3. For each stage, write a tight `stages/NN-name/CONTEXT.md` (L2) — the stage contract is the edge.
4. Put rules/voice/doctrine in `_config/` and `references/` (L3); write run output to `output/` (L4).
5. Gate each stage on `evals/`; record sources in `provenance`.
6. Log the run in `docs/memory/runs/` and update `docs/memory/handoff.md`.

## Boundaries

- Apply ICM only to genuinely long-horizon, multi-stage work; do not over-structure one-shot tasks.
- ICM does not replace orchestration. For concurrent/multi-agent work, ICM governs each agent's
  internal context; the event bus and council live above it (see `docs/library/multi-agent/multi_agent_stack.md`).
- ICM is a preprint, not consensus; cite it as a frontier pattern, not settled doctrine.
