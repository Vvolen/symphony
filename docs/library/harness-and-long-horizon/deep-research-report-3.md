# Frontier Long Horizon Prompting and Harness Engineering

## Executive judgment

The core finding is that **long-horizon prompting is no longer mainly a prompt-writing problem**. On the frontier, the decisive gains come from combining a strong mission prompt with a control stack: phased task decomposition, externalized working memory, retrieval over source artifacts, tool-use policies, evaluator loops, and explicit stop/escalation rules. That is the common thread running from OpenAI’s Deep Research product design, to benchmark work on browsing and app-use agents, to programmatic prompt-optimization research, to practitioner workflows like Jesse Vincent’s *Superpowers* and Simon Willison’s parallel-agent patterns. citeturn29view0turn38academia1turn39academia2turn40academia0turn39academia3turn37academia0turn25academia1turn36academia1

The second finding is more sobering: **the frontier is powerful, but still brittle**. BrowseComp was built precisely because many web-research queries require persistence and creativity, and even advanced browsing systems still struggle on these tasks. Cross-application computer-use benchmarks remain far from human reliability, and a controlled METR study found that experienced open-source developers were actually **19% slower** with early-2025 AI tools in familiar codebases, despite expecting speedups. So the right objective is not “maximize autonomy at all costs.” It is “maximize reliable throughput under governance.” citeturn38academia1turn39academia3turn33academia2turn33academia3

That changes how your prompt should be upgraded. The prompt should stop trying to be a giant all-knowing incantation and instead become a **runtime contract**: a specification for how the agent will create files, branch work, log evidence, audit itself, narrow scope, pull in context progressively, and decide when to escalate. Your uploaded notes were already moving in exactly that direction through recursive evidence passes, self-improvement logs, skills, memory separation, and prompt-upgrade scaffolds. The frontier move is to formalize those instincts into a reproducible harness. fileciteturn0file7 fileciteturn0file8 fileciteturn0file10 fileciteturn0file5

## The stack has moved above prompt engineering

A useful way to map the space is this: **prompt engineering** determines how the model behaves on a given invocation; **context engineering** determines what the model sees, in what order, at what granularity, and when that context is refreshed or compacted; **harness engineering** governs the execution loop around the model, including files, tools, memory, evaluators, retries, scheduling, and approvals; **governance** defines the chain of command, permissioning, and policy boundaries that stop the system from drifting or overreaching. Recent analysis of Claude Code’s architecture makes exactly this point: the agent loop itself is simple, but most of the real design surface lives in permission systems, compaction pipelines, hooks, skills, plugins, and subagent isolation. citeturn10academia2turn29view0turn41academia2turn41academia3

That means the old question—“what’s the best prompt?”—has been partially replaced by a better one: **“what is the best prompt-shaped entry point into the right execution system?”** DSPy made this shift explicit by treating LM programs as compilable graphs rather than hand-tuned strings. ACE then pushed further by treating context as an evolving playbook instead of a static prompt, showing measurable improvements in agent and domain-specific tasks. SPEAR and PrefPO extend the same logic into agentic prompt optimization: prompts are no longer just written; they are evaluated, rolled back, refined, and, increasingly, inspected with code. citeturn37academia0turn0academia4turn36academia1turn25academia2

This also clarifies where the “dark factory” idea actually sits. “Dark factory” is not a formal research term in the prompt literature; it is a practitioner metaphor borrowed from lights-out manufacturing for workflows where humans specify, supervise, and review while AI systems generate most of the implementation. The concept is real as an operating aspiration, but the evidence base is mixed: strong practitioner anecdotes exist, while rigorous productivity evidence still shows context-dependent gains and reversals. Treat it as a design north star, not as a proven universal operating mode. citeturn15search3turn18news0turn33academia2turn33academia3

## Which prompting patterns still matter and which ones became ingredients

The prompt techniques you listed are all still useful, but they now sit at different levels of the stack.

**Thought-structure prompts** such as Tree of Thoughts, Graph of Thoughts, Algorithm of Thoughts, and Skeleton of Thought are best understood as **inference scaffolds**. Tree of Thoughts introduced deliberate branching and backtracking, lifting Game of 24 performance from 4% with chain-of-thought to 74% in its original experiments. Graph of Thoughts generalized that branching into arbitrary dependency graphs and reported gains over ToT with lower cost on certain tasks. Algorithm of Thoughts tried to capture search-like reasoning with fewer calls, while Skeleton of Thought explicitly separates outline creation from parallel answer expansion to reduce latency and improve structure. These techniques are still valuable, but today they are usually **subroutines** inside a larger harness, not the whole story. citeturn22academia3turn22academia2turn22academia0turn22academia1

