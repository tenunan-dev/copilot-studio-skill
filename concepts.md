# Copilot Studio Core Concepts

Detail distilled from Microsoft Learn and the Microsoft Copilot blog (November 2026, post-Ignite 2026). For step-by-step tasks, follow the linked official pages.

## Harnesses (runtimes)

A harness is the runtime between your design and the language model: it decides when to call the model, what components to send, interprets responses, and calls tools. Everything you build runs on one of three harnesses; the choice affects behavior, capabilities, and billing. Status: Customer Conversation harness became generally available in November 2026 (Microsoft Ignite 2026); the Microsoft Copilot harness is production-ready; the standard harness remains the classic topic-based runtime.

| Aspect | Microsoft Copilot harness | Customer Conversation harness | Standard harness |
|---|---|---|---|
| Best for | Complex multi-step business processes | Customer-facing voice/chat, contact center | Rule-based agents, structured conversations |
| How it works | Reasons through a goal step by step | Multi-agent (primary + sub-agents) with escalation paths | Follows topics and rules you define |
| Recovery | Retries and finds alternative paths automatically | Escalates to a human representative | Follows the paths you built |
| Files | Creates/edits/reasons over Word, Excel, PowerPoint, PDF | Not a focus | Not a focus |
| Skills and memory | Yes | Yes | Not a focus |
| Publishing | Internal or external | Website chat or phone number | Internal or external |
| Billing | Copilot Credits (usage-based) | Copilot Credits (usage-based) | Copilot Studio capacity model (per-message packs) |

Example fits: accounts payable (read invoices, match POs, route exceptions) → Microsoft Copilot harness; website chat agent with a phone number and human escalation → Customer Conversation harness; internal help desk answering common questions → standard harness.

## Agents

- Created by describing in plain language (natural-language build, preview: describe a business goal and Copilot Studio determines the right combination of agents and workflows, creating multiple assets in one session).
- Instructions + knowledge + tools; reasoning decides the next step.
- Generative orchestration on by default; turn it off for classic topic-only mode (topics can still call tools).
- Agent accounts (preview): Entra ID, mailbox, Teams/directory presence; agent completes business processes end to end, responding to email, Teams messages, Office comments with its own identity. Dedicated agent accounts with managed credentials and approved-resource access enter public preview in December 2026 (teammate-like agents you can @-mention that keep working around the clock). Agent sharing is GA: multiple makers co-author the same agent.
- Upgrade path: standard → Microsoft Copilot harness (preview) carries instructions, tools, prompts; rebuilds topics as skills or workflows; produces a migration report.

## Workflows and agent flows

