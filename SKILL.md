---
name: |
  copilot-studio
description: |
  Load this skill for questions or tasks about Microsoft Copilot Studio, Power Platform and its family — Power Apps, Power Automate, Power Pages, Power BI, Microsoft Dataverse, connectors, AI Builder, Power Fx — plus agent harnesses, knowledge sources, channels, triggers, Copilot Credits and licensing, ALM and environments, and the wider Microsoft agent ecosystem (Microsoft 365 Copilot, Agent 365, Microsoft Foundry, Microsoft 365 Agents SDK, MCP).
---

# Microsoft Copilot Studio, Power Platform, and Dataverse

Microsoft Copilot Studio is Microsoft's graphical, low-code studio for building and managing AI-powered agents and workflows. It is one of the five Power Platform products (with Power Apps, Power Automate, Power BI, and Power Pages), all sharing Microsoft Dataverse as the data platform. Access Copilot Studio at https://copilotstudio.microsoft.com; build apps at https://make.powerapps.com; administer everything at https://admin.powerplatform.microsoft.com. Official docs: https://learn.microsoft.com/en-us/power-platform/

Core facts as of the November 2026 documentation (post-Microsoft Ignite 2026). Copilot Studio moved from a topic-only chatbot tool to a single studio combining agents, workflows, and apps. Three **harnesses** (runtimes) power everything you build:

1. **Microsoft Copilot harness** — reasoning-heavy, multistep business processes. Reasons from instructions, breaks goals into steps, calls tools, recovers from failures, creates/edits Word/Excel/PowerPoint/PDF files natively, supports skills and memory, runs tasks in a secure sandbox. Billed in Copilot Credits (usage-based).
2. **Customer Conversation harness** (GA, November 2026) — customer-facing voice and chat, contact-center style. A primary agent works with specialized sub-agents, each with a human escalation path. Billed in Copilot Credits.
3. **Standard harness** — rule-based agents with *topics*, structured predictable conversations (formerly the "classic" Copilot Studio / Power Virtual Agents experience). Billed with the Copilot Studio capacity model (per-message packs), not credits.

## Building blocks

- **Agents**: AI assistants that converse and complete tasks using instructions, knowledge, and tools. Can be created by describing them in plain language (also from Copilot Cowork/Code, preview). Agents can get their own Microsoft Entra ID account, mailbox, and Teams presence (preview) to act proactively; dedicated agent accounts (managed credentials, teammate-like agents you can @-mention) enter public preview December 2026. Agent sharing is GA: multiple makers can co-author the same agent.
- **Workflows**: drag-and-drop automations where each step can reason and act; AI helps generate and validate end to end; built-in testing and human-in-the-loop. Nodes include extract, Copilot node (preview), agent node, and classify node (decision-scoring model by default since November 2026); per-workflow Copilot Credit usage visibility.
- **Agent flows**: established flow format native to Copilot Studio (similar authoring to Power Automate); standalone or attached to an agent as a tool.
- **Apps** (GA November 2026, rolling out with Copilot Cowork): app creation experience in Copilot Studio; running these apps is included with Power Apps Premium subject to request limits, then Copilot Credits.
- **Skills**: reusable capability packages; can be shared across makers/organization via marketplace (preview); standard-harness topics can be rebuilt as skills or workflows during harness upgrade.
- **Topics**: standard harness conversation units with connected steps, questions, conditions.

## Harness selection

- Complex multi-step process, files, judgment → Microsoft Copilot harness.
- Customer support over voice/chat with escalation → Customer Conversation harness.
- Well-defined, rule-based, predictable → standard harness.
- Copilot Studio can upgrade standard-harness agents to the Microsoft Copilot harness (preview, produces a migration report).

## Tools and knowledge

Agent tools: prebuilt/custom Power Platform connectors, agent flows, prompts (basic/standard/premium tiers), REST APIs, MCP servers, connected agents (other Copilot Studio agents, Microsoft Foundry agents, Microsoft 365 Agents SDK agents, A2A agents preview). Generative orchestration is on by default (agent picks the tool/topic/knowledge); topics can also call tools explicitly.

