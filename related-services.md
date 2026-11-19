# Related Services and the Microsoft Agent Ecosystem

How Microsoft Copilot Studio fits with the rest of Microsoft's agent stack (as of October 2026 docs).

## Ecosystem map

```
                    ┌────────────────────────────┐
                    │   Microsoft 365 Copilot    │  ← user-facing Copilot app
                    │  (Chat, Cowork, Code,      │     (agents, plugins surface here)
                    │   Autopilot, plugins)      │
                    └──────────┬─────────────────┘
                               │
   ┌────────────────┐   ┌──────┴───────┐   ┌──────────────────────┐
   │ Copilot Studio │   │ Agent 365    │   │ Microsoft Foundry     │
   │ (low-code:     │──▶│ (control     │◀──│ (pro-code AI platform)│
   │ agents, flows, │   │  plane +     │   │  Azure AI Agent       │
   │ workflows,     │   │  observability│  │  Service, models)     │
   │ apps)          │   └──────────────┘   └──────────┬───────────┘
   └───────┬────────┘                                  │ connected agents
           │ tools/knowledge                            │
   ┌───────┴──────────────────────────────┐   ┌────────┴───────────┐
   │ Power Platform: connectors (1000+),  │   │ Microsoft 365       │
   │ Power Automate / agent flows,        │   │ Agents SDK          │
   │ Dataverse                            │   │ (pro-code, multi-   │
   └──────────────────────────────────────┘   │  channel)           │
                                              └────────────────────┘
```

## Microsoft 365 Copilot

- The Copilot app and ecosystem where Copilot Studio agents can be published (web + desktop, Teams).
- Components: Copilot Chat, Copilot Cowork, Copilot Code (preview), Copilot Autopilot, Researcher, Analyst, Agent Builder agents.
- **Plugins**: package skills, tools (including MCP servers), and agents so people find/install/manage them in supported Copilot experiences. Admin-managed in Microsoft 365 admin center; Microsoft 365 Copilot Plugin Hub. Use a plugin when the capability belongs in Copilot experiences rather than inside one designed agent conversation.
- Docs: https://learn.microsoft.com/en-us/microsoft-365/copilot/

## Microsoft Agent 365

- The observability/governance platform for AI agents: manage every agent from one place, wherever it was built.
- Identity representation in Microsoft Entra, Conditional Access and access governance workflows, centralized observability, agent inventory, lifecycle, tools, settings in Microsoft 365 admin center.
- Business value reporting (spend on AI and return) via the Agent overview page.
- Copilot Studio agents onboard to Agent 365 for centralized governance.
- Docs: https://learn.microsoft.com/en-us/microsoft-agent-365/

## Microsoft Foundry (formerly Azure AI Foundry)

- Unified Azure platform-as-a-service for enterprise AI operations, model builders, and application development.
- Agents built in Microsoft Foundry (or Azure AI Agent Service) can be added to Copilot Studio as **connected agents**; Copilot Studio calls them when relevant.
- Foundry agents can also be published to Microsoft 365 and Teams directly.
- Docs: https://learn.microsoft.com/en-us/microsoft-foundry/

## Microsoft 365 Agents SDK

- Pro-code SDK (successor path from Bot Framework SDK / Teams AI library) for building full-stack, multichannel, trusted agents for M365, Teams, Copilot Studio, and Webchat.
- Copilot Studio agents built with it are "custom engine agents."
- Also used in Copilot Studio escalation flows: a handoff triggers a Microsoft 365 Agents SDK skill routed through Azure Bot Service.
- GitHub: https://github.com/microsoft/agents

## Power Platform family

- **Connectors**: prebuilt connectors to thousands of Microsoft and non-Microsoft services; usable as agent tools or knowledge (Copilot connectors). Custom connectors wrap REST APIs.
- **Power Automate / agent flows**: agent flows are native to Copilot Studio with Power Automate-like authoring; can run standalone or as agent tools; support prompts, agent calls, human review.
- **Dataverse**: the data platform behind Power Platform and Dynamics 365. Dataverse tables work as knowledge sources (structured + preview unstructured columns). Agent configuration is stored in Dataverse; REST APIs (Dataverse Web API) allow programmatic agent management (create, publish, export/import as solutions). Copilot Studio also has dedicated connectors for evaluation/test management.
- Admin: Power Platform admin center (environments, DLP, Copilot Credits purchase/management, knowledge source restrictions, image rendering controls, telemetry export).

## MCP (Model Context Protocol) integration

- **Copilot Studio MCP**: connect MCP-compatible clients (Visual Studio Code, GitHub Copilot CLI) to create, test, deploy, and monitor agents and workflows without leaving the tool.
- **Agents as MCP servers**: expose your agent as a remote MCP server (MCP client channel, preview) so other tools, IDEs, and orchestrators can call it, authenticated with Microsoft Entra ID.
- **MCP servers as tools** (preview): attach external MCP servers or workflows as tools for Copilot-harness agents.
- **MCP certification** (preview): submit MCP servers for Microsoft certification for reliability, security, compliance confidence.

## Agent2Agent (A2A) protocol

- A2A client channel (preview): expose your agent to other agents over A2A.
- Add A2A agents as connected agents to delegate tasks to agents built outside Copilot Studio.

## Microsoft Contact Center Intelligence portal

- Same authoring experience as the Customer Conversation harness in Copilot Studio, but also connects the agent to a live contact center.

## Microsoft Entra ID for agents

- **Microsoft Entra Agent ID**: automatically created for every new Copilot Studio agent since July 2026 (environment-level opt-out removed). Provides identity for auth, governance, Conditional Access.
- Agent accounts (preview): full account with mailbox and Teams presence for proactive agents.

## Choosing where to build

| Need | Use |
|---|---|
| Low-code agent, fast time to value, business user | Copilot Studio |
| Customer service over voice/chat with escalation | Copilot Studio Customer Conversation harness or Contact Center Intelligence portal |
| Rule-based predictable bot, topic-driven | Copilot Studio standard harness |
| Pro-code, custom models, full control | Microsoft Foundry or Microsoft 365 Agents SDK (then connect to Copilot Studio) |
| Lightweight agent inside Microsoft 365 Copilot only | Agent Builder / declarative agents in Microsoft 365 Copilot |
| Govern and observe all agents | Microsoft Agent 365 |
