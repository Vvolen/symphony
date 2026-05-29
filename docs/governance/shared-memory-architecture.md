# Shared Memory Architecture for Multi-Agent Work

## Purpose

Create a **shared memory space** that all agents can use without turning the repository into noisy, conflicting notes.

## Design goals

1. Shared visibility for all agents.
2. Low-context overhead via progressive disclosure.
3. Strong provenance (what changed, by whom, and why).
4. Fast handoff across sessions.
5. Safe defaults for secrets and high-risk operations.

## Memory layers

| Layer | Scope | Owner | Retention | Write policy |
| --- | --- | --- | --- | --- |
| `AGENTS.md` | repo-wide constitution | humans + lead agent | durable | conservative, infrequent |
| `docs/governance/*` | policy/protocol | humans + lead agent | durable | PR-reviewed only |
| `docs/memory/INDEX.md` | memory catalog | lead agent | durable | update every meaningful run |
| `docs/memory/runs/*.md` | per-run logs | executing agent | durable | append-only summary + links |
| `docs/memory/decisions/*.md` | ADR/decision records | lead agent | durable | immutable after accepted (new record for changes) |
| `docs/memory/working/*` | scratch pads | executing agent | short/medium | mutable, prune regularly |

## Directory contract

```text
/docs/memory/
  INDEX.md                    # top-level memory map and recent activity
  conventions.md              # writing rules, tags, and status vocabulary
  handoff.md                  # next-agent handoff queue
  runs/
    YYYY-MM-DD-<slug>.md      # run journal with outcomes and evidence
  decisions/
    ADR-YYYY-MM-DD-<slug>.md  # accepted/rejected decisions
  working/
    active-<topic>.md         # temporary synthesis notes
```

## Required entries per run

Every run log in `docs/memory/runs/` must include:

- objective;
- inputs/sources;
- actions taken;
- artifacts changed;
- validation commands and outcomes;
- open risks/unknowns;
- explicit handoff for next agent.

## Anti-conflation rules

1. **One run, one log file** (no giant rolling journal).
2. **No decisions in scratch notes**; promote to `decisions/` only when stable.
3. **No raw secrets** anywhere in memory files.
4. **Use links not duplication**; reference source docs instead of copy/paste.
5. **Close stale working notes** by either promoting, archiving, or deleting.

## Status vocabulary

Use these status tags only:

- `planned`
- `in_progress`
- `blocked`
- `validated`
- `superseded`

## Agent startup checklist

At the start of each task, agents should:

1. Read `AGENTS.md`.
2. Read `docs/memory/INDEX.md` and `docs/memory/handoff.md`.
3. Read only linked run logs relevant to the current objective.
4. Update `docs/memory/handoff.md` before ending if any next action remains.

## Verification checklist

Before closeout, confirm:

- run log added or updated;
- `INDEX.md` updated with latest run;
- handoff queue updated;
- changed files referenced in run log;
- tests/checks recorded.
