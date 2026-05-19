---
name: research-brief
description: Produce source-grounded research briefs, landscape scans, tool evaluations, architecture recommendations, and executive summaries. Use when the user asks for serious research, frontier practice, current tooling, comparisons, governance, strategy, or claims that need citations and an evidence trail.
---

# Research Brief

Use this skill to turn open-ended research into a durable, source-grounded artifact.

## Workflow

1. Define the question, audience, decision needed, and freshness window.
2. Gather current primary sources first; add high-signal secondary sources only when useful.
3. Extract claim-level evidence with URLs, dates, and confidence.
4. Separate sourced fact, inference, recommendation, and speculation.
5. Produce an executive summary first, then the detailed evidence trail.
6. Record risks, unknowns, and concrete next actions.
7. Save durable research under `docs/research/` when the findings should persist.

## Source quality ladder

Prefer sources in this order:

1. Primary docs, release notes, source repositories, specs, papers, regulatory filings, or official announcements.
2. Maintainer posts, issue discussions, engineering blogs, and vendor docs with direct implementation detail.
3. Community reports, videos, Reddit/X/forum posts, and summaries.
4. Aggregators and AI-generated articles only as discovery leads, not final authority.

For OpenAI product behavior, use official OpenAI documentation or OpenAI repositories whenever possible.

## Output shape

Use `references/research-brief-template.md` for substantial work. At minimum include:

- executive summary;
- sources consulted;
- claims/evidence table;
- analysis and recommendation;
- risks and unknowns;
- next actions.

## Guardrails

- Do not present a claim as settled if the sources disagree or are weak.
- Do not use stale sources for fast-moving AI tooling unless you explain why they still matter.
- Do not include secrets in research artifacts.
- For financial, trading, legal, security, or medical topics, raise the confidence bar and label limitations clearly.
