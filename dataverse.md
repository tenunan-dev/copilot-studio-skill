# Microsoft Dataverse

Distilled from Microsoft Learn (November 2026). Overview: https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-intro

## What it is

Dataverse is the secure, cloud-based data platform that stores and manages data used by business applications across Power Platform (Power Apps, Power Automate, Copilot Studio, Power BI, Power Pages) and Dynamics 365. Data lives in **tables**; metadata and data are both in the cloud. Dataverse for Teams (lightweight, included with Teams) is deprecated in favor of full environments.

## Structure and terminology

- **Table** = set of rows (formerly records) and columns (formerly fields/attributes). Columns are typed (name, age, lookup, choice, currency, file, etc.).
- Terminology migration (Nov 2020, API names unchanged): entity→table, field/attribute→column, record→row, option set/picklist→choice, two options→Yes/No. Web API messages keep legacy names (e.g., `CreateEntityRequest`).
- **Standard (out-of-box) tables** come with a Dataverse environment: Account, Contact, Business Unit, User, Task, Activity tables, etc. Referenced in docs as the "entity reference"/table reference.
- **Custom tables** capture organization-specific concepts; created in the maker portal (Tables). Optionally enable for business process flows, feedback, notes, and activities.
- **Relationships**: 1:N, N:1, N:N; rich metadata is surfaced directly in Power Apps.
- **Choices (global option sets)**: reusable value sets.
- **Views, forms, charts, dashboards**: model-driven UI artifacts defined over tables.
- **Columns of note**: lookup, calculated (Power Fx formula columns), rollup, file/image, Multiline Text, and (preview for Copilot Studio knowledge) File columns for unstructured reasoning.

## Server-side logic and validation

Defined once on the table, applied no matter which app or flow touches the data:
- **Business rules**: validate across columns/tables; show warning/error messages at form level, no code.
- **Business process flows**: guide users through consistent stages/steps (model-driven apps only).
- **Workflows**: classic automation without interaction.
- **Rules/automation via Power Automate**: Dataverse triggers (create/update/delete message) and actions.
- **Code-based logic**: plug-ins, Azure Functions/ Service endpoints, JavaScript, webhooks for pro-developer extension; business logic with code applies to advanced scenarios.

## Security model

Layered: **business units** + **security roles** (role-based privileges: create/read/write/delete/append/assign/share at table level) + **row-level** (user/team ownership, hierarchies, access teams) + **column/field-level security profiles** (mask sensitive columns). Users see data only when granted access; sharing honors Dataverse roles from within Power Apps. Copilot Studio agents honor the maker/user's Dataverse permissions and org DLP policies. Admin doc: "Security in Dataverse in the Power Platform admin guide".

## Getting data in

- **Power Query** import from hundreds of online/on-premises sources with transformation, then scheduled refresh for some sources.
- **One-time import**: Excel/CSV import and export.
- **Excel add-in** for in-Excel productivity editing of Dataverse data.
- **Synapse Link / export to Azure**: export to data lake for analytics.
- **Virtual tables**: integrate external data (SQL, API) without physically copying it into Dataverse.
- **Dynamics 365**: shares the same Dataverse, so build Power Apps directly against D365 business data, no integration needed (Finance and Operations apps require the Data Integrator).

## Developers

Docs: "Dataverse Developer Overview" (https://learn.microsoft.com/en-us/power-apps/developer/data-platform/overview)
- **Web API** (REST, OData v4) for CRUD and metadata operations; org service (.NET) alternative.
- Create tables, columns, business logic programmatically; manage Copilot Studio agents programmatically too (agent config tables + APIs).
- **Solutions** transport tables and customizations; plug-ins registered on messages; custom actions; low-code plug-ins (Power Fx).
- Power Platform CLI (pac) for code-first ALM; Dataverse connector for flows.

## Capacity and admin

- Capacity pools per tenant: database, file, log; per-environment database minimums; add-ons and pay-as-you-go supported.
- Sandbox environments support copy/reset for dev/test; managed environments add governance at scale.
- Analytics in Power Platform admin center (Dataverse analytics).

## Copilot Studio touchpoints

- Dataverse tables as a knowledge source (structured fields; preview unstructured reasoning over Multiline Text/File columns).
- Dataverse connectors as agent tools (read/write rows, perform actions).
- **Dataverse-oriented triggers** (row created/updated) available for flows used as agent tools.
- Agents stored in environments; programmatically creatable/publishable via Dataverse APIs and solutions.

## VS Code and MCP touchpoints

- **Power Platform Tools extension** installs the Power Platform CLI (pac) in VS Code: auth profiles, solution pack/unpack/import/export, package deployment, environment management (https://learn.microsoft.com/en-us/power-platform/developer/howto/install-vs-code-extension).
- **Dataverse MCP server**: expose the environment at `{instance URL}/api/mcp` (GA endpoint) or `/api/mcp_preview` and connect GitHub Copilot in VS Code (Command Palette → MCP: Add Server → HTTP/SSE) or Copilot CLI (config file or `dataverse@awesome-copilot` plugin with `/dataverse:mcp-configure`); the Microsoft GitHub Copilot MCP client must be allowed in the environment (https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-mcp-vscode).
- Dataverse Web API scripting in VS Code: PowerShell extension guide at https://learn.microsoft.com/en-us/power-apps/developer/data-platform/webapi/use-ps-and-vscode-web-api