Knowledge sources: uploaded files (PDF/Word/Excel/PowerPoint), public websites, SharePoint, OneDrive for Business, Dataverse tables, Azure SQL, ServiceNow, Salesforce, Confluence, Jira, Azure DevOps (wiki/work items), Bing Custom Search, Enterprise websites, Copilot connectors (non-Microsoft data indexed for Copilot), Work IQ (real-time grounding in files/email/meetings/chats, GA and on by default for new Copilot-harness agents), Fabric IQ (preview, Microsoft Fabric semantic models).

## Publishing and channels

Microsoft channels: Microsoft Copilot app, Microsoft Teams, SharePoint (standard harness only). Web/app: demo website, custom web app via iframe, native apps via Direct Line. Preview channels: MCP client (agent as remote MCP server) and A2A client, authenticated with Microsoft Entra ID. Voice: real-time voice agents deployable across voice and digital messaging. Contact center: Genesys, LivePerson, Salesforce, ServiceNow, Dynamics 365 Omnichannel (handoff via Microsoft 365 Agents SDK skill routed through Azure Bot Service); the Customer Conversation harness (GA) is Microsoft's purpose-built path for customer-facing voice/chat. Note: no new WhatsApp agents via Azure Communication Services channel as of October 23, 2026.

## Autonomous agents

Event triggers (preview) run agents autonomously on SharePoint events, incoming email, or schedules; autonomous agents can be shared to run with other users' credentials. Agents can respond to email, Teams messages, and Office comments with their own identity (preview).

## Models

Standard harness default: GPT-5.5 Chat; Claude Opus 4.8 GA; GPT-5.3 Chat preview. Copilot harness: model dropdown, experimental models, external models possible (may process data outside your geography). Agents can stay on their current model up to 30 days after a default-model upgrade.

## Governance, security, billing

- Microsoft Entra Agent ID auto-created for every new agent since July 2026 (no opt-out).
- Security audit logging flows through Microsoft Purview (agent invocations, tool calls, policy enforcement); DLP for Copilot Studio; sensitivity label inheritance; Power Platform admin center controls (restrict knowledge sources, image rendering/URLs, environment-level agent telemetry export to Azure Application Insights).
- Microsoft Agent 365: observability/control plane for all agents (inventory, identity in Entra, Conditional Access, centralized management in Microsoft 365 admin center).
- Billing: Microsoft Copilot and Customer Conversation harnesses use **Copilot Credits** (usage-based; pay-as-you-go via Azure subscription or prepaid packs, managed in Power Platform admin center; monitor per-agent consumption on the Monitor page). Standard harness uses the Copilot Studio capacity model. Licensing Guide (PDF): search "Microsoft Copilot Studio Licensing Guide" for current rates.
- Analytics and evaluations: session analytics, custom metrics, test sets with a shared grader library, content safety test method (harmful-content thresholds), model upgrades.

## Power Platform family (details in `power-platform.md`, `power-apps.md`, `dataverse.md`, `power-automate.md`)

