PROJECT B.O.S.S.
Hermes Solana Edge Stack
Canonical Build Spec v1
Signal from noise. Determinism before autonomy. Evidence before execution.




How to read this document
This is written as both an executive operating thesis and a build draft. The first three sections explain why the Pulse corpus matters and what to keep versus kill. The middle sections define the Hermes architecture, agents, data contracts, signal objects, gates, memory, and evidence layer. The last sections define the roadmap, sprint plan, schemas, metrics, and research backlog.

1. Executive summary - the real opportunity
Here is the blunt version: the Pulse corpus is not a grab bag of random crypto-bot ideas. It is converging on a real institutional pattern. The through-line is that durable edge does not come from one clever indicator. It comes from an intelligence factory that observes faster, normalizes cleaner, rejects bad opportunities more aggressively, proves what it saw, sizes only into executable liquidity, and then learns from every decision.
That is why these notes felt different. Most retail “AI trading” material jumps straight to prediction. These suggestions repeatedly come back to deterministic sampling, evidence bundles, append-only memory, agent trust, anti-alpha gates, replayable backtests, slippage probes, and forensic traceability. Those are the ingredients of a professional research and execution stack, not a hype demo.
The central design decision is this: Hermes should use GPT-5.5 as a reasoning and orchestration brain, not as an unconstrained trade predictor. The LLM should decide what to investigate, which tools to call, how to synthesize contradictions, which hypotheses to falsify, and when to escalate. It should not be allowed to execute merely because a chart looks interesting or a social channel is hot. Execution should pass through deterministic gates, typed schemas, replayable evidence, and risk controls.
The edge we want is asymmetric. The winning loop is not “be right every time.” It is “see earlier, verify harder, abstain more often, size better, and learn faster.” In Solana, where markets are adversarial, fast, thin, and spoofable, the stack must be built around avoiding false positives as much as catching true moves.

At a C-suite level, the investment case is simple. This stack gives the team a disciplined path from “interesting on-chain anomaly” to “verified, size-aware opportunity.” It creates a repeatable decision membrane between raw noise and capital at risk. Every decision can be audited, replayed, and improved. That is the difference between a clever bot and a true trading intelligence platform.
1.1 The edge equation
The stack should optimize the following equation:
edge = (freshness * evidence_quality * falsification_discipline * execution_quality * learning_rate)
       - (latency_cost + vendor_error + overfitting + slippage + adversarial_decay)
This equation is not meant as math theater. It is an architectural constraint. Every feature should either increase one of the positive terms or reduce one of the negative terms. If a feature does neither, it is noise.
1.2 What changes after reading the Pulse corpus
The “canonical object” is no longer just a signal. It is a trade_card backed by evidence, replay metadata, anti-alpha checks, liquidity proof, and a deterministic decision id.
The first MVP should not be a trading bot. It should be a 72-hour forward-test and evidence loop that can prove whether one Solana signal family survives real-time data, slippage, and forensic checks.
Agent memory should be append-only and provenance-heavy from day one. Updating facts in-place creates silent corruption; adding records and linking lineage creates institutional memory.
Prometheus/OpenTelemetry/Grafana are not “nice ops dashboards.” They are the guardrail layer that decides whether agents are allowed to act.
Jito/ShredStream/ultra-low latency should be treated as a later acceleration layer, not the foundation. First prove signal quality, liquidity, and replayability; then speed it up.
Telegram/KOL burst detection is interesting, but it is not a primary alpha source until it is cross-validated against wallet movement, liquidity, and repeated outcomes.
2. What the Pulse corpus is really saying
The Pulse paste contains many small patterns, but they cluster into a very coherent system. The dominant themes are below.

2.1 The most important through-line
The strongest through-line is not “use more data.” It is “force every data point to earn trust.” The stack should ingest real-time data, but it should also rate-limit itself, sample deterministically, hash evidence, compare vendors, backtest anchors, and withhold execution when telemetry is stale. In a Solana environment full of wash volume, sybil behavior, spoofed liquidity, social manipulation, copy-trading, and survivorship bias, this is not optional. It is the edge.
2.2 The architectural north star

