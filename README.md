# copilot-studio-skill

A knowledge skill covering **Microsoft Copilot Studio, the Power Platform family, Microsoft Dataverse, and related Microsoft agent services**, distilled from official Microsoft Learn documentation (current as of November 2026).

Built as a skill for **Mistral Vibe** (Work), following the open [Agent Skills](https://agentskills.io/home) standard: a `SKILL.md` entrypoint plus focused support files. Also usable as reference material for other AI coding agents (GitHub Copilot, Claude Code, etc.).

## What it covers

- **Copilot Studio**: the three agent harnesses (Microsoft Copilot, Customer Conversation, standard), agents vs workflows vs agent flows, knowledge sources (incl. Work IQ, Fabric IQ), tools, connectors, MCP/A2A channels, autonomous triggers, models, evaluations, publishing
- **Power Platform**: Power Apps (canvas, model-driven, Plans), Power Automate (cloud flows, desktop flows/RPA, generative actions), Power Pages, Power BI, AI Builder, Power Fx, environments, ALM (solutions, pipelines), licensing
- **Dataverse**: tables, metadata, server-side logic, layered security model, developer APIs, integration patterns
- **VS Code tooling**: Copilot Studio extension (clone/edit/sync agents as YAML), Power Platform Tools (pac CLI), Dataverse MCP with GitHub Copilot
- **Ecosystem**: Microsoft 365 Copilot, Agent 365, Microsoft Foundry, Microsoft 365 Agents SDK, MCP ecosystem
- **changelog-2026.md**: dated snapshot of notable changes (June-October 2026) from the official What's New pages

## Files

| File | Contents |
|---|---|
| `SKILL.md` | Entrypoint: harnesses, building blocks, tools, knowledge, channels, governance, licensing, all doc links |
| `concepts.md` | Deep dive: harnesses, agents, workflows, tools, knowledge sources, channels, triggers, models |
| `related-services.md` | Microsoft agent ecosystem map and how the services relate |
| `governance-billing.md` | Purview audit, DLP, Entra Agent ID, Copilot Credits vs capacity licensing |
| `power-platform.md` | Platform overview, admin center, environments, managed environments, ALM, Power Fx, AI Builder, Power Pages |
| `power-apps.md` | Canvas/model-driven apps, Plans, maker/developer guidance |
| `dataverse.md` | Dataverse tables, logic, security, integration, developer APIs |
| `power-automate.md` | Cloud flows, desktop flows (RPA), generative actions, flow-type decision aid |
| `vscode-extension.md` | Copilot Studio extension, Power Platform Tools, Dataverse MCP setup and usage |
| `changelog-2026.md` | 2026 changes snapshot (Copilot Studio What's New + Power Platform notes) |

## Using it

**Vibe Work**: create a new skill (Context > Skills > New skill) and paste the contents of `SKILL.md`, attaching the support files.

**Clone**:

```bash
git clone https://github.com/tenunan-dev/copilot-studio-skill.git
```

AI coding agents (GitHub Copilot, Claude Code, Cursor, and other Agent-Skills-compatible tools): reference this folder in your agent's configuration, or ask the agent to read `SKILL.md` for orientation and the support files for depth.

## Freshness

Version-sensitive details (model defaults, credit rates, channel availability, preview vs GA status) change quickly. The skill includes the canonical Microsoft Learn links for verification, and `changelog-2026.md` records the documented state as of November 2026.
