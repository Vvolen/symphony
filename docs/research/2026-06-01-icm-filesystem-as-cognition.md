# Research Brief: ICM and the Filesystem-as-Cognition Pattern

- Date: 2026-06-01
- Owner: Copilot (GitHub Copilot coding agent), for @Vvolen
- Freshness window: sources through 2026-05; refresh ICM publication status if relied on after 2026-09
- Question: What is ICM, is it real, where does it sit among frontier filesystem-as-state practices, and how should this repo adopt its load-bearing parts?
- Decision needed: Whether to make ICM the organizing model for the repo's long-horizon workspaces, and what to add on top of it.

## Executive summary

**ICM (Interpretable Context Methodology)** replaces framework-level multi-agent orchestration
with **filesystem structure**: numbered stage folders plus plain-Markdown context files that tell a
single agent what role to play at each step. It is a **real but narrow** artifact — an arXiv
preprint (not yet peer-reviewed) with an MIT-licensed reference repo — scoped explicitly to
**sequential, human-reviewed** workflows. Its load-bearing engineering claim is the **Layer 3
(constraints / "the factory") vs Layer 4 (input / "the product") split**, plus the discipline that
**each stage loads only the ~2–8k tokens it needs**, sidestepping "lost in the middle" degradation.

ICM is one clean instance of a **broader convergence**: the filesystem as the durable substrate for
agent cognition. The same primitive shows up independently in the cross-tool **AGENTS.md**
convention, Anthropic's **Claude Skills (SKILL.md)**, and academic work (**InfiAgent** file-centric
state; **ACE** context-as-evolving-playbook; **CoALA** cognitive architectures for language agents).

**Recommendation:** adopt ICM's load-bearing parts as the repo's workspace model (see
`docs/systems/icm-operating-model.md` and `workspaces/_template-icm/`), but **add the layers ICM
omits** — per-stage evals, evidence/claim/decision separation, append-only provenance, and policy
enforcement — because this repo's north-star use cases (Hermes, multi-agent) are concurrent and
adversarial, which the ICM authors explicitly say ICM does **not** cover.

## Source register

| Source | Date | Type | Link / locator | Why it matters |
| --- | --- | --- | --- | --- |
| Van Clief, J. & McDermott, D. "Interpretable Context Methodology: Folder Structure as Agent Architecture" | ~2026-03 | arXiv preprint (not peer-reviewed; "submitted to ACM TiiS") | arXiv:2603.16021 — https://arxiv.org/abs/2603.16021 | Primary specification of ICM and the 5-layer model. |
| RinDig/Interpretable-Context-Methodology-ICM- | 2026 | Reference implementation (MIT software license, ~559★) | https://github.com/RinDig/Interpretable-Context-Methodology-ICM- | Canonical worked example; README defines Layer 3 vs Layer 4. |
| Liu, N. et al. "Lost in the Middle: How Language Models Use Long Contexts" | 2023 | Peer-reviewed-track paper | arXiv:2307.03172 — https://arxiv.org/abs/2307.03172 | Empirical anchor: LLMs under-attend to the middle of long contexts. |
| AGENTS.md convention | 2025–2026 | Cross-tool standard (Codex, Cursor, Claude Code) | https://agents.md | The interoperable entry point; ICM's `CLAUDE.md` is one instance. |
| Anthropic Claude Skills / SKILL.md | 2025–2026 | Vendor docs / pattern | https://docs.anthropic.com (Agent Skills) | Progressive disclosure of reference material = ICM Layer 3 generalized. |
| Sumers et al. "Cognitive Architectures for Language Agents (CoALA)" | 2023 | Paper | arXiv:2309.02427 — https://arxiv.org/abs/2309.02427 | Reframes ICM layers as a folk version of procedural/declarative/episodic/working memory. |
| InfiAgent (file-centric state for long-horizon agents) | 2026 | Paper (as cited in corpus) | see `docs/library/icm/Files_grow_on_trees.txt` | Academic confirmation: long-horizon agents fail from context growth + accumulated error; fix is file-centric state. |
| ACE — "Context as Evolving Playbook" | 2025 | Paper (as cited in corpus) | see `docs/library/icm/ICM_deep_dive.md` §5.5 | Layer 3 reference material should evolve/curate over runs, not stay static. |
| `docs/library/icm/ICM_deep_dive.md` | 2026-06 | User corpus (verbatim quotes of the above) | repo path | Synthesis with verbatim abstract/README quotes; basis for this brief. |
| `docs/library/icm/Files_grow_on_trees.txt` | 2026-06 | User corpus | repo path | The "durable garbage" failure mode and files-as-external-memory ladder. |