3. Signal vs noise - what to keep, bend, or defer
Not everything in the Pulse corpus should be built immediately. The most valuable ideas are the ones that compound reliability. The most dangerous ideas are the ones that look advanced but would create premature complexity or false confidence.

3.1 Biggest useful insight from outside the paste
The frontier lesson from LLM trading research is sobering and useful: an LLM does not automatically become an alpha engine because it can reason or use tools. Realistic trading benchmarks show that many LLM agents struggle to beat simple baselines, even when they can process market signals. That does not weaken Hermes; it clarifies its role. Hermes should not rely on “model intuition” as alpha. It should use GPT-5.5 to run disciplined research workflows, generate hypotheses, select tools, explain contradictions, enforce schemas, and improve the loop.
In other words: the AI advantage is in orchestration, research velocity, instrumentation, and falsification. The market advantage comes only after those workflows produce validated, executable, low-slippage, risk-adjusted signals.
4. Target-state architecture
Hermes should be designed as three connected loops. Each loop is independently useful, but the edge emerges when they reinforce each other.

A simplified pipeline:
sources -> event bus -> normalized stores -> signal detectors -> candidate registry
        -> evidence workers -> anti-alpha gates -> liquidity replay -> trade_card/reject_card
        -> human/shadow/probe/execute -> post-trade attribution -> memory + trust updates
4.1 Reference stack

4.2 Event bus and storage shape
The event bus should be intentionally boring. Kafka, Redpanda, or NATS JetStream can all work. The priority is deterministic ordering, replay offsets, dead-letter queues, and explicit schema versioning. Do not let agents consume untyped blobs directly from vendors. Vendors publish into adapters; adapters normalize; agents read normalized contracts.

5. Hermes as an agent operating system
Hermes should be implemented as an agent council with strict contracts. GPT-5.5 is the brain that reads, reasons, compares, and plans, but every high-risk step is mediated by typed tool calls, guardrails, deterministic outputs, and human or system approval. The most important principle is role separation: the agent that discovers a signal should not be the same agent that approves execution.

5.1 Autonomy ladder

The critical policy: agents do not become autonomous by being impressive. They become autonomous by accumulating evidence-backed, replayable decisions with acceptable false-positive and drawdown behavior.
5.2 Agent trust scoring
Trust should be measured per agent and per signal family. Use EWMA to smooth recent performance while allowing trust to decay or recover. Trust observations should be decomposed by reason: schema validity, tool-use precision, evidence completeness, prediction calibration, abstention quality, and realized execution quality.
agent_observation = weighted_sum(
  schema_pass,
  tool_use_precision,
  evidence_completeness,
  prediction_calibration,
  correct_abstention,
  post_trade_outcome,
  risk_compliance
)

trust_new = alpha * agent_observation + (1 - alpha) * trust_prev
Use hysteresis for autonomy: block below 0.35, recover only above 0.45, and require no critical telemetry gaps. A low-trust agent can still research, but it cannot directly promote trade drafts.
6. Data source strategy - useful integration, not vendor soup
The Pulse material names a strong vendor stack, but the key is to assign each vendor a job and never let any one vendor become truth. Hermes should cross-validate freshness, labels, transactions, prices, and depth across source classes.

6.1 Source freshness and conflict policy
Every source should publish freshness and confidence metrics. A candidate cannot be promoted if the primary source is stale, if the secondary source contradicts it materially, or if a vendor response is missing required lineage.
source_health = {
  source,
  last_seen_block_time,
  last_message_ts,
  ingest_lag_ms,
  error_rate_5m,
  schema_version,
  freshness_status: fresh|warning|stale,
  confidence: 0.0..1.0
}
7. Canonical signal taxonomy
Hermes should treat each signal family as a research product with its own features, gates, backtests, baselines, and retirement rules. Do not mix signal families into one vague alpha score too early.