- **Workflows**: drag-and-drop designer; each step can reason and act; AI generation and end-to-end validation; built-in testing; human-in-the-loop controls. Nodes include extract (pull named values/tables from documents like invoices, contracts, financial statements), Copilot node (preview: run Copilot Chat or a Cowork task grounded in the connected user's mail/files/calendar/chats; call Researcher, Analyst, or Agent Builder agents), agent node (call a Copilot Studio agent from an agent flow), and classify node (decision-scoring model by default since November 2026, e.g. email triage and routing). Per-workflow Copilot Credit usage is visible to makers. Agents and workflows can also be created in natural language from Copilot Cowork or Copilot Code (public preview, November 2026) and then governed in Copilot Studio.
- **Agent flows**: established flow format, Power Automate-like authoring, native to Copilot Studio. Standalone, or attached to an agent as a tool that returns results. Can run prompts, call agents, include human review steps.

## Tools

| Tool type | What it does |
|---|---|
| Prebuilt connector | One of thousands of Power Platform connectors (Outlook, Teams, ServiceNow, Dataverse, weather, etc.) |
| Custom connector | Your own REST API wrapped as a connector |
| Prompt | AI Builder text/generative AI prompts (basic, standard, premium tiers by underlying model; premium charges for advanced reasoning) |
| Agent flow | Automation attached as a tool |
| Workflow (preview) | Multistep automated process as a tool for Copilot-harness agents |
| MCP server (preview) | External service exposed via Model Context Protocol |
| Connected agent | Another Copilot Studio agent, Foundry agent, Microsoft 365 Agents SDK agent, or A2A agent (preview) |
| Skill | Reusable capability package (marketplace sharing in preview, with update notifications) |

Tools in an agent vs Microsoft 365 Copilot plugin: tools belong to one agent and its orchestration decides when they run (maker-managed, Power Platform data policies); a plugin packages skills + tools (MCP servers) + agents for use directly in Copilot experiences (admin-managed in Microsoft 365 admin center).

## Knowledge

Add from the Build tab (agent level) or via generative answers node (topic level, standard harness). Uploaded files: PDF, Word, Excel, PowerPoint. Featured sources: public websites, SharePoint, OneDrive for Business, Salesforce, ServiceNow, Azure SQL. Advanced: Azure DevOps Wiki, Azure DevOps Work Items, Bing Custom Search, Custom Connector, Enterprise websites, Confluence. Also: Dataverse tables (with preview unstructured reasoning over Multiline Text and File columns), Copilot connectors (non-Microsoft data indexed for Copilot), Jira. Attachments in a conversation are end-user files, not knowledge sources (maker-defined grounding). SharePoint tip: document titles are a selection signal, so use clear descriptive titles. Work IQ (GA Oct 2026, on by default for new Copilot-harness agents) grounds responses in real-time org context: files, emails, meetings, chats, Business Applications; write operations enabled by default subject to org policy. Fabric IQ (preview) grounds in Microsoft Fabric semantic models.

## Publishing and channels

Publish overview: https://learn.microsoft.com/en-us/microsoft-copilot-studio/publication-fundamentals-publish-channels

- Microsoft: Microsoft Copilot app (agent list), Microsoft Teams, SharePoint (standard harness only).
- Web/app: demo website (prebuilt test/demO site), custom web app (iframe embed), native app via Direct Line.
- Preview: MCP client (agent as remote MCP server), A2A client (agent callable by other agents over Agent2Agent protocol), both authenticated with Microsoft Entra ID, early release cycle environments.
- Real-time voice: same agent across voice and digital messaging channels (digital messaging preview); GPT-5-Chat (preview) model for voice customization; Application Insights monitoring.
- Contact center: Genesys, LivePerson, Salesforce, ServiceNow, Dynamics 365 Omnichannel. Escalation/handoff triggers a Microsoft 365 Agents SDK skill routed through Azure Bot Service; handoff requires Dynamics 365 Omnichannel or another engagement hub.
- Teams + Microsoft Copilot setup: https://learn.microsoft.com/en-us/microsoft-copilot-studio/publication-add-bot-to-microsoft-teams
- WhatsApp (Azure Communication Services-based): no new agent connections from October 23, 2026; existing ones keep working.

## Autonomous triggers (preview)

https://learn.microsoft.com/en-us/microsoft-copilot-studio/agents-experience/authoring-add-event-trigger

- Triggers: connected-service events (e.g., new SharePoint item), incoming email, scheduled time.
- Share the autonomous agent so others can run it with their own credentials.
- Combine with agent accounts for fully proactive agents.

## Models

- Standard harness default: GPT-5.5 Chat. Also GA: Claude Opus 4.8. Preview: GPT-5.3 Chat.
- Copilot harness: model dropdown; experimental models for early evaluation; external models available (may require data processing/storage outside your organization's geographic boundaries).
- Model retirement: keep your agent on the current model up to 30 days after Copilot Studio upgrades the default.

## Analytics and evaluations

- Analytics: performance monitoring, custom metrics, session outcomes (standard harness).
- Evaluations: test sets, shared grader library, content safety test method (configurable severity thresholds for hateful, sexual, violent, self-harm content).
- Monitor page: per-agent Copilot Credit consumption with activity breakdown.
- Telemetry: environment-level agent telemetry export to Azure Application Insights via Power Platform admin center (preview).
