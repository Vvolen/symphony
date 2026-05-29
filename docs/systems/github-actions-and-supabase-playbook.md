# GitHub Actions and Supabase Playbook

## What GitHub can do for this repository

GitHub-native automation can make the repo do real work even when no agent is actively chatting:

| Capability | Example | First implementation |
| --- | --- | --- |
| Validation | Run repo checks on every PR/push. | `.github/workflows/research-hub-check.yml` |
| Drift detection | Detect stale memory indexes or missing run-log sections. | `scripts/memory-check` |
| Scheduled research refresh | Open issue/PR when tracked sources change. | future scheduled workflow |
| Prompt queue | Pick up queued task specs and dispatch agents. | future queue + approval gate |
| Secret scanning guardrails | Fail on obvious committed secrets. | current `./scripts/check`, future GitHub secret scanning config |

## Supabase direction

Supabase is useful here as a future memory and coordination backend, but should be added in phases:

1. **Docs-only design**: define tables and access model.
2. **Local CLI/dev stack**: add `supabase/` migrations and generated types.
3. **Managed project**: connect GitHub Actions with `SUPABASE_ACCESS_TOKEN` and project refs.
4. **Memory API**: expose read/write through a narrow service or MCP server.
5. **Agent policy**: require read-only access by default; writes need run IDs and provenance.

## Candidate tables

| Table | Purpose |
| --- | --- |
| `sources` | URLs, retrieval dates, source quality, freshness windows. |
| `artifacts` | Docs, modules, skills, scripts, and their owning system. |
| `runs` | Long-horizon run metadata, status, validation, and handoff. |
| `decisions` | ADRs and decision states. |
| `memory_edges` | Lightweight graph between sources, claims, modules, and runs. |

## CLI/tooling note

This environment can run networked install commands when needed, including npm/npx-based tools, Supabase CLI installers, and Firecrawl packages. Do not add a live dependency until the exact package, version, permissions, and secret requirements are documented.

## Sources

- GitHub Actions docs: <https://docs.github.com/en/actions>
- Supabase CLI reference: <https://supabase.com/docs/reference/cli/about>
- Supabase migrations docs: <https://supabase.com/docs/guides/deployment/database-migrations>
- Supabase GitHub Actions example: <https://supabase.com/docs/guides/functions/examples/github-actions/>
- Supabase self-hosting docs: <https://supabase.com/docs/guides/self-hosting>
