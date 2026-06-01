# ICM, the Filesystem-as-Cognition Pattern, and Where It Actually Sits

*A response for sablekeys. Written to your spec: source → context inside the source → step-by-step reasoning → conclusion → connections → unknown unknowns.*

---

## TL;DR (read this first)

1. **ICM is real, but narrower than the marketing suggests.** It is an arXiv preprint by **Jake Van Clief** (@JEVanClief — the same guy replying "you get it perfectly" in your screenshot) and **David McDermott**, "Eduba, University of Edinburgh," posted ~March 2026 as **arXiv:2603.16021**, MIT-licensed reference repo at `github.com/RinDig/Interpretable-Context-Methodology-ICM-` (559★). The skeptic (@NonameDerp) is technically right: it is **not yet peer-reviewed**. "Submitted to ACM TiiS" means *under review at* ACM Transactions on Interactive Intelligent Systems — that's an aspirational claim, not a publication. And the "MIT" in the GitHub repo is the **MIT software license**, not Massachusetts Institute of Technology. (NonameDerp conflated those two, which weakens the "liar" call — but the publication-status hedge is fair.)
2. **The sarcastic comment (@MultiMyNickName) is half right and entirely wrong.** Yes, "use folder structure" is common-sense project management. But ICM's actual contribution isn't "use folders" — it's a *specific layered context-loading discipline* (Layers 0–4, with a hard structural split between Layer 3 "constraints / the factory" and Layer 4 "input / the product"). That split is the engineering claim, and it's not what PMs have always done. It comes from Unix pipelines + multi-pass compilers + Parnas's information hiding, applied to LLM context windows. That's the part PMs without an LLM-context-engineering frame keep missing.
3. **The five layers in the YouTube comment map cleanly onto the paper.** Identity → Routing → Stage Contract → Reference Material → Working Artifacts is a *visualization* of the paper's Layer 0 → 1 → 2 → 3 → 4. The commenter (@jtraveler888) got it right; Van Clief confirmed it.
4. **ICM is one specific instance of a much larger pattern** that the agent-builder world is converging on: *the filesystem as the agent's durable cognition substrate.* That pattern shows up — independently — in (a) Anthropic's Claude Skills / SKILL.md, (b) the emerging cross-tool **AGENTS.md** convention (OpenAI Codex, Cursor, Claude Code all read it), (c) Jesse Vincent's *Superpowers* harness, (d) Simon Willison's parallel-agent worktrees, (e) academic papers like **InfiAgent** (file-centric state for long-horizon agents) and **ACE** (context as evolving playbook). ICM is a clean, teachable, narrow version of this pattern for **sequential, human-reviewed workflows**. That is its sweet spot and also its ceiling.
5. **For your Hermes Solana stack and your lead-gen agency, ICM is necessary but not sufficient.** It gives you the cognitive *substrate*. What it doesn't give you is the *control plane* — evals, anti-alpha gates, evidence-vs-claim separation, provenance, agent trust scoring, governance against memory poisoning. That second layer is what your `Hermes_Solana_Edge_Canonical` doc already correctly insists on. Marry the two and you have something serious.

Now the long version.

---

## Part 1 — What ICM actually says (sourced, with the actual context inside the source)

I read the arXiv paper (`arxiv.org/abs/2603.16021`), the canonical GitHub repo, the LLM-Wiki summary, and the Lyceum Skool community posts. Here is what the paper claims, with the actual quotes:

### 1.1 The thesis (paper abstract, verbatim)

> "Current approaches to AI agent orchestration typically involve building multi-agent frameworks… These frameworks work well for complex, concurrent systems. But for sequential workflows where a human reviews output at each step, they introduce engineering overhead that the problem does not require. This paper presents Interpretable Context Methodology (ICM), a method that replaces framework-level orchestration with filesystem structure. Numbered folders represent stages. Plain markdown files carry the prompts and context that tell a single AI agent what role to play at each step."
> — *arxiv.org/abs/2603.16021*, Abstract

**Notice what this paper is *not* claiming.** It is not claiming to be a general theory of agency. It is not claiming to solve multi-agent orchestration. It is explicitly scoped to *sequential* workflows with *human review at each step*. That scope matters — and almost every YouTube hype-take strips it off.

### 1.2 The five-layer architecture (paper §3, GitHub README)

