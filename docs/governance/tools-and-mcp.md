# Tools, MCP, Skills, and Progressive Disclosure

## Stack layers

| Layer | Best use | Persistence | Context impact |
| --- | --- | --- | --- |
| `AGENTS.md` | repo policy and workflow defaults | Git | always relevant inside scope |
| Skills | packaged expertise for repeatable workflows | Git/user/system | metadata first, full file only when used |
| Scripts | deterministic repeatable actions | Git | low if invoked by name |
| MCP servers | live tools and external context | config/environment | depends on exposed tool list |
| External stores | memory, corpora, embeddings, graph data | external | low if accessed through search/retrieval |

## Skill policy

Skills are high leverage, but they are also executable influence over an agent. Add them deliberately.

A good repo skill should:

- have one clear job;
- include trigger words in the `description`;
- keep `SKILL.md` short;
- put longer details in `references/`;
- include scripts only when deterministic behavior is needed;
- be validated before relying on it.

This repo starts with `.agents/skills/research-brief`, a source-grounded research workflow skill.

## MCP policy

Use MCP when the agent needs live information or a tool outside the repo, such as Firecrawl, GitHub, Linear, Figma, browser automation, logs, databases, or a memory store.

For many MCP servers, prefer progressive disclosure:

1. expose only the server(s) needed for the task;
2. use allow lists for high-risk servers;
3. prefer read-only scopes first;
4. set per-tool approval modes for mutating tools;
5. document each configured server in a tool registry before making it default.

## Gateway pattern

For a large tool catalog, use an MCP gateway or small local CLI wrapper instead of preloading every server. The gateway should expose a small stable set of discovery tools, then route to specialized tools only when needed.

Recommended first-class tool groups:

- research: Firecrawl, browser/search, docs retrieval;
- project: GitHub, Linear, local repo search;
- memory: vector/graph store, notes, source register;
- verification: Playwright/browser, test runners, trace/eval tooling;
- communication: Slack/Telegram/Discord only after safety boundaries are defined.