7.1 Signal promotion standard
A signal family graduates only when it passes five hurdles:
Definition: typed features, windows, thresholds, and data sources are frozen for the test period.
Replayability: anchors and outcomes can be reconstructed from stored artifacts.
Baseline: performance is compared to simple baselines, random anchors, and liquidity-matched controls.
Execution realism: returns are net of routeable slippage, fees, and failed fills.
Forward proof: 72h to 30d shadow outcomes are good enough to justify micro-probes.
8. Canonical objects and data contracts
The system needs a small number of canonical objects. These are more important than dashboards. Once the objects are stable, agents, dashboards, backtests, and execution can all speak the same language.
8.1 candidate_signal
{
  "schema_version": "candidate_signal_v1",
  "candidate_id": "cand:<timestamp>:<mint>:<family>:<hash>",
  "created_at_utc": "ISO8601",
  "signal_family": "persistence|second_leg|wallet_cluster|liquidity_migration|kol_rotation|launch_quality|execution_quality",
  "chain": "solana",
  "symbol": "string|null",
  "token_mint": "string",
  "venue_or_pair": "string|null",
  "features": {"typed_feature_name": "value"},
  "source_refs": [{"source":"birdeye|dune|rpc|helius|tardis|arkham|nansen", "ref":"uri-or-id", "freshness":"fresh|warning|stale"}],
  "detector": {"name":"string", "version":"semver", "params_hash":"sha256:..."},
  "raw_event_hashes": ["sha256:..."],
  "status": "new|evidence_requested|rejected|promoted|expired"
}
8.2 evidence_bundle
{
  "schema_version": "evidence_bundle_v1",
  "decision_id": "uuid-or-deterministic-id",
  "candidate_id": "cand:...",
  "created_at_utc": "ISO8601",
  "replay_epoch": "YYYY-MM-DD-or-run-id",
  "sampler": {"version":"v1", "salt_id":"release-2026-05", "default_rate_pct":0.1, "override_rate_pct":1.0},
  "tx_samples": [{"tx_sig":"...", "slot":0, "commitment":"finalized", "rpc_artifact_uri":"s3://...", "tx_json_hash":"sha256:..."}],
  "market_artifacts": {"birdeye_refs":[], "tardis_snapshot_ids":[], "jupiter_quote_refs":[]},
  "entity_artifacts": {"arkham_profile_ids":[], "nansen_label_refs":[]},
  "forensic_scores": {"wash_score":0, "sybil_score":0, "label_entropy":0, "memo_pattern_flag":false},
  "proof": {"manifest_uri":"s3://.../manifest.json", "manifest_sha256":"sha256:...", "signed_by":"key-id"}
}
8.3 trade_card
{
  "schema_version": "trade_card_v1",
  "decision_id": "tc:<timestamp>:<mint>:<family>:<version>",
  "timestamp_utc": "ISO8601",
  "market": {"chain":"solana", "symbol":"...", "token_mint":"...", "venue":"...", "side":"buy|sell|none"},
  "thesis_text": "One or two sentence evidence-backed thesis.",
  "signal": {"family":"...", "strength":0.0, "confidence_percentile":0, "confidence_method":"empirical-windowed-ewma", "n_matches":0},
  "sizing": {"suggested_size_usd":0, "available_depth_usd":0, "slippage_estimate_bps":0, "max_slippage_bps":0, "liquidity_use_fraction":0.0},
  "anti_alpha": {"checks_passed":false, "hard_fails":[], "soft_warnings":[], "wash_score":0, "spoof_flag":false, "tiny_liquidity_flag":false, "depth_retreat_flag":false},
  "execution_plan": {"mode":"human|shadow|probe|live", "route_provider":"jupiter", "send_provider":"none|jito", "ttl_seconds":0},
  "evidence_refs": {"bundle_uri":"...", "sample_txids":[], "dune_permalink":"...", "manifest_sha256":"sha256:..."},
  "manual_review_required": true,
  "fallback_reason": "string|null"
}
8.4 reject_card
The reject_card is as important as the trade_card. A sophisticated system should collect “why not” data, because correct abstention is one of the largest sources of risk-adjusted edge.
{
  "schema_version": "reject_card_v1",
  "candidate_id": "cand:...",
  "decision_id": "rej:<timestamp>:<mint>:<family>:<version>",
  "reasons": ["STALE_DATA", "LIQUIDITY_SLIPPAGE_GT_LIMIT", "WASH_SCORE_GT_LIMIT", "NO_HISTORICAL_COHORT"],
  "debug": {"z":0, "unique_buyers_4h":0, "slippage_bps":0, "limit_bps":0},
  "evidence_refs": {"bundle_uri":"..."},
  "learning_tags": ["correct_abstention_candidate", "needs_backtest", "vendor_conflict"]
}
9. Anti-alpha gates - the decision membrane
The anti-alpha gate is where this stack starts to become powerful. It should assume every signal is guilty until it survives falsification. The goal is not to perfectly detect every manipulation pattern. The goal is to block the obvious traps, force evidence into every decision, and make false-positive promotion measurable.

