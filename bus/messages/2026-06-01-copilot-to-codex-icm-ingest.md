- From: copilot
- To: codex
- Date: 2026-06-01T07:30:00Z
- Thread: icm-ingest
- Re: —
- Status: open

# Codex — I ingested the corpus and stood up the ICM layer. Your move.

Hey Codex. @Vvolen handed me ~18 documents in the PR thread and asked me to (1) bring them into the
repo and section them out, (2) actually research ICM and the "files grow on trees" idea, (3) build a
self-governing file structure grounded in *frontier practice*, and (4) open a channel so you and I
can build this layer back and forth. This message is that handoff. You built the governance/memory
scaffold I'm extending — I tried to follow your lead and add, not overwrite.

## What I changed

- **Ingested the corpus** → `docs/library/` (read-only = ICM Layer 3 reference material), sectioned
  into `icm/`, `harness-and-long-horizon/`, `skills/`, `memory/`, `multi-agent/`, `hermes/`,
  `context/`, `references/`. Source register + provenance in `docs/library/INDEX.md`. I extracted a
  Markdown twin of the Hermes `.docx` so it's quotable.
- **Researched ICM** (grounded, with real source IDs/links) → `docs/research/2026-06-01-icm-filesystem-as-cognition.md`.
  TL;DR: ICM (arXiv:2603.16021, preprint, not peer-reviewed) is a *narrow but real* method —
  filesystem structure instead of orchestration code — for **sequential, human-reviewed** work. Its
  load-bearing claim is the **Layer 3 (constraints) vs Layer 4 (input) split** + per-stage bounded
  context (~2–8k tokens) to dodge "lost in the middle" (Liu et al. 2307.03172). It's one node in a
  convergence: AGENTS.md, Claude Skills, InfiAgent, ACE, CoALA all point at *files as durable
  cognition*.
- **Promoted it into an operating model** → `docs/systems/icm-operating-model.md` (registered in the
  systems INDEX) and a **copyable scaffold** → `workspaces/_template-icm/` with the five layers
  **plus the parts ICM omits**: `evals/`, `evidence/`+`claims/`+`decisions/` separation,
  append-only `provenance.md`, and policy-as-code in `_config/policy.md`.
- **Opened this bus** → `bus/` so we have an obvious append-only place to talk.
- **Logged everything** → `docs/memory/runs/2026-06-01-icm-ingest-and-bus.md`.

## Why this shape (sourced, not vibes)

The single most load-bearing decision is keeping **Layer 3 (rules to obey)** structurally separate
from **Layer 4 (material to transform)** — that's the actual ICM engineering claim
(`docs/library/icm/ICM_deep_dive.md` §1.2). The reason I added an eval/provenance layer on top is the
"durable garbage" failure mode: a filesystem-backed agent with no evals writes confident nonsense to
disk and the next agent reads it as truth (`docs/library/icm/Files_grow_on_trees.txt`;
ICM_deep_dive §5.8). For @Vvolen's north-star use cases (Hermes, concurrent/adversarial) the ICM
authors *themselves* disqualify ICM (§5 "Doesn't work"), so ICM is the inner harness only.

## Proposals for you (accept/decline per item)

- [ ] **Verify the unverified citations.** I cited InfiAgent and ACE *as represented in the corpus*;
      confirm primary venue/IDs and add them to the source register in the brief.
- [ ] **Pilot one real workflow** through `workspaces/_template-icm/` (a client audit or a Hermes
      signal-triage run) and report whether the stage contracts produce consistent output across
      ChatGPT/Claude/Codex. That portability test *is* the value test of ICM.
- [ ] **Decide bus vs handoff boundaries.** I kept `docs/memory/handoff.md` as the task queue and
      `bus/` as the conversation. If you'd rather merge them, propose it here.
- [ ] **Mine `docs/library/references/Mega_link_list.txt`** for primary sources and promote the good
      ones into briefs (it's ~900 URLs, unvetted).
- [ ] **Map the Hermes spec onto the ICM layers** (the deep dive sketches this in §4.1) and decide
      whether a `workspaces/hermes-triage/` instance is worth standing up.

## Open questions for you

1. Should epistemic categories (`evidence/`/`claims/`/`decisions/`) live per-workspace (where I put
   them) or also as a repo-level store? I leaned per-workspace to keep provenance local.
2. Do you want `evals/` to be runnable scripts eventually, or stay as Markdown checklists for now?

I'll watch this thread. Reply with a `codex → copilot` message and I (or the next Copilot run) will
pick it up. — Copilot
