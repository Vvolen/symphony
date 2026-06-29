# Hermes Solana Edge OS — Context Pack

> Hand this to any agent as its **first read**. It is the compressed brain of the project: who,
> what, why, what's verified, what's decided, and the next action. Optimize for high signal; keep it
> current.

## Operator

Self-taught AI-orchestration architect. Works by **specifying and delegating to agents**, not by
writing code. Voice-first (dictates; listens back at 1.25–1.5×). Strengths: whole-system thinking,
spec-driven design, pattern recognition, governance/delegation taste. The operating asset is
**judgment** — multiple years of Solana pattern memory and the ability to decide what to delegate,
how to verify, and when to trust.

How to work with him: map every recommendation to a concrete file / API / decision; challenge
assumptions directly (do not validate without pushback); lead with the single highest-leverage
move; always produce the build path; surface adjacent risks and opportunities.

## What we're building

**Hermes Solana Edge OS** (a.k.a. Project B.O.S.S.) — an **evidence-governed intelligence factory**
plus a **deterministic capital-decision factory** for Solana. Not a trading bot: a disciplined loop
that detects a narrow class of on-chain events, proves what it saw, rejects manipulated or
untradeable candidates aggressively, sizes only into real liquidity, and learns from every
decision — *including the rejections*.

Core doctrine: **slow cognition, fast reflex.** The cognitive layer (LLM + specialist agents)
proposes intent; a deterministic reflex layer enforces survivability and can veto anything. Evidence
before execution. Determinism before autonomy. The model proposes; **policy + a one-time grant
authorizes**.

## Substrate (verified, June 2026)

- **Nous Research Hermes Agent** is real and is the intelligence-factory substrate. Persistent,
  self-improving agent: built-in learning loop, skills-as-files, `MEMORY.md`/`USER.md`/`SOUL.md`,
  durable SQLite **Kanban** multi-agent board, cron, MCP-native, 20+ messaging gateways, six
  backends (local/Docker/SSH/Daytona/Singularity/Modal), ~$5/mo VPS. **Async background subagents**
  shipped 2026-06-15. **Self-evolution** (separate repo, DSPy + GEPA) auto-optimizes skills/prompts;
  an autonomous Curator prunes the skill library. Repo: `github.com/NousResearch/hermes-agent`.
- **Wallet intelligence is mostly off-the-shelf.** `netvyxe/godmode` (funding-chain tracing, 0–100
  risk scoring, BUNDLER/SNIPER/WHALE verdicts, Helius `funded-by` endpoint).
  `drtiibiird/helius-forensics-mcp` (the wallet stalker already packaged as an MCP server).
  Institutional pattern seen in the wild: Helius Geyser → Kafka → ClickHouse → agent API.
- **Solana data/execution have MCPs now:** Alchemy, GMGN, Jupiter, QuickNode, Helius.

## Strategic verdict

~**85–90% of this is buy / assemble**, not build. The infrastructure (agent runtime, memory,
skills, multi-agent board, wallet plumbing, data reach, observability, policy) is all off-the-shelf.
**The infrastructure is therefore NOT the moat** — if everyone can assemble it in a weekend, it
cannot be the edge.

**The three things that are yours, and hard:**

1. **Discovery** — *which* wallets/signals belong on the watchlist, and keeping it alive as edges
   decay and crowds copy them. Clustering is solved (godmode); monitoring is solved infra;
   **discovery is the actual alpha and nobody hands it to you.** Flip the off-the-shelf tools from
   *defensive* (detect bundlers to avoid) to *offensive* (find winners to follow).
2. **Expert-distillation flywheel** — your blind-first judgments captured as labels → rules →
   policies. The one thing better models cannot clone, because it is *your* data.
3. **Eval / holdout discipline that wraps everything — including the self-evolution.** Without a
   ground-truth eval, a self-evolving async agent confidently optimizes toward nothing — while you
   sleep.

**The real risk is not buildability — it is whether edge exists.** The edge equation is
multiplicative (information × evidence × execution × learning × capacity). If the signal has no
predictive value, all the governance produces a perfectly-audited zero. So build the system to
**disprove edge cheaply and protect capital while you find out** — not assuming edge is there.

## Where it stands (SDLC frame)

Per current frontier consensus (Google's AI-Driven SDLC; Anthropic context engineering;
"Agent = Model + Harness, ~90% harness"):

- **Spec / Requirements** — *over-delivered.* World-class (v1, v2 spec, backlog, source register).
- **Architecture / Design** — done.
- **Implementation** — *nothing running.* (Now cheap and fast — minutes to hours.)
- **Verification** — *nothing running.* (Output + trajectory eval = the differentiator.)

**The bottleneck moved off spec and onto implementation + verification. The fix is not more spec —
it is to run one cycle.**

## Decisions made

- Build in a **dedicated private repo** (see `ADR-000`). The research hub stays the library.
- **First deliverable = a read-only, no-capital vertical slice:** *Call Channel + Holder Intelligence
  Lab.* Watch 10–20 call channels; at each call, snapshot on-chain holder behavior. Exercises ~70%
  of the P0 backlog (capture, evidence bundles, blind labels, samplers) with zero money at risk;
  running artifact in ~a week.
- **No capital path until the evidence loop is proven.** Crypto.com / exchange MCPs stay **OFF**.
  Trading graduates only after replay + anti-alpha + execution-quality + forward-test gates.
- **Governance = OPA + deterministic reflex layer** next to the execution gateway. Cloudflare is
  perimeter only (Tunnel / Access / Workers), never the authority layer.

## Stack (concrete)

- **Agent / orchestration:** Hermes Agent on a ~$5 VPS (Docker + systemd linger).
- **Solana data:** Helius (RPC + webhooks/Geyser), QuickNode; Birdeye / DexScreener (price); Dune
  (analytics / backtest).
- **Execution quality:** Jupiter (quotes / routes / simulation).
- **Wallet intel:** fork `godmode` or mount `helius-forensics-mcp` (Helius free tier covers a
  ~100-wallet daily refresh).
- **Ledger / storage:** Supabase/Postgres (canonical, append-only) + object storage (R2 / Backblaze)
  for raw evidence.
- **Governance:** OPA (policy-as-code).
- **Observability:** Prometheus + Grafana + OpenTelemetry (+ Langfuse for agent traces).
- **Memory:** Hermes built-in + Honcho (multi-agent); others later.
- **Knowledge:** Notion.
- **Agent MCPs (keep it ~5–6):** GitHub, Supabase, QuickNode, a research/web tool, Notion, Context7.

## Open questions

- VPS host (leaning Hetzner; let deploy requirements decide).
- Confirm repo visibility on the `symphony` fork; move/redact `MASTER_CONTEXT.md` if public.
- Verify the external arXiv citations in the v2 Source Register (the likeliest place for
  fabricated-but-plausible IDs).
- Which memory provider beyond Hermes built-in (Honcho is the lead).

## Next action

Stand up Hermes on a $5 VPS → wire wallet intel (godmode / helius-forensics-mcp) → build the only
parts that are yours: a thin **discovery loop** (recent winners → candidate watchlist) and a
**blind-first expert-label card** (you judge before seeing the agent's output; it records and
learns) → run read-only, shadow, zero capital. Every yes/no becomes training data from day one.