9.1 Sizing logic
The Pulse sizing formula is directionally right: tie size to executable depth, confidence, and volatility. It needs one critical adjustment: all units must be standardized. Volatility must be fractional, not sometimes percent and sometimes decimal. Slippage should not be a linear approximation once the replay layer exists; use actual route/depth simulation whenever possible.
base_liquidity_size = available_depth_usd * liquidity_use_fraction_max
confidence_adj = confidence_percentile / 100
volatility_adj = max(0.25, 1 + ewma_volatility_fraction)
raw_size = floor(base_liquidity_size * confidence_adj / volatility_adj)
size = clamp(raw_size, min_size_usd, max_size_usd)

hard_fail if simulated_slippage_bps(size) > max_slippage_bps
hard_fail if available_depth_usd < portfolio_usd * tiny_liquidity_fraction
For very small Solana tokens, fixed $25k/$50k/$100k probes are often too large. Probe sizes should be dynamic: start at a tiny fraction of available 1% depth, then ladder only if realized slippage and depth persistence pass.
10. Research and backtesting discipline
The Pulse backtesting material is one of the highest-signal parts of the corpus because it recognizes that a detector is not useful until it creates deterministic anchors and forward outcomes. Hermes should make backtesting an artifact pipeline, not an analyst memory exercise.

10.1 Validation rules
UTC everywhere; deterministic rounding for anchors; no feature may peek beyond anchor time.
Freeze detector params before forward tests. Any threshold change creates a new detector version.
Compare against random anchors, liquidity-matched anchors, and simple momentum/volume baselines.
Use walk-forward and purged/embargoed splits where time leakage is plausible.
Track the number of trials. If many variants are tested, correct for multiple testing using Deflated Sharpe / PBO / Reality Check style methods.
Promote only after both historical and forward evidence survive slippage and execution assumptions.
Record rejected hypotheses. A hidden graveyard of failed backtests is how teams fool themselves.
10.2 First signal family to test
The best first candidate is a combined persistence + second-leg continuation detector. It is concrete, observable, and testable quickly: on-chain buy pressure persists, independent wallets continue buying, price follows through, and L2/depth remains strong enough for the intended size. It avoids the worst trap of pure social/KOL signals and creates a direct path into liquidity-aware sizing.
candidate if:
  hour_ewma_buy_usd_z > 2.5
  persistence_streak_10m >= 3
  unique_funded_buyers_4h >= 3
  mid_price_change_5_to_15m > configured_min
  min_depth_top10_5m > target_size_usd * depth_safety_mult
  source_freshness == true

promote only if:
  anti_alpha_pass == true
  simulated_slippage_bps <= limit
  historical_cohort_n >= minimum_n or status == research_only
11. Execution and risk architecture
Execution should be treated as a separate product surface from signal discovery. A signal can be “true” and still be a terrible trade if route quality is poor, depth is fragile, or the act of trading reveals the opportunity. Hermes should therefore move through an execution ladder: shadow quote, micro-probe, staged POV, restricted live, and only later latency optimization.

11.1 Kill switches

12. Observability, evals, and governance
The Pulse observability material is very strong, but one adjustment matters: Prometheus Pushgateway should be used mainly for batch jobs and short-lived jobs, while long-running services should expose scrapeable /metrics endpoints. This avoids stale metrics and aligns with Prometheus best practices. Hermes can still use Pushgateway for Dune batch workers, evidence packagers, backtest jobs, and nightly agent eval exports.

12.1 Agent eval suite
Nightly and pre-deploy agent evals should cover five base metrics from the Pulse corpus: task success rate, hallucination/factual error rate, tool-use precision, throughput/cost ratio, and memory consistency. For Hermes, add four trading-specific metrics: evidence completeness, correct abstention, calibration, and schema compliance.

