# Governance, Security, and Billing

Distilled from Microsoft Learn (October 2026). Rates and thresholds change; check the Licensing Guide and billing pages before quoting numbers.

## Security and governance

Key page: https://learn.microsoft.com/en-us/microsoft-copilot-studio/security-and-governance

- **Audit logging**: agent invocation events, tool and action calls, policy enforcement decisions, and runtime activity signals flow through the Microsoft Purview audit logging pipeline (not a separate Copilot Studio store). Tenant audit settings and retention apply. Not available in some sovereign/government clouds.
- **Microsoft Purview for Copilot Studio** (https://learn.microsoft.com/en-us/purview/ai-copilot-studio): Data Loss Prevention for Copilot Studio, sensitive information detection, sensitivity label inheritance (new Word/PowerPoint content inherits the highest priority label), AI data security for Copilot Studio.
- **Microsoft Entra Agent ID**: auto-created for every new agent since July 2026; no environment-level opt-out. Supports Conditional Access and access governance via Agent 365.
- **Authentication options for agents**: Microsoft Entra ID OAuth (user and app authentication) for secure channel and API access; SSO for Microsoft Teams and Microsoft 365 Copilot channels.
- **Power Platform admin center controls**:
  - Restrict which knowledge sources makers can add (local file uploads, SharePoint/OneDrive, public websites; independently or together) — GA Oct 2026.
  - Control image rendering and embedded URLs in agent responses, per environment or environment group.
  - DLP policies for connectors used as tools.
  - Environment-level agent telemetry export to Azure Application Insights (preview).
- **Data handling**: agent geographic boundaries; note external models may require data processing/storage outside your organization's geographic boundaries.
- **Privacy statements**: configurable privacy statement link shown at the start of agent conversations (preview).
- **Agent inventory**: inventory, secure, and manage agents org-wide with role-based access and cost management.
- **Agent 365 onboarding**: centralized governance, identity in Entra, Conditional Access, observability.

## Billing models (two parallel systems)

### 1. Copilot Credits (usage-based) — Microsoft Copilot harness and Customer Conversation harness

- Copilot Credits measure usage of agents, workflows, and apps powered by these harnesses, including building, testing, and evaluating.
- Purchase/management: Power Platform admin center, via pay-as-you-go (linked to an Azure subscription; pay monthly for actual use) or one-year prepaid Copilot Credit packs.
- Monitor per-agent consumption on the agent's Monitor page in Copilot Studio, with activity/outcome breakdown when available.
- Estimation: Copilot Credits estimator; guide: "Copilot Credits Guide".
- Overview: https://learn.microsoft.com/en-us/microsoft-copilot-studio/agents-experience/billing-credit-overview
- Buy/manage: https://learn.microsoft.com/en-us/microsoft-copilot-studio/agents-experience/billing-manage-buy-credits
- Related usage-based billing across Copilot: https://learn.microsoft.com/en-us/microsoft-365/copilot/usage-based-billing-overview-copilot-credits

### 2. Capacity model (per-message) — standard harness

- "Messages" model for standard-harness agents (the historical Copilot Studio billing). See https://learn.microsoft.com/en-us/microsoft-copilot-studio/billing-licensing
- Billing rates for pay-as-you-go / Copilot Credit pack metering of standard-harness features (prompt tiers basic/standard/premium based on the underlying model; premium text and generative AI item charges for advanced reasoning): https://learn.microsoft.com/en-us/microsoft-copilot-studio/requirements-messages-management

### Licensing

- Authoritative source: the current "Microsoft Copilot Studio Licensing Guide" PDF (published monthly-ish, e.g., April/June/August 2026 editions) — search for the latest edition. Covers purchase channels (MOSP, EA, MPSA, EAS, EES), pay-as-you-go Copilot Credit meter, and base/license requirements.
- Do not quote exact per-message or per-credit prices from memory: they change with licensing guide editions.

## Compliance disclaimers

From the official docs: Copilot Studio is not a medical device and not a substitute for professional medical advice; it does not support emergency calls. Any agent you create is your own product/service, separate from Microsoft Copilot Studio; you are solely responsible for its design, development, implementation, warnings, and disclaimers.
