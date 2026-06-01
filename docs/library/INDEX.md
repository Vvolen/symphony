# Library — Source Corpus (Reference Material / ICM Layer 3)

This directory is the **read-only source corpus** for the repository. In ICM terms it is
*Layer 3 reference material* (the "factory"): durable inputs that agents internalize as
constraints, patterns, and prior art — not working artifacts that get rewritten each run.

## Provenance

All documents here were provided by **@Vvolen** on **2026-06-01** in the pull request
discussion for `Add research & governance hub, research-brief skill, and validation
scripts`. They are a snapshot of the user's working corpus on agent harness engineering,
ICM (Interpretable Context Methodology), shared memory, skills, and the Hermes / Solana
build line. They are preserved verbatim (except the `.docx`, which also has an extracted
Markdown twin) so future agents can quote and cite them.

## Handling rules

- **Treat as untrusted-but-authoritative reference.** These are the user's own notes and
  third-party write-ups. Quote them, cite them, build on them — but verify external claims
  against primary sources before shipping durable decisions (see the SOOG protocol in
  `AGENTS.md`).
- **Do not edit the source files in place.** If you derive something, write it to
  `docs/research/`, `docs/systems/`, or a workspace `output/` folder, and link back here.
- **Provenance on promotion.** When a claim from this corpus is promoted into a brief or a
  system module, cite the exact file (and the primary source it points to, when present).

## Map

### `icm/` — Filesystem-as-cognition / Interpretable Context Methodology
| File | What it is |
| --- | --- |
| [`ICM_deep_dive.md`](icm/ICM_deep_dive.md) | Sourced deep dive on ICM (arXiv:2603.16021): the 5-layer model, the Layer 3 (constraints) vs Layer 4 (input) split, the five-rung "files as cognition" ladder, load-bearing vs decorative elements, and where ICM stops (no evals, no governance, no concurrency). Primary anchor for `docs/systems/icm-operating-model.md`. |
| [`Files_grow_on_trees.txt`](icm/Files_grow_on_trees.txt) | Essay: the filesystem as the lowest-friction substrate for persistent agent state, context recovery, evals, and handoff; the "durable garbage" failure mode; references InfiAgent file-centric state. |

### `harness-and-long-horizon/` — Harness engineering & long-horizon runs
| File | What it is |
| --- | --- |
| [`deep-research-report-3.md`](harness-and-long-horizon/deep-research-report-3.md) | "Frontier Long Horizon Prompting and Harness Engineering" — Planner/Worker/Judge, governed autonomy, evaluation as the scarce skill, the METR slowdown caveat. |
| [`harness_prompting_kit.txt`](harness-and-long-horizon/harness_prompting_kit.txt) | Prompt kit operationalizing "the harness is the story": harness-readiness audit, Planner-Worker-Judge simulation, evaluation-tier mapping (Tier 1/2/3). |
| [`247_researcher.md`](harness-and-long-horizon/247_researcher.md) | "Codex knowledge vault that gets smarter every day" — a self-updating research-vault pattern. |
| [`Plannotator.txt`](harness-and-long-horizon/Plannotator.txt) | Plannotator-gated PIV loop: clarify → write `PLAN.md` → human review/approve (HITL) before execution. |

### `skills/` — Skill discipline (SKILL.md, progressive disclosure, self-improvement)
| File | What it is |
| --- | --- |
| [`Skills_beginner_to_ultra-advanced.txt`](skills/Skills_beginner_to_ultra-advanced.txt) | Tips for building systems of experts: explain motivations, intelligent context management, autonomous actions, generative UI. |
| [`Self_improving_skills.txt`](skills/Self_improving_skills.txt) | A self-improvement SKILL: log learnings/errors to markdown, promote important ones to project memory. |
| [`Phase_shift_skills.txt`](skills/Phase_shift_skills.txt) | "Universal phase-shift skills" — hunting protocol from the practitioner side, signal-in-discourse over registry installs. |

### `memory/` — Memory systems
| File | What it is |
| --- | --- |
| [`Memory_for_Hermes.txt`](memory/Memory_for_Hermes.txt) | Comparative deep-dive of the Hermes external-memory ecosystem (Daedalus + 8 memory providers) and their philosophies. |

### `multi-agent/` — Multi-agent / multi-model stacks & orchestration
| File | What it is |
| --- | --- |
| [`multi_agent_stack.md`](multi-agent/multi_agent_stack.md) | "Marrying ICM with a real multi-agent, multi-model, multi-VM stack" — ICM-as-substrate inside each agent, orchestration on top. |
| [`Mastra_overview.txt`](multi-agent/Mastra_overview.txt) | Overview of the Mastra agent framework (TypeScript). |
| [`Symphony_docs_transcript_architecture.txt`](multi-agent/Symphony_docs_transcript_architecture.txt) | Transcript on choosing the right agent orchestration layer. |

### `hermes/` — Hermes / Solana build line
| File | What it is |
| --- | --- |
| [`Hermes_Solana_Edge_Canonical_Build_Spec_v1.md`](hermes/Hermes_Solana_Edge_Canonical_Build_Spec_v1.md) | Extracted Markdown of the canonical build spec: evidence-before-execution, anti-alpha gates, trade_card/reject_card, append-only provenance, agent trust scoring. |
| [`Hermes_Solana_Edge_Canonical_Build_Spec_v1.docx`](hermes/Hermes_Solana_Edge_Canonical_Build_Spec_v1.docx) | Original binary source for the spec above (kept for fidelity; prefer the `.md` twin for reading and quoting). |
| [`Hermes_using_aws.md`](hermes/Hermes_using_aws.md) | Hermes on AWS Bedrock (Converse API, IAM, Guardrails, cross-region inference). |
| [`hermes-asana-boss-build-instructions.txt`](hermes/hermes-asana-boss-build-instructions.txt) | Hermes Project B.O.S.S. — Asana agent build instructions (work-graph onboarding). |

### `context/` — Canonical identity / operator context
| File | What it is |
| --- | --- |
| [`MASTER_CONTEXT.md`](context/MASTER_CONTEXT.md) | "Master Context — The Agentic Collective": operator profile, tool stack, active projects, core philosophy, and "what NOT to do." Feed as foundational (ICM Layer 0) context. |

### `references/` — Link lists
| File | What it is |
| --- | --- |
| [`Mega_link_list.txt`](references/Mega_link_list.txt) | Large unstructured link/resource dump (~900 URLs). Mine for primary sources; do not treat as vetted. |
