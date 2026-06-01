# Marrying ICM with a Real Multi-Agent, Multi-Model, Multi-VM Stack

*For sablekeys. Written boots-on-the-ground, with primary sources, ICM-in / ICM-out, and an actual implementable architecture.*

---

## TL;DR

1. Everything you named is real. **Hyperagent (Airtable)** — Howie Liu's enterprise multi-agent platform with Skills as the primitive. **Hermes Agent (NousResearch)** — open-source agent, 174K stars, **v0.15 "Velocity" released 28 May 2026**, with Kanban turned into a real multi-agent platform (worktree-per-task, swarm topology, per-task model overrides, durable SQLite board). **Claude Opus 4.8** released 28 May 2026. **GPT-5.5 (incl. Codex)** released April 2026. **Grok 4.3** is real, 1M context, $1.25-in/$2.50-out, 1800 RPM. Sources cited inline below.
2. **Name disambiguation is non-trivial.** Your *project* is "Hermes Solana Edge." NousResearch's *tool* is "Hermes Agent." From here I'll call them **"Hermes-SE"** (your project) and **"Hermes-NR"** (the tool). Confuse them at your own risk.
3. **The ladder is real.** Single model → tools → filesystem-as-memory (ICM enters) → subagents → durable multi-agent board → multi-model swarm with worktree isolation → cross-VM federation with governance + protocols → governed adversarial-grade council. Rung 5 (Hermes-NR Kanban) is where you actually are right now. Rung 7 is your target.
4. **ICM lives inside each agent at every rung.** It is the cognition substrate. The orchestration layer above (Hermes-NR Kanban / Hyperagent skills / A2A protocol) is what ICM consciously doesn't do.
5. **Governance is *not* one layer. It's six.** Input rails → tool/action policies → output rails → inter-agent contracts → system policy (anti-alpha gates) → audit & replay. Skip any and you have a Lambo with no brakes.
6. **VM-per-agent is correct and increasingly standard.** E2B / Modal / Daytona / Fly Machines are the four canonical providers. Hyperagent has its own VM per agent. Hermes-NR uses worktree-per-task (filesystem isolation) and can also push tasks to sandboxed runtimes.

Now the full breakdown.

---

## Part 1 — Reality check (what's real, with sources)

### 1.1 Hyperagent — Airtable's multi-agent platform

From Howie Liu's own essay introducing it (`howietl.substack.com/p/agi-is-here-now-harness-it`, 19 Feb 2026):

> "What's missing isn't any single feature — it's the complete system. The orchestration, the tools, the memory, the skills, the ability to deploy and manage agents across an entire organization. No one has built it yet. We are. We're calling it Hyperagent."

From the Stork.AI explainer (`stork.ai/blog/airtables-ceo-just-built-your-ai-team`):

> "At the heart of Hyperagent's power are **Skills**, the platform's fundamental primitive. Skills encode specific playbooks and processes, effectively transforming generally intelligent models into highly specialized domain experts."

So: Hyperagent = orchestration layer + tools + memory + Skills. Skills are *exactly* the ICM Layer-3 idea, productized into an enterprise platform. The $35 startup-in-a-box demo (market research → Reddit validation → competitive analysis → prototype → marketing site) is the headline use case.

### 1.2 Hermes Agent (NousResearch) v0.15 — the Velocity release

From the official release notes (`github.com/NousResearch/hermes-agent/releases/tag/v2026.5.28`):

> "**Kanban grew into a real multi-agent platform** — 104 PRs end to end. Triage auto-decomposes one task into a tree of sub-tasks. `hermes kanban swarm` creates a full Swarm v1 graph in one command — root, parallel workers, gated verifier, gated synthesizer, shared blackboard. Tasks support per-task model overrides (cheap models for boilerplate, expensive ones for hard sub-tasks), board-level default workdirs, **per-task worktree paths and branches**, scheduled start times, configurable claim TTL, retry fingerprinting, stale-task detection, respawn guards… Workers report through `/workers/active`, `/runs/{id}`, and `/inspect` endpoints."

From the Hermes Kanban docs (`hermes-agent.nousresearch.com/docs/.../kanban`):

> "Hermes Kanban is a durable task board, shared across all your Hermes profiles, that lets multiple named agents collaborate on work without fragile in-process subagent swarms. Every task is a row in `~/.hermes/kanban.db`; every handoff is a row anyone can read and write; **every worker is a full OS process with its own identity**."

