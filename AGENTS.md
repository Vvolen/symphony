# Symphony Research Hub

This fork is allowed to host both the upstream Symphony implementation and a repo-local research and governance hub.

## Operating principles

- Ground durable claims in current sources when the user asks for research, frontier practice, tools, safety, or recommendations.
- Prefer artifacts that can be searched, cited, and updated: Markdown briefs, decision records, source registers, scripts, and repo-scoped skills.
- Keep generated governance practical and small. Add policy only when it changes agent behavior, safety, reproducibility, or handoff quality.
- Never commit real API keys, tokens, wallet secrets, private keys, seed phrases, or production credentials.
- Put secret names and examples in `.env.example`; put real values in the Codex environment, local shell, or a secret manager.
- For large work, capture an explicit goal, constraints, validation loop, stop condition, and evidence trail before implementation.

## Research protocol

Use the "standing on the shoulders of giants" pattern for research-heavy work:

1. State the question and scope.
2. Collect current primary or high-signal sources.
3. Extract claim-level evidence with links.
4. Separate sourced facts from inference and recommendation.
5. Record unknowns, risks, and follow-up checks.
6. Save durable findings under `docs/research/` when they should persist across sessions.

## Repository structure

- `.agents/skills/` stores repo-scoped Codex skills.
- `.codex/` stores Codex-oriented local configuration examples and repo skills.
- `docs/governance/` stores operating policy for agents, scripts, secrets, tools, and long-horizon runs.
- `docs/research/` stores sourced research briefs and templates.
- `scripts/` stores low-risk helper scripts for diagnostics and checks.

## Validation

- For documentation-only changes, run `scripts/check`.
- For changes under `elixir/`, follow `elixir/AGENTS.md` and run the relevant Elixir checks.
