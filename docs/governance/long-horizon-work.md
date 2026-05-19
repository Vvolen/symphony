# Long-Horizon Agentic Work

## Definition

A long-horizon run is work that spans many tool calls, multiple validation loops, or potentially multiple sessions. It needs a stronger contract than a normal prompt.

## Required run contract

Before starting a long-horizon build or research sweep, capture:

1. Objective: the durable outcome.
2. Scope: what may change and what must not change.
3. Evidence: sources, files, logs, screenshots, traces, or tests required.
4. Validation loop: commands or checks to run repeatedly.
5. Stop condition: how the agent knows it is done.
6. Escalation condition: when the agent should stop and ask.
7. Cost/safety boundary: network, credentials, spending, production, and trading restrictions.

## Multi-agent patterns

| Pattern | Use when | Risk |
| --- | --- | --- |
| Single agent + scripts | task is linear and validation is deterministic | tunnel vision |
| Orchestrator + workers | work decomposes into independent slices | bottleneck or lossy summaries |
| Peer-to-peer agents | specialized agents need two-way exchange | loops, unclear authority, message poisoning |
| Verifier/critic agent | claims or changes are high stakes | token cost, false confidence |
| External persistent agent | needs scheduled work or cross-session memory | secrets, drift, monitoring burden |

## Recommended stance

Use focused agents with clear separation of concerns. Add peer-to-peer communication only where two agents hold different authority or context, such as production-vs-development, researcher-vs-builder, or implementer-vs-verifier.

## Evidence trail

If it cannot be searched, cited, or replayed, treat it as weak memory. Durable work should leave artifacts in `docs/research/`, `docs/governance/`, issue comments, PR bodies, or logs.