The two-primitive distinction matters. From the same page:

| `delegate_task` | Kanban |
|---|---|
| RPC call (fork → join) | Durable message queue + state machine |
| Parent blocks until child returns | Fire-and-forget after `create` |
| Child = anonymous subagent | Child = named profile with persistent memory |
| No resumability | Block / unblock / retry / reclaim |
| No human-in-loop | Comment / unblock at any point |
| Audit lost on context compression | Durable rows in SQLite forever |

**This is exactly the architecture you described.** Hermes-NR Kanban = Linear-but-built-for-agents. The agents drive the board through a dedicated `kanban_*` toolset; you (and cron, and scripts) drive it through the CLI. Both write to the same SQLite — no drift.

And critically (`.../codex-app-server-runtime`):

> "Hermes can optionally hand `openai/*` and `openai-codex/*` turns to the Codex CLI app-server… Run OpenAI agent turns against your **ChatGPT subscription (no API key required)** using the same auth flow Codex CLI uses. Use Codex's own toolset and sandbox — `shell`, `apply_patch`, `update_plan`, all running inside seatbelt/landlock sandboxing."

So your ChatGPT Codex subscription is your gateway to GPT-5.5 inside Hermes-NR *without* paying OpenAI API rates. That's the Codex App-Server Runtime feature. Real.

### 1.3 The model fleet

- **Claude Opus 4.8** (Anthropic, 28 May 2026 — same day as Hermes v0.15): *"the only model to complete every case end-to-end on our Super-Agent benchmark, beating prior Opus models and GPT-5.5 at parity on cost… 84% on Online-Mind2Web (computer-use), a meaningful jump over Opus 4.7 and GPT-5.5."* (`anthropic.com/news/claude-opus-4-8`)
- **GPT-5.5** (OpenAI, April 2026): general agentic upgrade, available via Codex subscription + API.
- **Grok 4.3** (xAI): 1M context, $1.25/$2.50 per 1M tokens, 1,800 req/min, 10M tokens/min. *"Leading the industry in non-hallucination rate, agentic tool calling, and instruction following capabilities."* (`docs.x.ai/developers/models/grok-4.3`)

For Solana social monitoring, Grok 4.3 is actually well-positioned: it's cheap, fast, has 1M context (you can stream a *lot* of tweets through one window), and its non-hallucination characteristics matter for signal triage. Don't dismiss xAI's Solana-ecosystem position either — it's a meaningful corner of their user base.

### 1.4 The $1,000 in Hyperagent credits — yes, the playbook is real

Hyperagent's promo strategy maps onto a real pattern: enterprise SaaS giving credit-heavy trials so devs build with it, get attached, and pull their org in. From Stork.AI: *"a Hyperagent workflow that performs market research, Reddit validation, competitive analysis, and generates a prototype, marketing site, and ad creative for around $35."* If that's accurate, $1,000 is ~28 full startup-in-a-box workflows or ~200 mid-sized agent runs. That's a real budget. Burn it.

---

## Part 2 — The ladder, simplest → most advanced

This is the spine of the answer. I'll do each rung once, with what changes, what ICM contributes, what governance you add, and where you are.

### Rung 1 — Single model, single chat window

*Example:* ChatGPT, claude.ai, x.com/Grok.
- *Capability:* one model, one context, no tools, no persistence.
- *ICM contribution:* none — there's no file system.
- *Governance:* the provider's content policy. Nothing more.
- *Failure mode:* context window fills up; loses thread; can't act in the world.

### Rung 2 — Single model + tools (function calling / tool use)

*Example:* Claude with `web_search` and `view_image`, ChatGPT with browse + code interpreter.
- *Capability:* model can read web, run sandboxed Python, view images. Limited persistence inside the session.
- *ICM contribution:* still mostly none.
- *Governance:* tool-level: which tools are exposed, scopes per tool.
- *Failure mode:* "lost in the middle" on long contexts; tool calls cost real tokens; no memory across sessions.

### Rung 3 — Single model + tools + **filesystem memory** (ICM enters here)

