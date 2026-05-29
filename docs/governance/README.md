# Governance Hub

This directory turns the Symphony fork into a durable operating base for agentic research and build work.

## Why this exists

Agentic systems become powerful when their instructions, tools, evidence, and stop conditions are explicit. The goal is not bureaucracy; the goal is leverage:

- repeatable research;
- safe handling of tools and credentials;
- clear separation between facts, inference, and recommendations;
- reusable skills and scripts;
- long-horizon work that has an objective, validation loop, and stopping rule.

## Core documents

- [`environment.md`](environment.md): environment variables, secrets, setup scripts, and persistence boundaries.
- [`tools-and-mcp.md`](tools-and-mcp.md): MCP, CLI tools, gateways, and progressive disclosure.
- [`long-horizon-work.md`](long-horizon-work.md): goal-driven runs, multi-agent collaboration, and evidence trails.
- [`shared-memory-architecture.md`](shared-memory-architecture.md): shared memory structure, anti-conflation rules, and handoff protocol.

## Default stance

Start narrow, make the artifact searchable, and only add persistent power after the safety boundary is clear.

## Systems catalog

Use `docs/systems/INDEX.md` for reusable architecture modules, procurement candidates, and long-horizon hydration scaffolds.


## Usage note

Run checks as `./scripts/check` (or `bash scripts/check`) from any directory. The script resolves the repo root automatically.
