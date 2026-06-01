# Systems Catalog

This catalog is the front door for reusable long-horizon systems, reference architectures, agent constellations, and tool scaffolds.

## How to use this catalog

1. Start here, not in a random research brief.
2. Pick the system that matches the task.
3. Read only that module plus its linked sources.
4. Record changes in `docs/memory/runs/` when a system is applied.

## Current modules

| Module | Use when | Status |
| --- | --- | --- |
| [`icm-operating-model.md`](icm-operating-model.md) | Organizing long-horizon, multi-stage work as filesystem structure (ICM Layers 0–4) plus the eval/provenance layers ICM omits. | active |
| [`copilot-eclipse-capability-map.md`](copilot-eclipse-capability-map.md) | Mining Copilot for Eclipse / Eclipse governance for agentic architecture ideas. | researched |
| [`repo-hydration-architecture.md`](repo-hydration-architecture.md) | Designing this repo so any agent can hydrate into a long-horizon task quickly. | active |
| [`github-actions-and-supabase-playbook.md`](github-actions-and-supabase-playbook.md) | Adding repo-native automation, GitHub Actions, and Supabase/memory backend scaffolding. | planned |

## Procurement rule

A module is not adopted just because it is exciting. It needs:

- clear capability;
- source evidence;
- local fit;
- safety boundary;
- validation path;
- owner or next action.
