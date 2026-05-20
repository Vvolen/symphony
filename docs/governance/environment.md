# Environment, Secrets, and Persistence Policy

## Mental model

An environment is the repeatable runtime Codex receives for a task: repository checkout, setup script, installed tools, configured variables, network policy, and any cached container state.

Environment variables are named values available to processes. They are powerful because they let scripts and agents adapt without changing code. They are risky because the same mechanism can expose credentials, change endpoints, alter sandbox behavior, or point tools at production systems.

## Persistence layers

| Layer | Persists across tasks? | Use for | Do not use for |
| --- | --- | --- | --- |
| Git-tracked files | Yes | docs, scripts, policies, `.env.example`, skills, templates | real secrets |
| Codex environment variables | Environment-specific | non-secret config needed during setup and agent work | private keys or credentials that the agent should not see |
| Codex secrets | Environment-specific | credentials needed only during setup | values needed by the agent after setup |
| Setup script output/cache | Up to the platform cache window | installed dependencies and tools | authoritative memory |
| Research docs | Yes | durable memory and evidence trails | stale facts without review dates |
| External memory/MCP stores | Yes, if configured | large corpora, embeddings, knowledge graphs, cross-agent memory | ungoverned sensitive data |

## Secret rules

- Never commit real API keys, wallet keys, seed phrases, SSH private keys, OAuth refresh tokens, or production credentials.
- Commit variable names and safe example values in `.env.example`.
- Prefer read-only, least-privilege keys for research tools.
- Rotate any credential that appears in a transcript, log, diff, or committed file.
- Treat trading, wallet, exchange, and Telegram automation credentials as high risk.

## Recommended variables

| Name | Secret? | Intended use |
| --- | --- | --- |
| `FIRECRAWL_API_KEY` | Yes | Firecrawl cloud API access for web search, scrape, crawl, and extraction tools. |
| `FIRECRAWL_API_URL` | No, unless private | Override for a self-hosted Firecrawl endpoint. |
| `SYMPHONY_WORKSPACE_ROOT` | No | Workspace root for Symphony-managed agent runs. |
| `SOURCE_REPO_URL` | Maybe | Repo cloned by setup hooks or Symphony workflows. |
| `LINEAR_API_KEY` | Yes | Linear API access for Symphony or Linear MCP workflows. |
| `OPENAI_API_KEY` | Yes | OpenAI API access for local scripts or MCP servers that need it. |
| `HERMES_PROFILE` | No | Select a Hermes agent profile/persona when running Hermes externally. |

## Setup-script policy

Setup scripts should install tools and dependencies. They should not become hidden product logic.

- Safe: install packages, create caches, validate versions, write non-secret shell defaults.
- Risky: mutate external systems, write secrets into files, start long-lived services without health checks.
- Important: shell `export` commands in setup scripts may not persist into the later agent phase; use environment settings or shell startup files when persistence is required.
