# Power Platform Overview, Administration, and Ecosystem

Distilled from Microsoft Learn (November 2026). Docs hub: https://learn.microsoft.com/en-us/power-platform/

## What Power Platform is

A low-code/no-code platform to "build agents, apps, automations, analytics, and websites". Five products on one shared foundation:

| Product | What it does | Best for |
|---|---|---|
| Copilot Studio | Agents, workflows, agent flows | AI assistants, automation with reasoning |
| Power Apps | Canvas, model-driven, and AI-generated apps | Custom business apps |
| Power Automate | Cloud flows, desktop flows (RPA), generative actions | Process automation |
| Power BI | Business intelligence and analytics | Reports, dashboards, data viz |
| Power Pages | Low-code external websites | Portals backed by Dataverse |

Shared capabilities:
- **Microsoft Dataverse** — the data platform (see `dataverse.md`).
- **Connectors** — prebuilt connectors to 1000+ services (SharePoint, SQL Server, Dynamics 365, Office 365, Salesforce, Twitter/X, and more) plus custom connectors for REST APIs. Used by all products, incl. Copilot Studio tools/knowledge.
- **AI Builder** — prebuilt and custom AI models (document processing, invoice processing, object detection, prediction, sentiment analysis, category classification, entity extraction) usable in Power Apps and Power Automate. Docs: https://learn.microsoft.com/en-us/ai-builder/overview
- **Power Fx** — the open-source, Excel-like low-code formula language; spans no-code to "pro-code" with no rewriting cliffs. Used in canvas apps, Dataverse formula columns, and increasingly elsewhere. Docs: https://learn.microsoft.com/en-us/power-platform/power-fx/overview ; GitHub: https://github.com/microsoft/Power-Fx
- **Copilot and generative AI** — Copilot assistance across all makers' experiences.

## Power Platform admin center (admin.powerplatform.microsoft.com)

Central administration: environments (create/manage), Dataverse analytics, security and governance, capacity, DLP policies, real-time self-help recommendations and support. Docs: https://learn.microsoft.com/en-us/power-platform/admin/admin-documentation

### Environments

Docs: https://learn.microsoft.com/en-us/power-platform/admin/environments-overview

- Containers for apps, flows, data (Dataverse), and agents; each tenant gets a **default environment**. Types: **Production**, **Sandbox** (for dev/test, supports copy/reset), **Developer** (for the Power Apps Developer Plan), **Trial**, and managed environment variants.
- Deprecated: **Dataverse for Teams environments** (lightweight with Teams) and **unmanaged developer environments**; new guidance is to use sandbox/managed developer environments.
- **Managed environments**: a suite of premium admin capabilities (group policies, sharing limits, usage insights, DLP enforcement at scale, solution checker enforcement) usable with any environment type. Docs: https://learn.microsoft.com/en-us/power-platform/admin/managed-environment-overview
- Environment groups for bulk governance.
- Data policies (DLP) classify connectors as business/non-business and can block connectors per environment; this also restricts Copilot Studio agent tools and knowledge sources.

### ALM (Application Lifecycle Management)

Docs: https://learn.microsoft.com/en-us/power-platform/alm/basics-alm

- **Solutions** are the ALM mechanism: bundles of tables, apps, flows, agents, and components. **Unmanaged** = development ("your source"); **managed** = deployed to test/production, layered customization supported.
- Move solutions between environments via export/import or **Power Platform pipelines** (automated deployment in host environments; admins see run history). Docs: https://learn.microsoft.com/en-us/power-platform/alm/admin-deployment-hub
- Avoid installing unnecessary Dynamics 365 apps in environments to prevent dependency complications.
- Source control integration (Power Platform CLI / pac, GitHub/Azure DevOps export of solution source) for pro-dev ALM.

## Power Pages

Low-code, secure, external-facing websites: design, configure, and publish data-driven sites that work across browsers and devices; authentication options (Entra ID, Microsoft account, local, B2C); backed by Dataverse; pro-developer extensibility with VS Code and Liquid templates. Docs: https://learn.microsoft.com/en-us/power-pages/introduction

## Power BI (in-scope basics)

The analytics product of the family; semantic models, reports, dashboards; integrates natively with Dataverse and Fabric; Microsoft Fabric is its SaaS analytics successor for enterprise-scale. Copilot Studio agents can ground in Fabric semantic models via Fabric IQ (preview). Docs: https://learn.microsoft.com/en-us/power-bi/fundamentals/

## Licensing

Overview: https://learn.microsoft.com/en-us/power-platform/admin/pricing-billing-skus ; Licensing Guide (October 2026 edition PDF): https://cdn-dynmedia-1.microsoft.com/is/content/microsoftcorp/microsoft/bade/documents/products-and-services/en-us/bizapps/Power-Platform-Licensing-Guide.pdf

Key points (verify against the current guide for prices):
- **Power Apps**: per user plans for apps; per app SKU no longer available to new customers through some purchasing channels effective January 2, 2026 (existing customers keep entitlement during agreement term).
- **Power Automate**: per user and per flow plans; premium connectors require premium plans.
- **Power Platform capacity** is pooled: Dataverse database (per environment minimums), file, and log capacity; self-serve disaster recovery requires pay-as-you-go.
- **Pay-as-you-go**: link an environment to an Azure subscription; billed monthly on actual usage (incl. Copilot Credits meter for Copilot Studio).
- **Copilot Studio**: standard harness uses capacity/per-message model; Microsoft Copilot and Customer Conversation harnesses use Copilot Credits (see `governance-billing.md`).
- M365-included lightweight capabilities (e.g., "Power Apps for Microsoft 365") allow limited apps on M365 data; premium use of Dataverse/connectors needs paid plans.
- Dynamics 365 licenses bundle Power Platform entitlements (use rights) up to limits.

## Architecture and guidance

- Architecture Center: reference architectures and established patterns for Power Platform and Copilot Studio (https://learn.microsoft.com/en-us/power-platform/architecture/index)
- Well-Architected Framework for Power Platform workloads.
- CoE (Center of Excellence) Starter Kit for adoption/governance.
- Training and certifications: Power Platform Fundamentals (PL-900), Power App Maker/Functional Consultant (PL-100/PL-200), Solution Architect (PL-400/PL-600).

## How the pieces share data

All products sit on Dataverse: Power Apps writes/reads tables; Power Automate triggers include Dataverse rows; Copilot Studio agents can use Dataverse tables as knowledge and store agent configuration; Dynamics 365 stores its data in Dataverse (build Power Apps directly against D365 business data without integration; Finance and Operations apps need Data Integrator). Data can be integrated from many sources into Dataverse via Power Query, one-time Excel/CSV import, or scheduled sync.