*Example:* Claude Code with a project repo, Cursor with `AGENTS.md`, Hermes-NR with skills + memory.
- *Capability:* the agent reads/writes files. Context across sessions becomes possible.
- *ICM contribution:* **this is where ICM does its real work.** Identity (CLAUDE.md) + Routing (CONTEXT.md) + Stage Contracts + Reference Material + Working Artifacts. Token budget per stage drops from 30–50k to 2–8k. *Per-stage* portability between models becomes possible.
- *Governance:* file-system permissions, write scopes (`workspace-write` vs `workspace-read`), per-skill allowlists.
- *Where you are if you do ONE thing right:* you can hand off the same workspace to ChatGPT, Claude, or Grok and they all do useful work because the workspace teaches them the role.

### Rung 4 — Single model + **subagents** (in-process delegation)

*Example:* Claude Code's `Explore` / `Plan` / `general-purpose` subagents; OpenAI Agents SDK `handoffs`; Hermes-NR `delegate_task`.

From Claude Code docs (`code.claude.com/docs/en/sub-agents`):
> "Each subagent runs in its own context window with a custom system prompt, specific tool access, and independent permissions… Use one when a side task would flood your main conversation with search results, logs, or file contents you won't reference again: the subagent does that work in its own context and returns only the summary."

- *Capability:* parent agent forks workers with fresh context windows for narrow tasks (search a codebase, summarize logs, run an evaluator). Child returns *only the summary* to the parent.
- *ICM contribution:* each subagent can inherit a *subset* of the parent's CLAUDE.md or be given its own. Explore + Plan deliberately skip CLAUDE.md to stay cheap.
- *Governance:* per-subagent tool allowlists. Explore is *read-only* by design. Plan is *read-only*. Costs are controlled by routing trivial work to Haiku.
- *Failure mode:* still in-process — if the parent crashes, the work is lost. No durable handoff between subagents.

### Rung 5 — **Durable multi-agent board** (named, persistent agents)