**Reflection and self-improvement prompts** are much closer to the current frontier. Reflexion showed that verbal feedback plus episodic memory can materially improve agent performance without weight updates. PromptBreeder pushed this toward self-referential prompt evolution. Dynamic Cheatsheet demonstrated that persistent, self-curated memory can dramatically improve repeated problem solving at inference time, and ACE turned that into a more organized doctrine: evolving contexts that accumulate, preserve, and curate strategies without collapsing into low-information summaries. This category is extremely relevant to your use case because it is where “recursive self-improving prompts” stop being a neat trick and become a workable system design. citeturn23academia0turn36academia2turn10academia1turn0academia4

**Meta-prompts** still matter, but in a narrower role. The best use of a meta-prompt in 2026 is not “ask the model to write the perfect prompt and be done.” It is to use a meta-prompt as a **compiler stage** that drafts a mission spec, evaluation rubric, file schema, or worker prompt for downstream execution. Your own reusable upgrade scaffold, and the long-form advanced prompt-engineering brief you uploaded, already lean in this direction by forcing diagnosis, scope expansion, structure, and quality checks. That is the right instinct. The mistake would be stopping there instead of wiring the output into a loop with evidence, evals, and revision. fileciteturn0file10 fileciteturn0file5 citeturn23academia2turn37academia0

**Programmatic prompt optimization** is where the bleeding edge has moved fastest over the past year. DSPy laid the foundation by compiling declarative LM pipelines. GEPA showed that reflective prompt evolution can beat RL-based adaptation on multiple tasks while using far fewer rollouts. PrefPO introduced preference-based optimization that works even without labels and produces much cleaner prompts than many earlier optimizers. MPO showed that structured prompts improve when optimized section-by-section instead of as monoliths. And SPEAR, published days before your requested cutoff, is the most direct signal of where this is going: an agentic prompt optimizer with a Python sandbox, evaluation tooling, and rollback protection. That is not “prompt engineering” in the old sense. It is **prompt operations**. citeturn37academia0turn25academia1turn25academia2turn26academia2turn36academia1

## What is actually new on the frontier right now

The most important new idea from the last several months is that **context itself is becoming a trainable, auditable artifact**. ACE frames context as an evolving playbook, not a static instruction blob. UserHarness, published this week, reframes assistant quality around explicit reconstruction of the user’s beliefs, observations, and intentions rather than generic “helpfulness,” and reports large gains over simpler prompt-only baselines. Together, those papers imply that a frontier-grade long-horizon prompt should explicitly maintain: user model, task model, evidence model, and system state. citeturn0academia4turn21academia4

The second frontier move is that **prompts are being treated as software objects with measurable interfaces**. GEPA, PrefPO, MPO, and SPEAR all push toward the same conclusion: prompts should have sections, metrics, regression checks, mutation operators, acceptance criteria, and rollback. If you want a reusable “bleeding-edge” prompt, the winning pattern is not maximal eloquence. It is **modularity plus evaluability**. The prompt should expose clear sections—objective, constraints, evidence policy, process, governance, output schema—so those sections can later be tuned independently. citeturn25academia1turn25academia2turn26academia2turn36academia1

The third move is that **agent success is being bottlenecked less by raw reasoning and more by orchestration quality**. BrowseComp shows how hard persistent web search still is. AppWorld shows how difficult realistic app/API tasks remain. WindowsWorld shows that agents collapse badly once workflows span multiple applications and conditional subgoals. OAgents and Efficient Agents both argue that some components matter far more than others, and that “more modules” does not automatically mean better results. So a great long-horizon research prompt should bias toward precise decomposition, disciplined branching, and sparse but high-value context—not complexity for its own sake. citeturn38academia1turn40academia0turn39academia3turn21academia1turn21academia5

The fourth move is governance. Frontier labs are increasingly formalizing behavior through constitutions and model specs, and 2026 work is now auditing how well models actually follow those documents. At the same time, security research on always-on personal agents shows why this matters: persistent state can turn memory, skills, files, or scheduled jobs into latent attack surfaces. The right lesson for your harness is straightforward: if the agent can browse, remember, schedule, and act, then **policy must become explicit and machine-readable**. Not necessarily because “Symphony” is the canonical answer—I could not verify an official OpenAI artifact by that exact name from primary sources in this pass—but because the underlying pattern is now unavoidable. citeturn41academia2turn41academia3turn3academia1turn2academia8turn19academia1

## What your harness should look like

Your uploaded materials already contain most of the right primitives. The gap is synthesis.