12.2 Trace design
Every important run should produce an OpenTelemetry trace with spans that map the decision path: candidate detection, evidence sampling, forensic check, liquidity replay, risk gate, execution quote, approval, and postmortem. The trace id should be stored in candidate_signal, evidence_bundle, trade_card, and agent_trust observations.
trace: hermes_decision_run
  span: candidate_detection
  span: evidence_sampling
  span: entity_enrichment
  span: anti_alpha_gate
  span: liquidity_replay
  span: trade_card_validation
  span: risk_approval
  span: execution_quote_or_probe
  span: post_trade_attribution
13. Memory architecture
Hermes memory should be append-only, provenance-rich, and retrieval-aware. This is one of the places where the project can become genuinely powerful over time. Every signal, rejection, trade draft, evidence bundle, postmortem, and research note becomes a future training example for the system’s judgment.

13.1 Memory rules
Never mutate a primary fact record. Add a superseding record with valid_from/valid_to or supersedes pointer.
Every record stores source, source_id, actor, ingest time, schema_version, confidence, and canonical_hash.
Embeddings are an index, not truth. Retrieval results must cite source records and confidence.
Contradictions are first-class. Store label conflicts and teach the reader to prefer recency + source quality + corroboration.
Redaction and privacy hooks should mask on read, not rewrite append-only records.
14. Operator interface - what the human should see
The dashboard ideas are good, but they should be built around decisions rather than “cool screens.” The user should be able to answer five questions in seconds: What is moving? Who is moving it? Is liquidity real? What killed or promoted the signal? What evidence can I inspect?

15. Build roadmap
The fastest path is not to build everything. The fastest path is to build the smallest loop that proves the architecture: one or two signal families, one evidence path, one liquidity path, one trade_card schema, one eval loop, and one dashboard view.

15.1 First two-week sprint

15.2 Suggested repo layout
hermes/
  apps/
    api/                         # FastAPI/Node API for control plane
    dashboard/                   # Minimal operator UI
    workers/
      birdeye_ws_worker/
      dune_anchor_worker/
      rpc_evidence_worker/
      signal_detector_worker/
      backtest_runner/
      trust_exporter/
  packages/
    schemas/                     # JSON schemas + Pydantic/Zod models
    sampler/                     # deterministic sampler + token bucket + hash utils
    gates/                       # anti-alpha, source freshness, liquidity, schema gates
    agents/                      # Hermes agent definitions, tools, guardrails
    metrics/                     # Prometheus/OTel helpers
  sql/
    migrations/
    views/
    dune_queries/
  configs/
    signal_families/
    risk_limits/
    source_registry.yaml
  evidence/
    README_artifact_layout.md
  tests/
    fixtures/
    unit/
    integration/
    replay/
16. Build specs by module
16.1 Deterministic sampler module
The sampler is a core primitive. It should be packaged as a small library used by evidence workers and forensic jobs. Requirements: deterministic HMAC sample, replay_epoch support, sampler_version, per-mint sample controls, token bucket rate limiting, batch RPC support, and proof_hash helper.

16.2 Anti-alpha gate module
The anti-alpha module should be deterministic, unit tested, and explainable. It should return structured hard_fails and soft_warnings instead of a vague score.
gate_result = {
  "checks_passed": bool,
  "hard_fails": [{"code":"TINY_LIQUIDITY", "evidence":"..."}],
  "soft_warnings": [{"code":"KOL_FLOW_FLAG", "evidence":"..."}],
  "scores": {"wash_score":0.0, "sybil_score":0.0, "depth_retreat_ratio":0.0},
  "required_review": bool
}
16.3 Liquidity replay module
Liquidity replay should output simulated fill quality by size and time bucket. For CEX markets, Tardis L2 makes this straightforward. For Solana DEX pools, use pool reserves, Jupiter routes, Birdeye trades, and any available depth/quote snapshots. Never rely only on a single point quote.

16.4 Backtest runner module
The backtest runner must be boring and strict. It should refuse to run if detector versions, feature windows, or price/liquidity sources are not pinned.