> Note on verification: the ICM paper, GitHub repo, and "Lost in the Middle" are cited with stable
> identifiers above. InfiAgent and ACE are cited **as represented in the user corpus**; treat their
> exact venue/IDs as unverified until checked against a primary index.

## Claims and evidence

| Claim | Evidence | Confidence | Notes |
| --- | --- | --- | --- |
| ICM exists and is specified, not vaporware | arXiv:2603.16021 + MIT-licensed repo with worked examples | High | "Real artifact," but a preprint. |
| ICM is **not** peer-reviewed | "Submitted to ACM TiiS" = under review, not published; arXiv = author-uploaded | High | Treat as a frontier signal, not settled doctrine. |
| The load-bearing claim is the Layer 3 vs Layer 4 split | Repo README §"How It Works": constraints internalized vs input transformed | High | Numbered folders / "five layers" / Markdown specifically are decorative. |
| Each stage should load ~2–8k focused tokens, not a 30–50k monolith | LLM-Wiki summary of ICM; grounded in Liu et al. 2307.03172 | Medium-High | Token figures are illustrative, not a benchmark. |
| ICM is explicitly **not** for concurrent / adversarial / autonomous-branching work | Paper §5 "Doesn't work" list (authors' own scope) | High | Decisive for Hermes-class systems. |
| The filesystem-as-state pattern is a multi-source convergence | AGENTS.md, Claude Skills, InfiAgent, ACE, CoALA all independent | Medium-High | ICM is the simplest, most teachable node. |
| Filesystem state without evals produces "durable garbage" | `Files_grow_on_trees.txt`; ICM_deep_dive §5.8 | High | Bad agent + persistent files = compounding hallucination. |

## Analysis

The "files-as-cognition" idea reads as obvious ("use folders") but the engineering content is
specific: **prevent** context dilution by never loading irrelevant tokens, and **separate** the
rules an agent must obey (Layer 3) from the material it must transform (Layer 4). That maps onto a
five-rung ladder (from `ICM_deep_dive.md` §3.2):

1. Files as storage → 2. Files as memory → 3. **Files as context routing (this is ICM)** →
4. Files as control plane (stage contracts, policy-as-code, eval gates) →
5. Files as separated epistemic categories (evidence ≠ claim ≠ decision ≠ hypothesis).

This repo already lives partly at rungs 4–5 (governance docs, anti-conflation rules in
`docs/governance/shared-memory-architecture.md`). ICM supplies a clean **rung-3** model the repo was
missing: a copyable, stage-structured workspace where each stage's context is bounded. The
correct move is therefore **additive**: take ICM's substrate, keep this repo's governance/eval layer
on top.

## Recommendation

1. Adopt ICM's **load-bearing** elements (Layer 3/4 split, per-stage bounded context, every output an
   editable file, explicit stage contracts) as the model for long-horizon workspaces.
2. Ship a copyable scaffold: `workspaces/_template-icm/` with `identity.md` (L0), `routing.md` (L1),
   `stages/NN-name/CONTEXT.md` (L2), `_config/` + `references/` (L3), `output/` (L4).
3. **Add what ICM omits**, because the repo's targets are concurrent/adversarial:
   - `evals/` acceptance checks per stage (machine-checkable where possible);
   - `evidence/` vs `claims/` vs `decisions/` separation for stakes-bearing work;
   - append-only `provenance` on any externally retrieved content;
   - policy-as-code gates (allowlists, thresholds) as Layer 3 constraints.
4. Keep **AGENTS.md** as the cross-tool Layer-0/1 entry point so the structure is portable across
   Codex, Cursor, and Claude Code — do not couple to a single tool's filename.

## Risks and unknowns

- **Publication status risk:** ICM may never clear peer review; don't cite it as consensus.
- **Durable-garbage risk:** without the eval layer, ICM structure accelerates hallucination
  propagation. The added `evals/` + provenance layers are non-optional mitigations.
- **Memory-poisoning risk:** anything an agent later reads as Layer 3 is an attack surface; treat
  retrieved content as untrusted and never merge it with system instructions (ICM_deep_dive §5.9).
- **Unverified citations:** InfiAgent/ACE venue + IDs not independently confirmed here.
- **Scope creep:** ICM tempts over-structuring simple tasks; apply only to genuinely long-horizon work.

## Next actions

- [x] Promote the model into a system module: `docs/systems/icm-operating-model.md`.
- [x] Ship the `workspaces/_template-icm/` scaffold with the added eval/evidence/provenance layers.
- [ ] (Codex) Validate InfiAgent/ACE primary IDs and add them to the source register.
- [ ] (Codex) Pilot one real workflow (a client audit or Hermes signal triage) through the template and measure cross-tool portability.