| Layer | Filename in repo | The agent's question | Tokens | Changes per run? |
|---|---|---|---|---|
| 0 — Identity | `CLAUDE.md` (root) | "Where am I?" | ~800 | No |
| 1 — Routing | `CONTEXT.md` (root) | "Where do I go?" | ~300 | No |
| 2 — Stage Contract | `stages/NN-name/CONTEXT.md` | "What do I do here?" | ~200–500 | No |
| 3 — Reference Material | `_config/`, `references/` | "What rules apply?" (the *factory*) | varies | No |
| 4 — Working Artifacts | `stages/NN-name/output/` | "What am I working with?" (the *product*) | varies | **Yes** |

The mechanically important claim is the **Layer 3 vs Layer 4 split**:

> "Layer 3 material needs to be internalized as constraints and patterns — write *like this*, use *these colors*, follow *these conventions*. Layer 4 material needs to be processed as input — transform *this research* into a script, convert *this script* into a specification."
> — *RinDig/Interpretable-Context-Methodology-ICM-, README, §"How It Works"*

That distinction is the actual engineering insight. Most people throw everything into one mega-prompt. ICM's claim is that structurally separating "rules I should obey" from "stuff I should transform" gives the model cleaner signals and produces measurably better output.

### 1.3 The token-math claim

> "Each stage: 2,000–8,000 focused tokens. Monolithic equivalent: 30,000–50,000 tokens (most irrelevant to current task). Avoids 'lost in the middle' degradation (Liu et al.) by construction — irrelevant tokens are never loaded."
> — *LLM Wiki summary of ICM*

This is the paper's empirical anchor. It rides on a real, well-cited 2023 paper: **Liu et al., "Lost in the Middle: How Language Models Use Long Contexts" (arXiv:2307.03172)**, which showed that LLMs systematically under-attend to information in the middle of long contexts. ICM's response is: *don't try to compress the middle, never put it there in the first place.*

### 1.4 The five design principles (paper §3)

1. **One stage, one job** — Unix + Parnas's information hiding.
2. **Plain text as the interface** — markdown/JSON only, no binary, anything can read it.
3. **Layered context loading** — prevention, not compression.
4. **Every output is an edit surface** — a human can open/edit any intermediate artifact between stages.
5. **Configure the factory, not the product** — the workspace is set up once and run many times.

### 1.5 What the paper says it is NOT for (paper §5)

> "Works: Sequential workflows, human review at each stage, repeatable pipelines… Doesn't work: Real-time multi-agent collaboration, high-concurrency systems, complex automated branching."

**Burn this in.** The paper itself disqualifies ICM from concurrent multi-agent work. That is not a critic's complaint; it's the authors' own scope. So when you build Hermes — which *is* concurrent, multi-agent, and adversarial — ICM cannot be the whole architecture. It can be the substrate, but you need another layer on top.

---

## Part 2 — My step-by-step reasoning

You asked me to walk through my thinking, not just hand you a conclusion. Here it is.

**Step 1 — Establish whether this is real or marketing.** First question: is "ICM" a thing or a creator-economy invention? Found the arXiv paper, the GitHub repo (MIT-licensed, 559 stars, actual code, with worked example workspaces), a community of practitioners on Skool with concrete implementations, and independent third-party summaries (LLM Wiki on imfsoftware.com). Verdict: real artifact. The methodology exists, it has a written specification, and other people are using it. Not a vaporware course.

**Step 2 — Test the skeptical comment.** @NonameDerp says "submitted to ACM TiiS" is being misrepresented as "published, peer-reviewed." I couldn't find a Lyceum marketing page making that exact bold claim, so I can't fully validate NonameDerp's accusation, but his underlying epistemics are sound: *"submitted to" is not "published in,"* and any creator who blurs that line is overclaiming. Right now ICM is an **arXiv preprint** — that means uploaded by the authors, not refereed. Treat it as a frontier signal, not settled doctrine.

