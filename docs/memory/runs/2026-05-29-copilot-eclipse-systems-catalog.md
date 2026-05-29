# Run: copilot-eclipse-systems-catalog

- Date: 2026-05-29
- Status: validated

## Objective

Mine Copilot for Eclipse and adjacent GitHub/Supabase capabilities for high-leverage repo systems, then add a discoverable systems catalog and hydration scaffolding.

## Context and sources

- Microsoft `copilot-for-eclipse` repository.
- GitHub Copilot custom agents, skills, and feature matrix docs.
- Eclipse developer tools and project governance docs.
- GitHub Actions docs.
- Supabase CLI, GitHub Actions, migrations, and self-hosting docs.

## Actions

- Added a systems catalog under `docs/systems/`.
- Added GitHub Copilot repository instructions in `.github/copilot-instructions.md`.
- Added a GitHub Actions workflow to run `./scripts/check`.
- Added a source-grounded research brief for Copilot/Eclipse/repo hydration.

## Files changed

- `.github/copilot-instructions.md`
- `.github/workflows/research-hub-check.yml`
- `docs/systems/INDEX.md`
- `docs/systems/copilot-eclipse-capability-map.md`
- `docs/systems/repo-hydration-architecture.md`
- `docs/systems/github-actions-and-supabase-playbook.md`
- `docs/research/2026-05-29-copilot-eclipse-and-repo-hydration.md`
- `docs/memory/runs/2026-05-29-copilot-eclipse-systems-catalog.md`
- `scripts/memory-check`

## Validation

- `./scripts/check` passed.
- `./scripts/memory-check` passed.
- `./scripts/doctor` passed.

## Risks / unknowns

- Exact Copilot custom-agent file formats differ by runtime; keep role profiles neutral until a target runtime is selected.
- Supabase should remain docs-only until secrets, project refs, and access boundaries are defined.

## Handoff

- Decide whether the first prompt queue should live under `docs/prompts/queue/` or `.agents/queue/`.
- Extend `scripts/memory-check` to validate handoff/index consistency.
