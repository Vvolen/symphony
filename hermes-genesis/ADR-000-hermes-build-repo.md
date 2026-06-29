# ADR-000: Build the Hermes Solana Edge OS in a dedicated private repository

- **Status:** Proposed (awaiting confirmation)
- **Date:** 2026-06-29
- **Decision owner:** Nick
- **Supersedes:** —

## Context

The planning and research corpus currently lives in a fork of `openai/symphony` (the "research
hub"). Two problems with building the product there:

1. **Opsec.** It is a fork of a *public* repository. Forks of public repos are public by default,
   which likely makes the operator dossier (`MASTER_CONTEXT.md`) and the full trading spec
   world-readable. (Confirm in repo Settings → visibility.)
2. **Architectural muddiness.** The fork carries an entire upstream Elixir "Symphony" orchestration
   implementation that is unrelated to Hermes. Building the product on top of someone else's
   framework fork mixes your IP with upstream and makes the system harder for an agent to reason
   about.

Separately, the build deserves a clean software-development-life-cycle start: a purpose-written
constitution (`AGENTS.md`), an `/agent` workspace, and ADRs from commit #1.

## Decision

- Create a **new, private repository** as the home for the Hermes Solana Edge OS build.
- Keep the `symphony` fork as the **research / governance library** (the reading room), not the
  workshop.
- Carry over only the reusable discipline and assets — see `PORT_LIST.md`; leave the upstream
  framework behind.
- Seed the new repo with this genesis packet as its spine.

## Consequences

**Positive:** removes the opsec exposure; clean constitution and history; the build is legible to
Hermes and to coding agents; the research library stays intact and separately useful.

**Negative / cost:** a one-time setup step (create repo, port ~6 assets); discipline required to
port deliberately rather than copy everything.

## Alternatives considered

- **Build in the existing fork.** Rejected: opsec exposure + upstream baggage + muddy ownership.
- **Start fully from scratch, abandon the hub.** Rejected: throws away genuinely good library work
  (governance docs, the research-brief skill, ICM discipline, the corpus).