16.5 Hermes agent module
The agent module should use tools as typed capabilities. The agent is not allowed to “know” market state from chat. It must retrieve it from tools. Its output should be strict JSON when it is performing operational work.
tools:
  search_memory(query)
  get_source_health(source)
  get_candidate(candidate_id)
  create_evidence_bundle(candidate_id)
  run_anti_alpha(candidate_id, evidence_bundle_id)
  run_liquidity_replay(candidate_id, size_ladder)
  validate_trade_card(trade_card)
  request_human_approval(trade_card)
  write_postmortem(decision_id)

guardrails:
  no_trade_without_valid_trade_card
  no_execution_if_source_stale
  no_execution_if_agent_trust_below_threshold
  no_social_only_promotion
  no_missing_evidence_refs
17. Research backlog

18. What I would not build yet
The easiest way to lose the edge is to build impressive-looking machinery before the evidence loop exists. I would intentionally defer or constrain the following:
Full autonomous live trading. It creates risk before we know which signal family has net edge.
A sprawling social/KOL platform. Build a small controlled archive and prove causality first.
Raw-shred/HFT infrastructure as phase one. Speed amplifies good signals and bad signals equally.
Overfit parameter grid searches without multiple-testing correction and full trial logs.
A beautiful multi-panel dashboard before the trade_card/reject_card/evidence_bundle objects are stable.
Heavy local GPU hosting unless privacy/cost/latency actually becomes a bottleneck.
Blind trust in “smart money,” KOL, or exchange labels. Labels are features, not decisions.
19. Operating principles
No evidence, no trade_card.
No valid trade_card, no execution.
No source freshness, no promotion.
No replay, no research claim.
No postmortem, no learning.
No agent trust, no autonomy.
No slippage proof, no sizing.
No single-vendor truth for high-risk decisions.
Rejected candidates are assets; store and learn from them.
Every threshold change is a new version, not a quiet edit.
20. Canonical next step
The immediate next step is to build a small, ruthlessly instrumented Hermes v1 demo around one signal family: persistence + second-leg continuation for selected Solana tokens. The goal is not profit yet. The goal is to prove the loop can detect, sample, package, gate, replay, and explain opportunities in real time.


Appendix A - Pulse corpus map
The Pulse corpus was treated as raw design signal. The following map groups the pasted suggestions into canonical Hermes modules.

Appendix B - External source spine
These are the external references used to validate and shape the build draft. The document uses them as architecture and research support, not as a claim that any vendor or method guarantees trading profits.

Appendix C - Minimum viable database tables
tables:
  source_health(source, last_seen_ts, ingest_lag_ms, error_rate_5m, schema_version, status)
  candidate_signals(candidate_id, created_at, family, mint, features_json, source_refs_json, status)
  forensic_evidence(id, decision_id, tx_sig, slot, token_mint, sampler_version, sample_rate_pct, tx_json, proof_hash)
  evidence_bundles(bundle_id, candidate_id, manifest_uri, manifest_sha256, created_at, source_refs_json)
  trade_cards(decision_id, candidate_id, trade_card_json, status, created_at, trace_id)
  reject_cards(decision_id, candidate_id, reasons_json, debug_json, created_at, trace_id)
  memory_fragments(id, created_at, agent_id, fragment_json, canonical_hash, source, source_id, version)
  memory_provenance(id, fragment_id, event_type, event_ts, actor, meta_json)
  agent_runs(run_id, agent_id, started_at, completed_at, trace_id, task_type, status, output_hash)
  agent_trust(agent_id, ewma, last_observed, sample_count, half_life_seconds, trace_id, decision_id)
  signal_family_scores(family, version, ewma_precision, n, last_promoted_at, status)
  backtest_anchors(anchor_id, family, version, mint, anchor_ts, features_json, sample_txids_json)
  backtest_outcomes(anchor_id, ret_1h, ret_6h, ret_24h, ret_72h, slippage_bps, anti_gaming_ok)
Appendix D - Canary questions for each agent

Appendix E - Final stance
The Pulse material is strongest where it behaves like institutional infrastructure: deterministic sampling, evidence bundles, anti-alpha gates, slippage proof, append-only memory, agent trust, evals, and replay. It is weakest where it tempts us to chase sophistication before proof: social signals without causality, label worship, shiny dashboards, and premature low-latency execution. The build path is clear: create the loop, prove one signal family, then expand. That is how Hermes becomes more than a bot. It becomes a compounding edge system.