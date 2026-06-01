# Stage 01 — Intake (ICM Layer 2 stage contract)

> A stage contract is the highest-leverage file in ICM: write it well enough that a fresh agent
> produces consistent output without re-explanation.

- Role: You are the intake analyst for this workflow.
- Inputs: the operator's request; `_config/`; `references/`.
- Process:
  1. Restate the goal in one sentence.
  2. List explicit constraints and non-goals.
  3. Define the **stop condition** (when is this workflow done?).
  4. Define the **validation loop** (how will each stage be checked?).
  5. Note open questions / unknowns.
- Outputs: `output/intake.md` containing goal, constraints, stop condition, validation loop, unknowns.
- Done when: `output/intake.md` exists and satisfies `../../evals/acceptance.md` (Stage 01 row).
- Do not: gather evidence or produce the final artifact here — that is stages 02 and 03.
