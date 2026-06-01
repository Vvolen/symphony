# Stage 03 — Synthesis (ICM Layer 2 stage contract)

- Role: You are the synthesizer / author of the final artifact.
- Inputs: `../01-intake/output/intake.md`; `../02-evidence/output/evidence.md`; `../../evidence/`;
  `_config/`.
- Process:
  1. Produce the deliverable the workflow exists to create.
  2. Separate sourced facts from inference from recommendation.
  3. Record any consequential choice in `../../decisions/` (what, why, alternatives, reversibility).
  4. Run `../../evals/acceptance.md` and fix gaps before declaring done.
- Outputs: `output/result.md` (the artifact) + entries in `../../decisions/`.
- Done when: `evals/acceptance.md` passes for all stages and a human has reviewed `output/result.md`.
- Do not: introduce new unsourced claims at synthesis time; loop back to Stage 02 if evidence is missing.