*Example:* **Hermes-NR Kanban** (you're here). Cline Kanban. Paperclip. NanoClaw.
- *Capability:* every task is a SQLite row. Every agent has a name and persistent memory. Tasks survive crashes, get reclaimed, blocked, unblocked, commented on. *Humans and agents share the board.*
- *ICM contribution:* each named agent has its own ICM workspace (identity, routing, stage contracts). The board itself becomes the routing layer between agents.
- *Governance:* `claim_ttl`, `respawn_guards`, `retry_fingerprinting`, per-agent profile permissions, board-level write scopes.
- *Failure mode:* still single-process-per-agent on a single machine in the default install. Hermes-NR profiles share `~/.hermes/kanban.db`.

### Rung 6 — **Multi-model swarm + worktree isolation per task** (you're heading here)

*Example:* `hermes kanban swarm` creating Swarm v1 graphs. Hyperagent multi-agent flows. Simon Willison's parallel worktrees.

From Hermes v0.15 release notes:
> "`hermes kanban swarm` creates a full Swarm v1 graph in one command — root, parallel workers, gated verifier, gated synthesizer, shared blackboard. Tasks support per-task model overrides… per-task worktree paths and branches…"

- *Capability:* one task fans out to N parallel workers, each in *its own git worktree* (so writes don't collide), each potentially running a different model (Opus 4.8 for hard reasoning, Haiku for boilerplate, Grok 4.3 for social-data parsing). A **gated verifier** checks each worker's output before a **gated synthesizer** merges. Shared blackboard for state.
- *ICM contribution:* each worktree is a clean ICM workspace. The factory (`_config/`) is the same; the product (`stages/output/`) is per-worker.
- *Governance:* per-task model override + per-task workdir + claim TTL + retry fingerprinting. Gated verifier *is* a governance choke point.
- *Failure mode:* still on one VM / machine. No cross-org collaboration. Verifier quality is now the single biggest determinant of swarm quality.

### Rung 7 — **Cross-VM federation + protocols + governance rails** (the next jump)

*Example:* Multiple agents on isolated VMs (Hyperagent on its own, Hermes-NR on its own, Grok-agent on its own), connected via **A2A protocol** (Google) for inter-agent messaging + **MCP** (Anthropic) for tool sharing, with **NeMo Guardrails** / **Llama Guard** on each border.

From Google's A2A announcement (`developers.googleblog.com/a2a-a-new-era-of-agent-interoperability`):
> "A2A is an open protocol that complements Anthropic's Model Context Protocol (MCP)… A2A focuses on enabling agents to collaborate in their natural, unstructured modalities, even when they don't share memory, tools and context. We are enabling true multi-agent scenarios without limiting an agent to a 'tool.'"

- *Capability:* agents on different VMs (different vendors, different models, different memory stores) can call each other as peers, not as tools. Each agent has its own ICM workspace + its own sandbox + its own governance rails. They negotiate handoffs via a typed protocol.
- *ICM contribution:* each agent's identity / routing / stage contracts are still ICM. The protocol (A2A) is the inter-agent equivalent of an HTTP API.
- *Governance:* per-VM rails (input/output guardrails, prompt-injection detection), inter-agent contracts (A2A typed messages), system policies (allowlists per agent), audit logs per agent + per handoff.
- *This is where you need to be heading.* Hyperagent + Hermes-NR + Grok-NR on three VMs, talking via A2A or a typed message queue, governed at each border.

### Rung 8 — **Governed adversarial-grade council with policy-as-code + append-only memory + agent-trust** (your real target)

This is your `Hermes_Solana_Edge_Canonical_Build_Spec_v1.docx` doc, taken to its conclusion.

- *Capability:* rung 7 + (a) policy-as-code (your anti-alpha gates, slippage caps, hysteresis bands), (b) append-only memory with provenance per claim, (c) agent-trust EWMA so bad agents get demoted automatically, (d) replayable runs from event-bus snapshots, (e) circuit breakers and kill switches that trigger on policy violations.
- *ICM contribution:* the *factory* (`_config/`) holds your governance doctrine; the *product* (`stages/output/`) holds trade_cards, reject_cards, evidence bundles.
- *Governance:* everything in rung 7 + agent-trust-driven autonomy gating, mandatory escalation thresholds (e.g., below 0.35 trust, block; above 0.45, allow; in between, escalate to you).
- *Failure mode:* you. Operator fatigue, policy drift, doctrine that doesn't evolve. *This is the human-in-the-loop bottleneck and it's where Tier-3 judgment lives.*

---

## Part 3 — The governance layer, broken into six tiers

You asked specifically about governance. Here is what it actually consists of, by layer, with tools that exist today.

### G1. Input rails (pre-agent)
- **Prompt-injection detection** (Llama Guard, NeMo Guardrails injection-detection with YARA rules). NVIDIA docs:
  > "*Injection detection is primarily intended to be used in agentic systems to enhance other security controls as part of a defense-in-depth strategy.*"
- **Content moderation** (OpenAI moderation API, Llama Guard).
- **Tool-call validation**: schema-check every tool call before it runs.

### G2. Tool / action policies (intra-agent)
- Per-tool allowlists & denylists. Per-skill scope grants. *No agent should have every tool.*
- For your trading work: per-tool slippage caps, per-tool size caps, per-tool dry-run requirements before real exec.
- E2B / Modal / Daytona's sandbox-level network egress controls. From agentmarketcap on E2B: *"Network egress controls to prevent a compromised sandbox from calling home or exfiltrating data."*

### G3. Output rails (post-agent, pre-action)
- Hallucination / contradiction checks before writes.
- PII redaction.
- Structured-output validation (Pydantic, JSON Schema).
- *For Hermes-SE: every `trade_card` must pass schema + anti-alpha gates before it leaves the agent.*

### G4. Inter-agent contracts
- Typed messages (A2A protocol, or your own typed message queue).
- Authentication between agents (mutual TLS, signed messages, agent-ID provenance).
- Idempotency keys on every cross-agent action.

### G5. System policies (board / org level)
- Your **anti-alpha gates** (refuse trade if liquidity < threshold, if wallet-cluster correlation > threshold, etc.).
- **Agent-trust EWMA**: every agent's accuracy is tracked; below 0.35 they're auto-blocked, between 0.35–0.45 escalate, above 0.45 allow.
- **Kill switches** triggered by drawdown, latency, anomaly.
- **Promptware defense** — Hermes v0.15 added this against "Brainworm-class attacks." Real, in-product.

### G6. Audit & replay
- **Append-only memory** with provenance per claim.
- Hermes-NR's Kanban already gives you this: *"every handoff is a row in SQLite forever."*
- Event-sourced architecture so you can replay any decision from any point in time.
- Decision IDs as deterministic hashes of inputs, so the same inputs always produce a re-creatable trace.

Mapping to your existing doc: your canonical build spec already requires G5 and G6. You don't have G1–G4 explicitly. *That's the gap.*

---

## Part 4 — The concrete implementable architecture for *you* this quarter

Now the boots-on-the-ground version. Three VMs, three agents, three frontier models, one shared board, one governance fabric.

### 4.1 The topology

```
                    +----------------------------+
                    |   Hermes-SE Operator (you) |
                    |   - approves Tier-3 calls  |
                    |   - reviews kanban board   |
                    +-------------+--------------+
                                  |
                                  v
                    +----------------------------+
                    |   Shared Kanban Board      |
                    |   (Hermes-NR SQLite DB)    |
                    |   - durable handoffs       |
                    |   - audit trail forever    |
                    +-+----------+-----------+---+
                      |          |           |
            A2A/typed |    A2A/typed     A2A/typed
                      v          v           v
        +----------------+ +-----------+ +---------------+
        |  VM-1: Hermes  | | VM-2:     | | VM-3: Grok    |
        |  -NR (your     | | Hyperagent| | Social Agent  |
        |  Solana edge   | | (Airtable)| | (xAI)         |
        |  harness)      | |           | |               |
        |                | |           | |               |
        | Model: GPT-5.5 | | Model:    | | Model:        |
        | via Codex sub  | | Opus 4.8  | | Grok 4.3      |
        |                | |           | |               |
        | Job: trading,  | | Job: lead | | Job: Solana   |
        | risk, evidence | | -gen      | | social-graph  |
        | gating         | | workflows | | monitoring    |
        +----------------+ +-----------+ +---------------+
                Sandbox: seatbelt/landlock + E2B for risky exec
        Each VM has: ICM workspace + per-agent governance rails
```

### 4.2 What each agent gets (the ICM workspaces)

**VM-1 — Hermes-NR harness (your Solana-edge brain)**
```
~/.hermes/profiles/hermes-se/
  CLAUDE.md                       # Identity: "I am Hermes-SE..."
  CONTEXT.md                      # Routing across stages
  _config/                        # The factory
    doctrine.md                   # Anti-alpha gates, allowlists, slippage caps
    policy_as_code.yaml           # Hysteresis bands, kill-switch thresholds
    agent_trust.json              # Per-agent EWMA scores
    evidence_schema.json
  skills/                         # ICM Layer-3 made reusable
    wallet_cluster_analysis/SKILL.md
    kol_burst_validation/SKILL.md
    liquidity_probe/SKILL.md
    trade_card_assembly/SKILL.md
  stages/                         # Working artifacts (the product)
    01-ingest/output/
    02-classify/output/
    03-evidence/output/
    04-gate/output/
    05-draft-trade-card/output/
  memory/
    append_only/                  # decisions + provenance, forever
    contradictions.log
```
Drives it through Hermes-NR Kanban. Use `hermes kanban swarm` for the per-event parallel research → verify → synthesize pattern.

**VM-2 — Hyperagent (lead-gen agency engine)**
- Use Hyperagent's native **Skills** as your ICM Layer-3 substrate. Each client = a workspace, each audit stage = a Hyperagent flow.
- Their $35-startup demo is exactly your "leaky bucket" audit pipeline: market research → validation → competitive → prototype → marketing. Burn the $1k credit on running 20–30 real local-business audits *to refine the stage contracts.*
- *Don't try to make Hyperagent your trading brain.* It's not what it's for. Lead-gen is its lane.

**VM-3 — Grok 4.3 social agent**
- Cheap ($1.25/$2.50 per 1M), 1M context, 1800 RPM. Wire it to Twitter/X firehose + Telegram + Discord for Solana social signal.
- Two responsibilities: (a) ingest + classify social signal → push candidate signals as kanban rows to the shared board, (b) optionally execute *your* social-presence posts under your voice.
- Run it as either: a Hermes-NR profile (cleanest — same Kanban) or a standalone xAI Live Search agent.

### 4.3 The wiring

- **Cross-VM transport.** Hermes-NR's Kanban is your primary bus. If Hyperagent doesn't speak Hermes Kanban natively (it won't), use **A2A** if both sides support it, or a typed message queue (Redis Streams, NATS) with idempotency keys. Pragmatic interim: a *single* `hermes kanban` board where each VM has a profile that polls.
- **MCP for tools.** Each VM exposes its useful tools as MCP servers; other agents consume them. Hermes v0.15 added a Nous-approved MCP catalog. Use it.
- **Secrets.** Hermes v0.15 added Bitwarden Secrets Manager so one bootstrap token replaces N API keys. Use that, don't sprawl `.env` files across three VMs.
- **Governance rails.** NeMo Guardrails on Hermes-NR's I/O. Llama Guard on Grok-agent's I/O (because social input is the highest-risk attack surface for prompt injection). Hyperagent has its own enterprise rails.
- **Sandbox layer.** For anything that compiles, executes, or touches an RPC: E2B microVMs (cheapest, 80ms cold-start, Firecracker isolation) or Daytona if you want longer-running sandbox sessions. Don't run untrusted-input-derived code outside a sandbox. Ever.

### 4.4 The frameworks to actually use

From Composio's framework comparison and what I see being deployed in 2026:
- **OpenAI Agents SDK** — lightweight, three primitives (Agents, Handoffs, Guardrails). Easiest to start, weakest at complex state. Use if your work fits a flow.
- **LangGraph** — graph-based, strong state management, steeper learning curve. Use if you need cyclic flows with real state (you do, in Hermes-SE).
- **CrewAI** — role-based multi-agent. Most intuitive for "give each agent a role." Less suited to adversarial work.
- **AutoGen** — flexible conversation patterns, weaker docs.
- **Hermes-NR Kanban (Swarm v1)** — durable, multi-process, audit-trail-first. *This is the one you should default to* because adversarial-market work demands every handoff be durable.

You don't need to pick one of LangGraph / OpenAI Agents SDK / CrewAI right now. Hermes-NR Kanban gives you the orchestration; you can later wrap a specific stage in LangGraph if you need state-machine-grade flow.

---

## Part 5 — Where ICM fits at every rung (the unified picture)

ICM is **not a rung**. It is **the substrate inside every rung**.

| Rung | What's new at this rung | What ICM contributes |
|---|---|---|
| 1 — single chat | nothing | nothing |
| 2 — + tools | tool-call vocabulary | nothing (no FS) |
| 3 — + filesystem | persistence | **ICM defines the file layout: identity → routing → stage → reference → working** |
| 4 — + subagents | per-subagent fresh context | each subagent inherits or selects an ICM slice |
| 5 — + Kanban | durable named agents | each named agent has its own ICM workspace |
| 6 — + swarm | parallel workers in worktrees | each worktree is a clean ICM workspace |
| 7 — + cross-VM | inter-agent protocols | each VM's agent has its own ICM, A2A is the wire |
| 8 — + governed adversarial | policy-as-code, trust, audit | ICM holds the doctrine in `_config/`, the product in `stages/`, the audit in `memory/` |

ICM = how *one agent* organizes its mind.
Hermes-NR Kanban / Hyperagent / A2A = how *many agents* coordinate their minds.
Governance rails = how you *constrain* what any mind can do.

**You need all three. ICM does not substitute for orchestration; orchestration does not substitute for ICM; neither substitutes for governance.**

---

## Part 6 — Frontier patterns the hype doesn't cover yet

These are the things the YouTube videos won't tell you, and they're where the alpha is.

### 6.1 Verifier-gated swarms beat unguarded multi-agent every time

The Hermes Swarm v1 pattern — *root → parallel workers → gated verifier → gated synthesizer* — is the most important architectural shape in 2026. Why? Because raw multi-agent (just spawn N workers and average) hits *amplified hallucination*: workers reinforce each other's errors. A *gated verifier* — an independent worker that *rejects* outputs failing the contract — is what makes multi-agent actually safer than single-agent. Skip the verifier and you're worse off than one good model.

### 6.2 Cross-model verification is real alpha — but watch the architectures, not the labels

Different model *architectures* genuinely fail in different places. Claude tends to be over-cautious, GPT tends to over-confidence, Grok tends to under-context. So a verifier that runs on a *different family* than the producer catches errors a same-family verifier misses. Practical pattern: GPT-5.5 produces a trade_card → Opus 4.8 verifies it → Grok 4.3 checks the social-corroboration claim. Disagreement → escalate to you.

### 6.3 Worktree-per-task is *the* isolation pattern

Hermes v0.15's "per-task worktree paths and branches" + Jesse Vincent's Superpowers + Simon Willison's parallel agents converge on the same shape: each task gets its own `git worktree`. Means: workers can't clobber each other's files, you can `git diff` any agent's work, merge is via a real PR-style review. This is *much* better than locks or shared scratch dirs.

### 6.4 The MCP + A2A combo (use both)

- **MCP** (Anthropic) — the agent ↔ tool protocol. Use it to expose tools (your Helius/Birdeye/Jupiter calls, your wallet-clustering function) to *any* agent.
- **A2A** (Google + 50 partners) — the agent ↔ agent protocol. Use it for *peer* communication between agents, not for tool calls.

These complement, they don't compete.

### 6.5 The "Promptware defense" / Brainworm class is new and important

Hermes v0.15's release notes explicitly call out "Promptware defense lands against Brainworm-class attacks." Brainworm-class = attacks where prompt-injected instructions try to *modify the agent's own skills/memory/scheduled jobs* — a self-modifying compromise. For your Solana social monitoring, this is a real risk: a KOL posts adversarial text designed to compromise your agent's memory. Treat *every retrieved string* as hostile until proven otherwise. Specifically:
- Never let retrieved content reach the system prompt or trusted skill files.
- Never let an agent write to its own `_config/`.
- Sign skills and verify signatures on load.

### 6.6 The durable-garbage problem at multi-agent scale

I mentioned this in the ICM thread. At multi-agent scale it *compounds*. Agent A writes wrong claim → Agent B reads it as truth → uses it to validate Agent C's output → now three agents agree on a fiction. The fix is *epistemic typing*:

- `evidence` (raw, sourced, immutable)
- `claim` (an agent's assertion, with source, timestamp, confidence)
- `decision` (an action taken, with linked evidence and claims)
- `hypothesis` (unverified, tracked, eventually proven or pruned)

Each lives in its own file structure with its own lifecycle. *Never collapse them.* Your canonical doc's `trade_card / reject_card / evidence card` distinction is already doing this — extend it across all of Hermes-SE.

### 6.7 Constitutional AI / policy-as-code

This is the formal name for what your "anti-alpha gates" already are. Constitutional AI = enforce policies *as code that runs on agent outputs*, not as instructions inside the prompt. Why? Prompts can be jailbroken; code can't. Implementation:
- Every agent output passes through a deterministic policy function.
- Function returns `allow | escalate | block` + reason.
- Function code is in git, reviewed, versioned.

NeMo Guardrails' "output flows" + Llama Guard's classifiers + your own Python policies = a layered defense.

### 6.8 Agent-trust as a closed-loop control system

Your EWMA trust score is correct. The under-discussed part: *the inputs* to that EWMA need to be high-signal. Three sources:
1. **Verifier disagreement rate** (when does a second model reject this agent's output?)
2. **Realized outcome alignment** (did the trade thesis pan out, or did it under-perform predicted?)
3. **Provenance violations** (did the agent make claims without citing evidence?)

Weight these, run through EWMA, output drives the autonomy gate.

### 6.9 Cost arbitrage by routing per-task

Hermes v0.15's "per-task model overrides" is the operationalization of: *don't run Opus 4.8 on tasks that Haiku could do.* For your stack:
- Trivial classification: Grok 4.3 mini ($0.20 cached input). Cheap and good enough.
- Standard analysis: GPT-5.5 standard, via Codex sub (effectively free at the margin).
- Hard reasoning + final synthesis: Opus 4.8 (the expensive model, used rarely).
- Adversarial cross-check: opposite-family verifier.

Build this into your Kanban swarm template. *This is the multi-model "synergy" you mentioned — but the synergy comes from routing, not from spawning N models that all do the same thing.*

### 6.10 Evals as the immune system

I'll say this in every reply until you build them. **You need acceptance tests per stage.** For Hermes-SE:
- "Given this synthetic event stream, the wallet-cluster agent should output X."
- "Given this evidence bundle, the anti-alpha gate should block."
- "Given this trade_card, the verifier should mark it 'insufficient evidence.'"

These tests *gate every deploy* of an agent. Without them, you can't safely change anything. With them, you can safely change everything. Evals are the difference between "vibes-based" agent development and engineering.

---

## Part 7 — What to actually do this quarter (sequenced)

1. **Week 1 — Burn the Hyperagent credits.** Run 5 real local-business audits through Hyperagent's flows. Capture: what works, what doesn't, where the stage contracts are weak. *That's market research and product development at once.*
2. **Week 1–2 — Install Hermes-NR on a clean VM.** Use `hermes setup --portal` for the non-Codex path or wire your Codex subscription via the Codex App-Server Runtime. Build one ICM-style profile for Hermes-SE with the workspace structure in §4.2.
3. **Week 2–3 — Spin up a single `hermes kanban swarm` for one Solana event class.** Pick the easiest: KOL-burst signal. Root → parallel research workers → gated verifier (different model) → synthesizer → trade_card or reject_card. Measure: false-positive rate, latency, cost per event.
4. **Week 3 — Add evals.** Write 20 synthetic fixtures per stage. Wire to CI so changing a skill runs the evals.
5. **Week 4 — Add governance rails.** NeMo Guardrails injection-detection on inputs. Constitutional-style policy function on outputs (your anti-alpha gates). Agent-trust EWMA on every agent.
6. **Week 5 — Grok social agent.** Standalone Hermes-NR profile or independent xAI Live Search service. Pushes candidate signals to the shared Kanban board. *Read-only by default.*
7. **Week 6 — Cross-model verification.** Pair GPT-5.5 producer with Opus 4.8 verifier (or vice versa). Measure disagreement rate. Tune thresholds.
8. **Week 7–8 — Sandbox + secrets.** E2B for any code execution. Bitwarden Secrets Manager for credentials. Audit every tool's egress.

Don't try to do all of this in parallel. The order is deliberate — each step gives you something the next step depends on.

---

## Sources

- Howie Liu, *AGI is here. Now harness it. Introducing Hyperagent*, Feb 2026 — `howietl.substack.com/p/agi-is-here-now-harness-it`
- Stork.AI, *Airtable's CEO Just Built Your AI Team* — `stork.ai/blog/airtables-ceo-just-built-your-ai-team`
- Airtable, *AI agent software* — `airtable.com/platform/ai-agents`
- NousResearch, *Hermes Agent v0.15.0 (2026.5.28) — The Velocity Release* — `github.com/NousResearch/hermes-agent/releases/tag/v2026.5.28`
- NousResearch, *Kanban (Multi-Agent Board)* — `hermes-agent.nousresearch.com/docs/user-guide/features/kanban`
- NousResearch, *Codex App-Server Runtime (optional)* — `hermes-agent.nousresearch.com/docs/user-guide/features/codex-app-server-runtime`
- Anthropic, *Introducing Claude Opus 4.8*, 28 May 2026 — `anthropic.com/news/claude-opus-4-8`
- OpenAI, *Introducing GPT-5.5*, 23 Apr 2026 — `openai.com/index/introducing-gpt-5-5/`
- xAI, *Grok 4.3 docs* — `docs.x.ai/developers/models/grok-4.3`
- Google, *Announcing the Agent2Agent Protocol (A2A)*, 9 Apr 2025 — `developers.googleblog.com/a2a-a-new-era-of-agent-interoperability/`
- Anthropic, *Create custom subagents* (Claude Code) — `code.claude.com/docs/en/sub-agents`
- AgentMarketCap, *AI Agent Sandbox Infrastructure in 2026: E2B, Modal, Daytona, and Fly Machines* — `agentmarketcap.ai/blog/2026/04/07/ai-agent-sandbox-infrastructure-e2b-modal-daytona-fly-machines-secure-code-execution`
- Composio, *OpenAI Agents SDK vs LangGraph vs Autogen vs CrewAI* — `composio.dev/content/openai-agents-sdk-vs-langgraph-vs-autogen-vs-crewai`
- NVIDIA, *NeMo Guardrails — Agentic Security & Injection Detection* — `docs.nvidia.com/nemo/guardrails/latest/configure-rails/guardrail-catalog/agentic-security.html`
- Plus your earlier docs (`Hermes_Solana_Edge_Canonical_Build_Spec_v1.docx`, `files_grow_on_trees.txt`, `deep-research-report 3.md`, `harness_prompting_kit.txt`).