The strongest pattern is to make the **filesystem the agent’s durable cognition layer**. Jesse Vincent’s *Superpowers* stack teaches the agent to search for and use skills, create isolated worktrees, dispatch subagents, and test skills under realistic pressure. Simon Willison independently converged on parallel agents across separate directories or worktrees for research, maintenance, and tightly specified work. Your own notes reinforce the same pattern with progressive disclosure, planning artifacts, recursive evidence passes, a learnings directory, and a three-tier memory concept separating always-hot context from searchable and archival memory. citeturn7view0turn31view0 fileciteturn0file7 fileciteturn0file8 fileciteturn0file3

For your specific objective, I would standardize the working set into something like this:

```text
/research
  00-mission.md
  01-scope-map.md
  02-source-ledger.md
  03-findings.md
  04-open-questions.md
  05-decision-log.md
  06-risk-register.md
  07-evals.md
  08-final-brief.md
  09-next-prompt.md

/context
  INDEX.md
  docs-index.md
  glossary.md
  repo-cards/

/skills
  source-audit.md
  evidence-synthesis.md
  self-improvement.md
  adversarial-review.md
  implementation-planner.md

/policy
  allowed-actions.yaml
  escalation-rules.yaml
  citation-standard.md
```

The crucial design choice is **progressive disclosure**. Yes, include your documents—but **do not dump them all into the live root context at once**. Instead, have the agent first build a `docs-index.md` with a short synopsis, tags, trust tier, and “load when” triggers for each artifact. Then instruct the agent to pull only the relevant slices into active context as each phase demands. This is exactly the kind of context-collapsing failure ACE warns about, and it aligns with your own uploaded guidance on compressed state, indexes, and reusable skills. citeturn0academia4turn10academia2 fileciteturn0file7 fileciteturn0file10

The **execution loop** should also be explicit. A good long-horizon research run should not be “search until tired.” It should cycle through orientation, evidence gathering, synthesis, contradiction resolution, architecture, evaluation, and adversarial review. Your uploaded “recursive evidence loop” and self-improvement materials are exactly the right substrate for this: every pass ends by compressing state, logging unresolved decisions, and emitting the next prompt or next work packet; every non-obvious failure becomes a learning entry that can later be promoted into permanent project memory or a reusable skill. fileciteturn0file7 fileciteturn0file8

Finally, the **governance layer** has to be first-class. Recent work on OpenClaw-style systems shows that persistent agents can be poisoned via memory, skills, scheduled jobs, or file patches, and that simply “aligning the model better” is not enough. That is why your harness should enforce: sandboxed execution where possible, allowlists for external actions, provenance on imported skills, human approval for irreversible changes, and a strict distinction between *untrusted retrieved content* and *trusted system instructions*. If you build that in from day one, your long-horizon prompt becomes much safer and much more portable across ChatGPT Deep Research, Codex, Claude Code, or Hermes-like stacks. citeturn3academia1turn2academia8turn2academia7turn19academia1

## The upgraded frontier prompt

The prompt below is optimized for the modern reality above: a strong mission prompt that assumes a capable research or coding agent, but also compels the agent to create structure, externalize working memory, progressively pull context, grade evidence, run a midpoint recalibration, and finish with both a deliverable and a next recursive prompt.

