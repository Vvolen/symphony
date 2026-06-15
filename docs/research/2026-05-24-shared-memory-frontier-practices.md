# Research Brief: Shared Memory Patterns Used by Frontier Agentic Teams

- Date: 2026-05-24
- Question: What shared-memory patterns are practitioners using successfully for multi-agent engineering and long-horizon coding/research?
- Scope: production-adjacent patterns that can be applied inside this repository immediately.

## Executive summary

Teams operating frontier coding agents tend to converge on a layered memory model:

1. **always-loaded project policy file** (constitution);
2. **task-scoped run logs** with strict schemas;
3. **decision records** for stable architecture choices;
4. **scratch/working notes** with pruning discipline;
5. **tool-level traceability** (tests, command logs, artifacts).

This model reduces context bloat while preserving continuity across sessions and agents.

## What is working in practice

### 1) Path-scoped memory + progressive disclosure

Production users of coding agents rely on memory files loaded by directory scope and keep them concise. They avoid putting everything in one giant prompt and instead use lightweight top-level memory plus deeper, opt-in references.

### 2) Deterministic run artifacts

High-performing teams keep per-run logs with fixed sections (objective, changes, checks, risks, handoff). This creates auditable traces and supports rapid takeover by another agent.

### 3) Decision records over mutable tribal knowledge

Architecture decisions are written as immutable ADR-like docs. If a decision changes, a new record is created instead of rewriting history.

### 4) Verification-first workflow

Reliable teams require explicit validation commands and outcomes in run logs, not just a claim that work was done.

### 5) Security boundaries for shared memory

Shared memory is treated as potentially exfiltratable text. Secrets and production credentials are never written; references point to secret-management systems instead.

## `/goal` note

The `/goal` workflow is widely discussed as a durable objective mechanism in current coding-agent practice. In this cloud session, exact command availability is client-dependent. The right approach is to verify locally in the user's Codex app/CLI and then codify the workflow in repo docs.

## Recommendations applied in this repo

- Added `docs/governance/shared-memory-architecture.md`.
- Added `docs/memory/` with index, conventions, handoff queue, and run-journal structure.
- Added first run journal entry to bootstrap the pattern.

## Sources checked

| Source | Accessed | Link / locator | Why it matters |
| --- | --- | --- | --- |
| OpenAI Codex docs | 2026-05-24 | https://developers.openai.com/codex/ | Primary product documentation for cloud workflows, skills, MCP, and use-cases. |
| Anthropic Claude Code memory docs | 2026-05-24 | https://docs.anthropic.com/en/docs/claude-code/memory | Reference for path-scoped memory behavior and progressive disclosure patterns. |
| SWE-bench benchmark project | 2026-05-24 | https://www.swebench.com/ | Benchmark lineage reference for traceable engineering-eval workflows. |
| Security survey used in the parallel environment brief | 2026-05-24 | `/home/runner/work/symphony/symphony/docs/research/2026-05-19-agentic-environment-setup.md` (source register row: "Confidential computing for agents survey") | Threat-model input for memory and tool-boundary policy. |
