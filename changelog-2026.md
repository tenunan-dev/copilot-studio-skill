# Snapshot: Notable Changes from Official What's New (2026)

Recorded from https://learn.microsoft.com/en-us/microsoft-copilot-studio/whats-new and the Power Platform docs as of November 2026. Releases roll out over several days. Always re-check the What's New page and Roadmap for current status.

## Power Platform notes (2026)

- Effective January 2, 2026, the Power Apps per app SKU is no longer available to new customers through some purchasing channels (existing customers/CSP vary).
- Dataverse for Teams environments are deprecated; use standard environments.
- Unmanaged developer environments (incl. classic Power Apps Developer Plan environments) are deprecated; Developer Plan now provisions managed developer environments.
- Managed environments recommended for at-scale governance; environment groups for bulk policy management.
- Power Platform Licensing Guide current edition: October 2026.

## Developer tooling (2026)

- The **Copilot Studio extension for Visual Studio Code** is generally available: clone agents to local YAML, edit with IntelliSense, sync with preview/get/apply, Git-based team workflows (https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-overview).
- Microsoft publishes **skills-for-copilot-studio** on GitHub: skills for AI coding agents (GitHub Copilot CLI, Claude Code) to build/edit agent YAML with schema validation and templates (https://github.com/microsoft/skills-for-copilot-studio).
- Copilot Studio MCP lets VS Code and GitHub Copilot CLI create, test, deploy, and monitor agents from inside the tool.
- **Dataverse MCP server**: GitHub Copilot in VS Code and Copilot CLI can connect to a Dataverse environment at `{instance URL}/api/mcp` (GA) or `/api/mcp_preview` (preview), enabled per environment by admins.
- **Power Platform Tools** VS Code extension remains the recommended Power Platform CLI (pac) install, with auto-updates and authentication profile management.

## October 2026

- **Customer Conversation harness (preview)**: customer-facing agents over speech and chat with specialized sub-agents and human escalation; build from Copilot Studio or the Microsoft Contact Center Intelligence portal (portal only connects to a live contact center). Billed in Copilot Credits.
- Admin control over which knowledge sources makers can add (local files, SharePoint/OneDrive, public websites).
- **Work IQ GA**: on by default for every new Microsoft Copilot harness agent; grounds responses in real-time org context (files, emails, meetings, chats); write operations enabled by default subject to org policy.
- Model retirement grace: keep current AI model up to 30 days after a default-model upgrade.
- **Copilot Studio MCP**: VS Code and GitHub Copilot CLI can create, test, deploy, and monitor agents/workflows.
- **Harness upgrade (preview)**: ask Copilot Studio to upgrade standard → Microsoft Copilot harness; migration report included.
- **MCP and A2A channels (preview)**: expose agent as remote MCP server or A2A agent; Entra ID auth.
- OneDrive for Business knowledge source with Purview sensitivity label support; Add knowledge dialog suggestions; SharePoint title matching.
- **Marketplace-shared skills (preview)**: share skills with specific people or whole org; update notifications.
- **Agent accounts (preview)**: agent with own Entra ID, mailbox, Teams presence; responds to email, Teams messages, Office comments.
- **Autonomous triggers (preview)**: run agent on events (SharePoint, email, schedule); shareable to run with others' credentials.
- Connected agents expanded: Foundry agents, Microsoft 365 Agents SDK agents, A2A agents (preview).
- Models: GPT-5.5 Chat default on standard harness; Claude Opus 4.8 GA; GPT-5.3 Chat preview.
- Privacy statement link at conversation start (preview).
- WhatsApp: no new Azure Communication Services-based connections from October 23, 2026.

## September 2026

- Workflow **extract node**: pull named values/tables from documents (invoices, contracts, financial statements).
- Workflow **Copilot node (preview)**: run Copilot Chat or Cowork tasks grounded in the connected user's mail/files/calendar/chats; call Researcher, Analyst, Agent Builder agents.
- Model dropdown for Copilot-harness agents, experimental models.
- Content safety test method for evaluations (hateful/sexual/violent/self-harm severity thresholds).
- **File attachments GA** for conversations (Excel, PowerPoint, Word added).
- **Dataverse tables as knowledge source**, with preview unstructured reasoning over Multiline Text and File columns.

## August 2026

- **Copilot Credits** usage-based billing for Copilot-harness agents, workflows, apps; pay-as-you-go or one-year prepaid in Power Platform admin center.
- **Fabric IQ (preview)**: ground responses in Microsoft Fabric business data/semantic models.
- **Microsoft Agent 365 onboarding** for Copilot Studio agents (Entra identity, Conditional Access, centralized observability).
- Admin control of image rendering and embedded URLs per environment/environment group.
- Azure SQL tables as knowledge source.
- Work IQ (preview at the time) for real-time shared org context.

## July 2026

- **Microsoft Entra Agent ID auto-created for every new agent**; environment-level opt-out removed.
- Workflow or MCP server as a tool for Copilot-harness agents (preview).
- MCP server Microsoft certification submission (preview).
- Real-time voice agents across voice and digital messaging (digital preview); GPT-5-Chat (preview); Application Insights monitoring.
- Environment-level agent telemetry export to Azure Application Insights (preview).
- File attachments preview for Copilot-harness agents (view agent-created files).

## June 2026

- **Microsoft Copilot harness production-ready preview**: enhanced orchestration runtime, new agent-building experience, alongside standard harness.
- Work IQ for org data access (emails, calendar, files) for Copilot-harness agents.