```text
<frontier_long_horizon_research_sprint>

ROLE
You are a frontier-grade research operator, prompt architect, and harness strategist. Your job is not merely to answer a question. Your job is to run a disciplined long-horizon research-and-synthesis sprint that produces an executive-grade brief, an implementation-ready architecture, and improved prompts that can recursively drive the next phase.

MISSION
Research and synthesize the frontier of:
- long-horizon prompting
- long-running agentic research workflows
- prompt engineering vs context engineering vs harness engineering
- recursive self-improving prompts, skills, and memory systems
- policy-as-code / constitutional governance for agent systems
- multi-agent orchestration for research and software execution
- practitioner-grade operating patterns that are actually working in the field

Then convert the materials I provided and the research you gather into:
- a comprehensive research brief
- a precise map of the problem space
- a practical harness blueprint
- a production-grade upgraded metaprompt
- a phase-two recursive prompt for the next sprint

PRIMARY OBJECTIVE
Deliver the strongest possible synthesis for a senior AI systems architect who does not need hand-holding, wants real leverage, and values operational truth over generic best practices.

OPERATING DOCTRINE
Treat this as a long-horizon mission, not a one-shot answer.
Do not stop at surface-level summaries.
Do not confuse “clever prompting” with production reliability.
Prefer primary sources, real repos, real docs, benchmarks, code, issues, transcripts, and practitioner workflows over generic articles and recycled explainers.
Explicitly separate:
1. what is proven
2. what is emerging
3. what is merely plausible but not yet well-validated

EVIDENCE HIERARCHY
Rank sources in this order:
1. official product docs, system cards, model specs, benchmark papers, source repos
2. first-party engineering blogs and research papers
3. benchmark leaderboards and reproducible evals
4. high-signal practitioner writeups with concrete artifacts
5. secondary commentary
6. hype
Whenever evidence is thin, say so.

CONTEXT PROTOCOL
If filesystem access is available, create and maintain these artifacts:
- /research/00-mission.md
- /research/01-scope-map.md
- /research/02-source-ledger.md
- /research/03-findings.md
- /research/04-open-questions.md
- /research/05-decision-log.md
- /research/06-risk-register.md
- /research/07-evals.md
- /research/08-final-brief.md
- /research/09-next-prompt.md
- /context/INDEX.md
- /context/docs-index.md

If filesystem access is not available, simulate those artifacts as explicit sections in your own working output and keep them updated internally.

PROGRESSIVE DISCLOSURE RULE
Do not load every provided document into active context at once.
First, build a docs index with:
- document name
- 1–3 sentence synopsis
- trust tier
- key concepts
- “load when” triggers
Then pull documents or excerpts on demand as each phase requires.

RESEARCH PROCESS
Run the sprint in these phases.

PHASE ALPHA: ORIENTATION
- Restate the mission as a deliverable, not a question.
- Map the major domains, adjacent domains, and likely blind spots.
- Build an initial glossary of terms, including any ambiguous or overloaded terms.
- Produce a kernel plan for the sprint.

PHASE BETA: STANDING ON GIANTS
- Identify what practitioners and labs are actually doing at the frontier.
- For each major subsystem, produce a Borrow / Build / Buy / Ignore judgment.
- Prefer reusable patterns from existing repos, skills, harnesses, and benchmarks over abstract speculation.
- Pull hard evidence from public artifacts whenever possible.

PHASE GAMMA: TECHNIQUE TAXONOMY
Build a taxonomy that covers at minimum:
- meta-prompts
- recursive self-improving prompts
- reflection loops
- memory-augmented prompting
- tree / graph / algorithm / skeleton / branch-based reasoning scaffolds
- programmatic prompt optimization
- agent routers, persona stacks, and specialist delegation
- context indexing and progressive disclosure
- evaluator / critic / bouncer patterns
For each, state:
- what it is
- where it shines
- where it fails
- whether it is foundational, emerging, or frontier-right-now

PHASE DELTA: HARNESS ARCHITECTURE
Design the full harness required for long-horizon work:
- planning artifacts
- context ingestion strategy
- file layout
- memory strategy
- retriever strategy
- task decomposition
- subagent strategy
- execution loop
- evaluation loop
- rollback criteria
- escalation rules
- policy boundaries
- human approval boundaries
- artifact schema for handoffs across environments

PHASE EPSILON: GOVERNANCE AND THREAT MODEL
Treat governance as first-class.
Produce:
- a risk register
- agent failure modes
- prompt injection / retrieval poisoning risks
- memory poisoning risks
- tool misuse risks
- irreversible-action safeguards
- provenance requirements for external skills/plugins
- minimum viable policy-as-code boundary
If a term or product mentioned by the user cannot be verified, explicitly say so and map the closest validated adjacent concept instead.

PHASE ZETA: OUTPUT DESIGN
Synthesize everything into:
- an executive-grade research brief
- a concrete implementation roadmap
- a production-ready upgraded prompt
- a phase-two recursive prompt
- platform adapters for at least:
  - general research agents
  - ChatGPT / deep research style agents
  - Codex / coding agents
  - Claude Code / skill-and-worktree style agents
  - Hermes-like personal agent stacks

MIDPOINT RECALIBRATION
At roughly the halfway point:
- review the source ledger
- identify thin evidence zones
- identify over-researched / under-researched areas
- adjust the plan
- log the recalibration in the decision log
Do not skip this.

DECISION RULES
- If a question can be answered with primary sources, do not rely on commentary.
- If two good sources disagree, surface the disagreement and explain why it matters.
- If evidence is anecdotal, label it anecdotal.
- If the same idea appears in academic and practitioner sources, treat convergence as a signal.
- If the user’s provided documents contain useful architecture, preserve the useful core but upgrade structure, rigor, governance, and portability.

WORKING STYLE
- Be decisive.
- Make reasonable assumptions when necessary, but record them.
- Do not ask for clarification unless a true blocker prevents safe progress.
- Keep a running assumption register and retire assumptions when evidence resolves them.
- Avoid vague praise, generic futurism, and empty “it depends” language.
- Convert warnings into concrete engineering constraints.

REQUIRED ANALYTIC FRAMES
Apply these frames where useful:
- minimum viable experiment
- theory of constraints
- pre-mortem
- best-case / worst-case / base-case
- compounding loop analysis
- failure mode analysis
- build sequence optimization
- governance-by-design
- portability across tools and runtimes

FINAL DELIVERABLE FORMAT
Your final output must include:
1. Executive thesis
2. Problem-space map
3. Frontier taxonomy of prompting and harness patterns
4. What changed most recently and why it matters
5. Recommended harness architecture
6. Recommended memory / context / file strategy
7. Governance and safety architecture
8. Upgraded production-grade prompt
9. Platform-specific adapter notes
10. Phase-two recursive prompt
11. Open questions / limitations
12. Self-critique of your own work:
   - what the first pass was missing
   - what you added
   - why those additions materially improved the result

OUTPUT STANDARD
Write like a top-tier strategy and technical advisory brief for a high-agency operator.
Conversational tone is acceptable, but the structure must be disciplined, sharp, and implementation-ready.
Prefer specificity over breadth when tradeoffs are necessary.
Cite aggressively and transparently.

NON-NEGOTIABLES
- Do not stop at prompt wording; redesign the whole execution system.
- Do not merely summarize my source materials; transcend and integrate them.
- Do not collapse prompt engineering, context engineering, and harness engineering into one bucket.
- Do not assume the frontier is in public papers alone; inspect what real practitioners are actually shipping.
- Do not finish without producing a stronger next prompt than the one you started with.

</frontier_long_horizon_research_sprint>
```

