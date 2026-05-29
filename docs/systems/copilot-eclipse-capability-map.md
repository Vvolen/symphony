# Copilot for Eclipse Capability Map

## Source baseline

- Repository: <https://github.com/microsoft/copilot-for-eclipse>
- Official feature matrix: <https://docs.github.com/en/copilot/reference/copilot-feature-matrix?tool=eclipse>
- Copilot SDK custom agents: <https://docs.github.com/en/copilot/how-tos/copilot-sdk/features/custom-agents>
- Agent skills docs: <https://docs.github.com/en/copilot/how-tos/copilot-on-github/customize-copilot/customize-cloud-agent/add-skills>
- Eclipse developer tools overview: <https://www.eclipse.org/ide/>
- Eclipse Project Handbook: <https://www.eclipse.org/projects/handbook/>

## What Eclipse itself contributes conceptually

Eclipse is not only an IDE. The stronger pattern for this repo is the Eclipse ecosystem model:

- vendor-neutral platform;
- explicit project governance;
- public project resources;
- formal roles and responsibilities;
- lifecycle/review gates;
- IP/security due diligence;
- extensibility through plugins and marketplaces.

For this repository, the portable idea is: **treat agentic work as an extensible platform with governance, not as a pile of prompts.**

## What Copilot for Eclipse contributes

The GitHub Copilot for Eclipse plugin exposes a compact agentic capability set:

| Capability | Why it matters here | Repository implication |
| --- | --- | --- |
| Agent Mode | Larger project-aware coding tasks need iterative autonomous loops. | Keep long-horizon run contracts and validation scripts first class. |
| Custom Agents | Specialized agents need distinct prompts/tool scopes. | Maintain role profiles for researcher, planner, builder, verifier, and archivist. |
| Isolated Subagents | Context isolation improves focus and reduces contamination. | Prefer task-scoped notes and per-agent context bundles over one giant memory file. |
| Plan Agent | Complex tasks should be planned before edits. | Require plan artifacts for long-horizon runs. |
| MCP | External tools should be attached through explicit boundaries. | Keep MCP registry/gateway docs and allow-list policy. |
| Skills | Reusable expertise should be packaged and discovered. | Continue building `.agents/skills/*` with concise triggers and references. |

## Caveat

The feature matrix currently shows Eclipse supports agent mode, custom agents, MCP, vision, and workspace indexing, while agent skills are not shown as supported for Eclipse itself. Skills remain valuable in this repo because Codex, Copilot cloud agent/CLI, and VS Code-style workflows can use repo-scoped `.agents/skills`.

## Pattern to borrow

Create an **agent constellation** rather than a single omniscient agent:

1. Researcher: source-gathering and evidence tables.
2. Planner: decomposition, constraints, run contract.
3. Builder: narrow implementation scope.
4. Verifier: tests, citations, trace review.
5. Archivist: memory index, handoff, decisions.

Keep each role's inputs small and explicit.