- **Power Platform** = 5 products (Copilot Studio, Power Apps, Power Automate, Power BI, Power Pages) + shared capabilities (Dataverse, connectors, AI Builder, Power Fx, Copilot/generative AI). Administered via the **Power Platform admin center**: environments, DLP, managed environments, capacity, Copilot Credits.
- **Power Apps**: low-code custom business apps; two classic types (**canvas** apps with pixel-level control in Power Apps Studio, **model-driven** apps generated from Dataverse data via app designer), plus **Plans** (copilot-first: describe your use case, get a full solution) and the new AI-native Power Apps experience (preview). Runs in browser and Power Apps mobile.
- **Power Automate**: **cloud flows** (automated/instant/scheduled), **desktop flows** (RPA for web and desktop, attended or unattended), and **generative actions** (preview: state intent, AI picks and orders the actions). Copilot Studio agent flows are the Copilot Studio-native variant.
- **Microsoft Dataverse**: the secure cloud data platform under Power Platform and Dynamics 365. Data lives in **tables** (rows + columns) with rich metadata, relationships, server-side logic (business rules, business process flows, workflows, calculated columns), and layered security (business units, role-based, row-level, column-level). Terminology: entity→table, field/attribute→column, record→row, option set→choice. Dataverse Web API for pro-code. Dataverse for Teams environments are deprecated.
- **Environments and ALM**: default/sandbox/production/developer environment types; managed environments for admin-at-scale; **solutions** (managed/unmanaged) and **pipelines** for application lifecycle management.
- **Power Fx**: the open-source, Excel-like low-code language across canvas apps, Dataverse formula columns, and more.
- **AI Builder**: add prebuilt and custom AI models (document processing, prediction, extraction, text recognition) to Power Apps and Power Automate.
- **Power Pages**: low-code external-facing websites securely backed by Dataverse.
- **Licensing**: Power Apps per user plans (per app SKU no longer available to new customers through some channels from Jan 2, 2026); Power Automate per user/per flow; pay-as-you-go with Azure; Dataverse capacity (database, file, log); managed environments add-on; Copilot Credits for Copilot Studio harnesses. Always check the current Power Platform Licensing Guide (October 2026 edition) rather than quoting prices.

## VS Code tooling (details in `vscode-extension.md`)