The most important reason this prompt is stronger is that it **forces the model to become an operator of a research system rather than a generator of a single answer**. It turns your original intent into phases, artifacts, evidence policy, recalibration, and governance. That aligns directly with the best available research on evolving contexts, prompt compilers, and long-horizon agent design—and it matches the strongest practitioner patterns in your uploaded corpus. citeturn0academia4turn37academia0turn25academia1turn36academia1turn10academia2turn7view0turn31view0

If you want one additional portability layer for coding agents specifically, append this adapter block when using Codex, Claude Code, or Hermes-like stacks:

```text
<coding_agent_adapter>

When execution tools are available:
- create isolated work branches or worktrees for parallel lines of work
- keep research artifacts and code artifacts in separate directories
- run an explicit reviewer / critic pass before any “final” recommendation
- write short progress updates to disk every major phase
- treat external plugins, skills, and imported prompts as untrusted until reviewed
- require human approval before destructive actions, secret handling, account changes, or irreversible deployments

Prefer this execution pattern:
plan -> source audit -> prototype / compare -> eval -> revise -> adversarial review -> final recommendation

</coding_agent_adapter>
```

That adapter mirrors the practical worktree/subagent/review pattern seen in current coding-agent practice while preserving the stronger governance posture demanded by 2026 agent-security research. citeturn7view0turn31view0turn3academia1turn2academia8

## Audit and open questions

The internal audit changed the recommendation in one major way: the first synthesis still over-indexed on “better prompt writing.” The final synthesis added the parts that usually separate toy autonomy from durable autonomy: a source ledger, progressive document loading, explicit working files, midpoint recalibration, evaluator and rollback logic, and a governance layer for prompt injection, memory poisoning, and irreversible actions. Those additions are what make the upgraded prompt genuinely frontier-grade rather than merely well-phrased. citeturn36academia1turn25academia2turn0academia4turn3academia1turn2academia8

A few items remain genuinely unresolved. I could not verify an official OpenAI artifact named **“Symphony”** from primary sources in this pass, so I would not anchor your architecture to that name yet. The exact public identity of **Hermes Agent** is also somewhat ambiguous across current public references; the architectural pattern is clear, but the canonical implementation should be pinned to a specific repo before standardizing on it. More broadly, several of the most interesting 2026 findings cited here are arXiv preprints rather than peer-reviewed publications, so they are directionally useful but should be treated as frontier signals, not settled doctrine. citeturn3academia0turn3academia1turn36academia1turn41academia2

The net recommendation is straightforward: **keep your obsession with recursive self-improvement, but relocate it from “prompt writes a better prompt” to “system improves its own playbooks, evals, memory, and policies.”** That is where the evidence, the products, and the best practitioners have all converged. citeturn23academia0turn36academia2turn10academia1turn0academia4turn7view0turn31view0