**Step 3 — Test the dismissive comment.** @MultiMyNickName says "you didn't invent this, every PM does it." Half-true. Folder structure is ancient. *But* "use folders" ≠ ICM. ICM's specific contribution is the Layer 3/4 split for LLM context plus the discipline that **only the current stage's slice gets loaded**. That is a context-engineering claim, not a PM claim. PMs were not doing it because PMs were not in the prompt-construction business. Engineers who built CrewAI/LangChain were, and they went the *opposite* way — toward heavier framework code. ICM is a deliberate countermove. So the dismissive comment confuses two different problems (organizing humans vs. organizing an LLM's context window).

**Step 4 — Figure out where ICM sits in the broader landscape.** I cross-referenced ICM against (a) the **AGENTS.md** convention now adopted by Codex, Cursor, and Claude Code, (b) Anthropic's **Claude Skills** (SKILL.md files), (c) Jesse Vincent's **Superpowers** harness, (d) Simon Willison's worktree-based parallel agents, (e) the **ACE** paper on "context as evolving playbook," (f) the **InfiAgent** paper on file-centric state for long-horizon agents. They're all converging on the same primitive — the filesystem as durable agent state — from different starting points. ICM is the simplest, most pedagogically clean version. AGENTS.md is the lowest-common-denominator industry standard. Skills are the modular reusable version. Superpowers is the heavy multi-agent + worktree version. ACE/InfiAgent are the academic versions. ICM is one node in a family.

**Step 5 — Test the depth claim.** You said it feels like the "missing piece." I think it is *a* missing piece, not *the* missing piece. The actual missing piece for your work is bigger than ICM: it's **harness engineering** — the whole loop of plan → context → act → verify → memorize → hand off → govern. ICM gives you the filesystem half. It does not give you the eval half, the governance half, or the multi-agent half. That's why your Hermes doc is correctly insisting on evidence cards, anti-alpha gates, agent trust scoring, append-only memory, and replay. Those are the parts ICM consciously *doesn't* cover.

**Step 6 — Form the teaching.** Reframe ICM not as a discovery but as one specific naming of a pattern you already half-have. Then layer it: where ICM is the right tool, where it's the wrong tool, what to add on top.

---

## Part 3 — The conclusion (the teaching)

### 3.1 The single sentence to remember

> **ICM is the right pattern for sequential, single-agent, human-reviewed workflows where the win is editability and inspection. It is the wrong pattern for concurrent, adversarial, autonomous-execution work — but its primitives (filesystem-as-state, layered context, edit surfaces) are still the foundation those harder systems sit on.**

### 3.2 The five-rung ladder you should internalize

(This is mine, distilled from the corpus you sent + what I found.)

1. **Files as storage.** Beginners. "I keep my notes organized." Useful, not yet agentic.
2. **Files as memory.** The agent writes durable state so it doesn't carry the world in its context window. This is where long-horizon work starts being possible.
3. **Files as context routing.** The harness tells the agent *which file to load when*. This is what ICM names. Without it, the model drowns. With it, every stage gets a clean ~2–8k-token slice.
4. **Files as control plane.** Files don't just feed the agent — they *govern* it. Stage contracts say what may be produced. Policy files say what may not be done. Eval files say when a stage is complete. This is what your Hermes doc is pushing for.
5. **Files as separated epistemic categories.** At the top, you stop letting evidence, claims, decisions, hypotheses, signals, and rejections live in the same file. Each kind of cognition gets its own structure with its own lifecycle. For Solana adversarial work this is not optional — collapsing categories is how you get "Wallet A made 600 SOL" silently turning into "Wallet A is smart money" turning into "we should copy Wallet A." Different claims, different verification, different consequences.

ICM lives at rung 3. Your Hermes work needs rungs 4 and 5.

### 3.3 What's actually load-bearing in ICM (and what isn't)

| Load-bearing | Decorative |
|---|---|
| The Layer 3 (constraints) vs Layer 4 (input) split | Numbered folder names |
| Each stage loads only what it needs | Markdown specifically (could be JSON, YAML) |
| Every intermediate artifact is a file a human can edit | The "five layers" framing (could be three or seven) |
| Stage contracts (inputs, process, outputs) are explicit | The CLAUDE.md filename specifically |
| Sequential, with human review between stages | Local Python scripts for non-AI work |

If you only keep the load-bearing column, you have the methodology. The rest is taste.

### 3.4 The honest critique

**What ICM gets right that few people are saying out loud:** the binding constraint on long-horizon LLM work is not model intelligence, it's *attention dilution from over-stuffed context*. ICM is the cleanest, simplest, most non-engineer-accessible response to that constraint that I've seen.

**What ICM under-states:** files alone don't make agents smart — they make agents' work *inspectable*. Bad agents plus persistent files produce *durable garbage*. The agent writes confident nonsense to disk; the next agent reads it as truth; you compound hallucination. ICM doesn't address this. It needs to be paired with an eval discipline (acceptance tests per stage, contradiction logs, provenance on every claim). Your `files_grow_on_trees.txt` document already says this explicitly — and it is right.

**What ICM is not, despite the marketing:** a peer-reviewed scientific result. It's a well-argued preprint. The 52-person community testimonials are not an experiment. Treat the methodology as a credible engineering pattern, not as research consensus.

---

## Part 4 — How this connects to your actual work

You're building two things: **Hermes Solana Edge** and a **local-business lead-gen agency**. ICM connects to both, but differently.

### 4.1 Hermes Solana Edge — ICM as substrate, not architecture

Your canonical doc already has the right instincts. Look at what you wrote:

> "The 'canonical object' is no longer just a signal. It is a trade_card backed by evidence, replay metadata, anti-alpha checks, liquidity proof, and a deterministic decision id."

That sentence is *already* doing rung-5 thinking — separating evidence from claim from decision. ICM's layered loading is how each Hermes agent should *receive* its slice of that world without drowning. The mapping:

| ICM Layer | Hermes interpretation |
|---|---|
| 0 — Identity | `hermes_identity.md` — "I am Hermes. I rank signals from adversarial markets. I do not execute. I escalate." |
| 1 — Routing | Which sub-agent gets called for which event class (wallet anomaly → cluster agent; KOL burst → social validator; liquidity move → execution drafter) |
| 2 — Stage Contract | The typed contract for each agent (evidence required, anti-alpha checks that must pass, output schema for a trade_card or reject_card) |
| 3 — Reference Material (the factory) | Governance policy, allowlists, anti-alpha doctrine, slippage thresholds, agent trust scores, prior decisions log |
| 4 — Working Artifacts (the product) | This run's normalized event stream, this candidate's evidence bundle, this trade_card draft |

**Where ICM breaks down for Hermes (and what to add):**

- ICM assumes *sequential* and *human-reviewed*. Hermes is *concurrent* and *partially autonomous*. So your event bus + agent council stays — ICM lives *inside each agent*, governing how that agent loads its slice. It does not replace your orchestration.
- ICM has no eval discipline. Your Hermes doc's `agent_observation` and `trust_new = α·obs + (1-α)·trust_prev` formula is exactly the missing layer. Keep it. ICM is silent on this.
- ICM has no policy/governance enforcement. Your `block below 0.35, recover only above 0.45` hysteresis is policy-as-code. ICM doesn't have it. Keep yours.
- ICM has no append-only memory or provenance lineage. Your "append-only and provenance-heavy from day one" rule is non-negotiable for adversarial markets where in-place updates create silent corruption. ICM doesn't address this. Keep yours.

**So the real Hermes architecture is:** event bus + typed agent council + append-only memory + eval/trust loop + policy-as-code — *with each agent's internal cognition organized in ICM-style layered context*. ICM is the cognition substrate. Your existing doc is the operating system.

### 4.2 Lead-gen agency — ICM as the product template

This is where ICM fits *almost natively*. Local-business audits are exactly the kind of work ICM is best at: sequential, human-reviewed at the end, repeatable, non-developer-editable.

A client workspace per business:

```
clients/acme-roofing/
  CONTEXT.md                              # Layer 1: routing for this client
  _config/
    business_profile.md                   # Layer 3: factory
    offer.md
    competitor_set.md
  stages/
    01-leak-audit/
      CONTEXT.md                          # Layer 2: stage contract
      references/missed_calls_rubric.md   # Layer 3
      output/findings.md                  # Layer 4
    02-evidence/
      CONTEXT.md
      references/
      output/screenshots/, comparisons/
    03-opportunities/
      CONTEXT.md
      references/
      output/quick_wins.md, high_roi.md
    04-outreach/
      CONTEXT.md
      references/voice.md, objection_responses.md
      output/personalized_email.md, loom_script.md
    05-delivery/
    06-results/
```

Each client is a copyable workspace. Each stage is editable by you, not just by a developer. You can hand a non-technical operator the folder and they can run the pipeline. *That's the ICM dream.*

The thing that makes this a business and not just a folder template is the **stage contract specificity** — you have to write the per-stage Layer-2 CONTEXT.md files so well that a fresh AI in stage 3 produces consistent output without you re-explaining. That is your edge. Anyone can copy folder names; almost nobody writes good stage contracts.

### 4.3 The single biggest lift you can do this week

Stop putting "everything I know" in one mega-system-prompt. Pick one workflow you actually run repeatedly (Hermes signal triage, or one client audit), and split its prompt into:

- one `identity.md` (~300 tokens, never changes),
- one `routing.md` (which stage handles what, never changes),
- one `stage-contract.md` per stage (inputs, process, outputs),
- a `_config/` folder with your voice, constraints, doctrine,
- a per-run `working/` folder.

Run it. Measure: does the model make fewer mistakes? Are intermediate outputs editable? Can you hand a stage to ChatGPT, the next to Claude, the next to Codex, without rewriting? That portability test *is* the value test of ICM. If it passes, you've internalized the lesson and you don't need the course.

---

## Part 5 — Unknown unknowns (things adjacent to this that you didn't ask about)

You explicitly asked for these. Here is what is sitting right next to ICM that you haven't named but should know about:

### 5.1 The AGENTS.md convention (this is bigger than ICM)
A cross-tool convention — adopted by **OpenAI Codex**, **Cursor**, **Claude Code**, and increasingly others — where a project's root `AGENTS.md` file (and/or `CLAUDE.md`) tells any AI coding agent what the project is, how to build, test, lint, commit, and what conventions matter. ICM's CLAUDE.md is one instance of this. The convention is more important than ICM specifically because it's becoming the *interoperable* standard. Learn this; everything else builds on it. (See `agents.md`.)

### 5.2 Claude Skills / SKILL.md (this is what Viktor uses)
Anthropic shipped a "Skills" system where reusable knowledge lives in `skills/{name}/SKILL.md` files with YAML frontmatter describing when to use them. Skills are *progressively disclosed*: their short descriptions are always loaded, full bodies only when needed. This is exactly the ICM Layer-3 idea generalized into a marketplace. I (Viktor) literally use this — my "memory" is skill files. Your Hermes "Skills" folder should follow this pattern; it's a more mature version of ICM's reference material.

### 5.3 Spec-first development / GitHub Spec Kit
A complementary methodology: write the *specification* before the code, and let agents implement against the spec. Spec Kit (from GitHub) is one packaging. The Hermes doc you wrote is already a spec — that's why it works. ICM and spec-first compose well: spec defines *what*, ICM organizes *how the agent reads context to do it*.

### 5.4 "Lost in the middle" (Liu et al., 2023, arXiv:2307.03172)
The empirical paper underneath ICM's token math. LLMs systematically *under-attend to information in the middle of long contexts*. This is why every "just paste everything in" workflow degrades on long inputs. Worth reading the abstract. It's the experimental anchor that makes ICM more than a vibe.

### 5.5 ACE — "Context as Evolving Playbook" (2025)
A frontier paper that says: don't treat context as a static prompt; treat it as an artifact that *grows and gets curated* over time, like a playbook. This is the next step beyond ICM — your Layer 3 reference material isn't fixed, it improves run over run as you accumulate doctrine. For Hermes this matters: your anti-alpha doctrine should evolve as you see new attacks.

### 5.6 Jesse Vincent's *Superpowers* + Simon Willison's parallel agents
These are the production-grade harnesses that go *beyond* ICM into multi-agent and worktree-isolated work. Vincent's Superpowers (github.com/obra/superpowers) gives Claude Code skills, subagent dispatch, and worktree isolation. Willison runs multiple Claude/Codex agents in parallel directories and merges. For Hermes you'll likely need worktrees: isolated sandboxes per investigation, parallelized, merged via reviewer pass. ICM doesn't cover this. Superpowers does.

### 5.7 InfiAgent (2026) and the "file-centric state" research line
Academic confirmation of what practitioners stumbled into: long-horizon agents fail because of context growth + accumulated errors. The fix is *file-centric state* — workspace snapshots + bounded context reconstructed from those snapshots. This is ICM's deeper validation: not "folders are tidy" but "files are how cognition persists across context resets."

### 5.8 The durable-garbage problem (this is the one most people miss)
A filesystem-backed agent that has *no eval discipline* will write confidently-wrong information to disk, future agents will read it as truth, and you'll compound hallucination across runs. The advanced move is not "write everything down" — it's **"write the right things in the right categories with confidence tags and verification status."** Every Hermes claim should carry: source, timestamp, evidence, inference, confidence, contradiction status, decision impact, next verification step. Without this, ICM-backed Hermes becomes a hallucination landfill in three weeks.

### 5.9 Memory-poisoning attacks on long-running agents (2026 security research)
Persistent agents can be attacked through their memory, skills, scheduled jobs, or file patches. If an attacker can write to a file the agent will later read as Layer 3, they can change its behavior. For Hermes this is real — Solana KOLs and adversarial wallets actively try to manipulate signal sources. Treat retrieved content as untrusted; treat system instructions as trusted; never let the two channels merge. Provenance every external skill.

### 5.10 The deep critique you should hold in mind
A controlled METR study found that experienced open-source developers were **19% slower** with early-2025 AI tools in familiar codebases, despite expecting to be faster. The frontier is brittle even when capable. The right operating mode is *not* "maximize autonomy." It is *"maximize reliable throughput under governance."* You already wrote this in your deep research report. Hold the line. Your edge is not autonomy; it is *governed autonomy with replayable evidence.*

### 5.11 The Tier 3 question
From the harness prompting kit you uploaded: as AI handles more execution, *evaluation* becomes the scarce skill. You should map your own work into Tier 1 (machine-checkable), Tier 2 (expert-checkable in 15 min), Tier 3 (genuinely judgment-dependent). For Hermes, almost all of trade *execution* is Tier 1–2 once gates exist. The genuinely Tier 3 work is: deciding *what counts as edge*, *when to retire a signal family*, *what to abstain on*. Invest your hours there. ICM and harnesses handle the rest.

### 5.12 Cognitive architectures (the 40-year-old missing context)
Cognitive scientists have been formalizing what working memory and long-term memory should look like since the 1970s — SOAR, ACT-R, the broader cognitive-architectures literature. They distinguish *procedural* knowledge (how to do), *declarative* (what is true), *episodic* (what happened), *working* (what's active now). ICM's layered system is a folk version of this. If you want to go deep, read **John Anderson's ACT-R papers** or the recent **"Cognitive Architectures for Language Agents"** (CoALA, 2023, arXiv:2309.02427). It will reframe ICM as one specific instance of a much older idea and give you a vocabulary that scales further.

### 5.13 The thing you're circling but haven't named
You said "I'm becoming almost a specialist in delegating and orchestrating agents." That's true. The name for that role is **agent harness designer** or **AI systems orchestrator**. It is a real, emerging, valuable role — and you don't need to be a developer to be excellent at it. The unique skill is *epistemic engineering*: designing the artifacts, contracts, and verification rules that let unreliable cognition produce reliable work. Most developers are *worse* at this than systems-thinking non-developers, because developers reach for code first. You reach for structure. That's the edge. Lean into it.

---

## Part 6 — What I'd actually do this week

1. **Don't buy a course.** You already have the concept. The arXiv paper + the GitHub repo are free and contain the entire methodology.
2. **Stand up one ICM-style workspace for your highest-frequency workflow** (probably a client audit or a Hermes signal triage). Measure portability across ChatGPT, Claude, and Codex.
3. **Add the missing layers ICM doesn't have:** an `/evals` folder with acceptance tests per stage; an `/evidence` vs `/claims` vs `/decisions` separation for any work involving real-world stakes; a `provenance.md` log for any external content you pull in.
4. **Adopt AGENTS.md as the cross-tool entry point.** That gives you portability beyond ICM.
5. **Read three papers, in order:** Liu et al. *Lost in the Middle* (arXiv:2307.03172) for the empirical foundation; the ICM paper (arXiv:2603.16021) for the pattern; *Cognitive Architectures for Language Agents* (arXiv:2309.02427) for the deeper framing.

That's the path. ICM is real, useful, and narrower than its hype. The bigger thing it points at — *files as the durable substrate for AI cognition* — is genuinely one of the bridges from "AI chat" to "AI labor." You're closer to it than you think.

---

## Sources cited (all primary)

- Van Clief, J., & McDermott, D. (2026). *Interpretable Context Methodology: Folder Structure as Agent Architecture.* arXiv:2603.16021. https://arxiv.org/abs/2603.16021
- Reference implementation: github.com/RinDig/Interpretable-Context-Methodology-ICM- (MIT-licensed)
- LLM Wiki summary: blog.imfsoftware.com/llm-wiki/docs/sources/icm-folder-structure/
- Liu, N. et al. (2023). *Lost in the Middle: How Language Models Use Long Contexts.* arXiv:2307.03172.
- AGENTS.md convention: agents.md
- Jesse Vincent, *Superpowers*: github.com/obra/superpowers
- Sumers et al. (2023). *Cognitive Architectures for Language Agents (CoALA).* arXiv:2309.02427.
- Your uploaded `files_grow_on_trees.txt` (the "Files grow on trees" essay)
- Your uploaded `deep-research-report 3.md` (Frontier Long Horizon Prompting and Harness Engineering)
- Your uploaded `Hermes_Solana_Edge_Canonical_Build_Spec_v1.docx`