Three official Microsoft VS Code developer surfaces (plus the new Copilot Studio CLI and GitHub-repo-backed developer artifacts, both public preview as of November 2026):
- **Copilot Studio extension** (GA, marketplace ID `ms-CopilotStudio.vscode-copilotstudio`) for standard-harness agent authoring: **Clone** cloud agents to local YAML (`agent.mcs.yaml`, `topics/`, `actions/`, `workflows/`, `trigger/`, `knowledge/files/`, settings, connection references) via the Agents pane, command palette, or agent URL; **Edit** AdaptiveDialog topics (SendActivity, Question, Power Fx ConditionGroup), tools, triggers with IntelliSense and the Problems pane; **Sync** with Preview (cloud→local), Get (cloud→local, conflict review), Apply (local→cloud, updates the live agent, blocked if remote changes weren't retrieved, NOT publish). Team ALM via Git/PR and `Copilot Studio: Reattach Agent`; solutions + pipelines remain the recommended deployment path.
- **Power Platform Tools extension** (`microsoft-IsvExpTools.powerplatform-vscode`): the recommended install of the **Power Platform CLI (pac)** — Dataverse solutions (create/pack/unpack/import), packages, environment management, Power Apps portals, auth profile management. Auto-updates; pac runs by default in the VS Code PowerShell terminal (CMD/PowerShell need .NET Tool/MSI/PATH).
- **Dataverse MCP server** with GitHub Copilot: expose a Dataverse environment at `{instance URL}/api/mcp` (GA) or `/api/mcp_preview` (preview). VS Code: `MCP: Add Server` → HTTP/SSE → paste URL + `/api/mcp` → use agent mode. Copilot CLI: add to `~/.copilot/mcp-config.json` or install the Dataverse plugin from the Awesome Copilot marketplace and run `/dataverse:mcp-configure`. Requires the Microsoft GitHub Copilot MCP client to be allowed in the environment.

## Related services

- **Microsoft 365 Copilot**: the Copilot app where Copilot Studio agents appear; includes Copilot Chat, Cowork, Code, Autopilot; plugins (skills + tools + agents packaged for Copilot experiences, managed by admins in M365 admin center, Plugin Hub).
- **Microsoft Agent 365**: agent governance and observability platform for the organization.
- **Microsoft Foundry** (formerly Azure AI Foundry): pro-code enterprise AI platform; agents built there connect into Copilot Studio as connected agents.
- **Microsoft 365 Agents SDK** (formerly Bot Framework SDK): pro-code SDK for full-stack multichannel agents; also used for handoff/escalation integrations.
- **Power Platform**: connectors (1000+ services), Power Automate (agent flows), Dataverse (data platform; agent tables; REST APIs to manage agents programmatically).
- **MCP ecosystem**: Copilot Studio MCP server lets VS Code and GitHub Copilot CLI create/test/deploy/monitor agents; MCP server certification; agents exposed as MCP servers.
- **Microsoft Contact Center Intelligence portal**: same authoring as Customer Conversation harness plus live contact-center connection.

## Working with this skill

Copilot Studio evolves rapidly (harnesses, credits, preview→GA transitions). For version-sensitive details (exact credit rates, channel availability, model lists, preview status), verify against the official docs before answering definitively:
- Copilot Studio docs hub: https://learn.microsoft.com/en-us/microsoft-copilot-studio/
- Power Platform docs hub: https://learn.microsoft.com/en-us/power-platform/
- Power Apps overview: https://learn.microsoft.com/en-us/power-apps/powerapps-overview
- Dataverse overview: https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-intro
- Power Automate flow types: https://learn.microsoft.com/en-us/power-automate/flow-types
- Power Fx overview: https://learn.microsoft.com/en-us/power-platform/power-fx/overview
- AI Builder overview: https://learn.microsoft.com/en-us/ai-builder/overview
- Power Pages overview: https://learn.microsoft.com/en-us/power-pages/introduction
- Environments overview: https://learn.microsoft.com/en-us/power-platform/admin/environments-overview
- ALM basics: https://learn.microsoft.com/en-us/power-platform/alm/basics-alm
- Power Platform licensing overview: https://learn.microsoft.com/en-us/power-platform/admin/pricing-billing-skus
- Agent 365: https://learn.microsoft.com/en-us/microsoft-agent-365/
- Microsoft 365 Copilot hub: https://learn.microsoft.com/en-us/microsoft-365/copilot/
- What's new in Copilot Studio: https://learn.microsoft.com/en-us/microsoft-copilot-studio/whats-new
- Harnesses: https://learn.microsoft.com/en-us/microsoft-copilot-studio/harnesses-overview
- Harness comparison guidance: https://learn.microsoft.com/en-us/microsoft-copilot-studio/guidance/choose-harness
- Knowledge sources: https://learn.microsoft.com/en-us/microsoft-copilot-studio/agents-experience/knowledge-sources-overview
- Channels: https://learn.microsoft.com/en-us/microsoft-copilot-studio/agents-experience/publication-channels-overview
- Standard harness licensing: https://learn.microsoft.com/en-us/microsoft-copilot-studio/billing-licensing
- Usage-based billing (Copilot Credits): https://learn.microsoft.com/en-us/microsoft-copilot-studio/agents-experience/billing-credit-overview
- Security and governance: https://learn.microsoft.com/en-us/microsoft-copilot-studio/security-and-governance
- VS Code extension overview: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-overview
- VS Code extension install: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-install-configure
- VS Code extension clone: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-clone-agent
- VS Code extension edit: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-edit-agent-components
- VS Code extension sync: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-synchronization
- Power Platform Tools VS Code extension: https://learn.microsoft.com/en-us/power-platform/developer/howto/install-vs-code-extension
- Power Platform developer tools: https://learn.microsoft.com/en-us/power-platform/developer/tools
- Dataverse MCP with GitHub Copilot in VS Code: https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-mcp-vscode

Support files in this directory:
- `concepts.md` — deeper detail on harnesses, tools, knowledge, channels, triggers, models.
- `related-services.md` — the Microsoft agent ecosystem and how services relate.
- `governance-billing.md` — security, Purview, admin controls, Copilot Credits and licensing models.
- `power-platform.md` — Power Platform overview, admin center, environments, ALM, licensing, Power Fx, AI Builder, Power Pages, Power BI.
- `power-apps.md` — canvas apps, model-driven apps, Plans, maker experience, developers.
- `dataverse.md` — Dataverse tables, logic, security, integration, developer APIs.
- `power-automate.md` — cloud flows, desktop flows (RPA), generative actions, Copilot in flows.
- `vscode-extension.md` — VS Code tooling: Copilot Studio extension (clone/edit/sync agents), Power Platform Tools (pac CLI for Dataverse ALM), Dataverse MCP with GitHub Copilot.
- `changelog-2026.md` — snapshot of notable changes recorded from the official What's New pages and Copilot blog (June–November 2026).
