# Run: icm-ingest-and-bus

- Date: 2026-06-01
- Status: validated
- Agent: Copilot (GitHub Copilot coding agent), for @Vvolen

## Objective

Ingest ~18 user-provided documents into the repo and section them out; research ICM and the
"filesystem-as-cognition" idea against frontier practice; stand up a self-governing ICM file
structure; and open an obvious append-only channel for Copilot↔Codex collaboration.

## Context and sources

- User corpus (now under `docs/library/`), especially `icm/ICM_deep_dive.md` and
  `icm/Files_grow_on_trees.txt`.
- Primary anchors cited in the brief: ICM arXiv:2603.16021; Liu et al. "Lost in the Middle"
  arXiv:2307.03172; AGENTS.md convention; Claude Skills; CoALA arXiv:2309.02427; InfiAgent and ACE
  (as represented in the corpus, IDs pending verification).

## Actions

- Ingested the corpus into `docs/library/` with topic sections and a source register
  (`docs/library/INDEX.md`); extracted a Markdown twin of the Hermes `.docx`.
- Added grounded research brief `docs/research/2026-06-01-icm-filesystem-as-cognition.md`.
- Added systems module `docs/systems/icm-operating-model.md` and registered it in
  `docs/systems/INDEX.md`.
- Added copyable ICM scaffold `workspaces/_template-icm/` (5 layers + evals/evidence/claims/
  decisions/provenance/policy).
- Opened the agent bus `bus/` with protocol + first message (Copilot → Codex).
- Cross-linked from `AGENTS.md`, `docs/memory/INDEX.md`, and `docs/memory/handoff.md`.
- Updated `scripts/check`: added new required files; fixed the over-escaped Firecrawl secret regex.

## Files changed

- `docs/library/**` (corpus + `INDEX.md`)
- `docs/research/2026-06-01-icm-filesystem-as-cognition.md`
- `docs/systems/icm-operating-model.md`, `docs/systems/INDEX.md`
- `workspaces/**` (`README.md` + `_template-icm/**`)
- `bus/**`
- `AGENTS.md`, `docs/memory/INDEX.md`, `docs/memory/handoff.md`
- `scripts/check`
- `docs/memory/runs/2026-06-01-icm-ingest-and-bus.md`

## Validation

- `./scripts/check` passed.
- `./scripts/memory-check` passed.
- `./scripts/doctor` passed.

## Risks / unknowns

- ICM is a preprint, not peer-reviewed; cite as a frontier pattern, not consensus.
- InfiAgent/ACE citation IDs are unverified (flagged in the brief for Codex to confirm).
- The `.docx` is binary; the `.md` twin is the source of truth for quoting.
- Filesystem-backed agents without evals risk "durable garbage"; the added `evals/`+provenance layer
  is the mitigation and must be used, not just present.

## Handoff

- See `bus/messages/2026-06-01-copilot-to-codex-icm-ingest.md` for the proposal list to Codex.
- Next: verify citations, pilot one workflow through the template, decide bus/handoff boundaries.
