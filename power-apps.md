# Power Apps

Distilled from Microsoft Learn (November 2026). Overview: https://learn.microsoft.com/en-us/power-apps/powerapps-overview ; maker portal: https://make.powerapps.com

## What it is

A suite of apps, services, connectors, and a data platform for rapidly building custom business apps without writing code (with pro-code extensibility). Apps connect to Dataverse or to online/on-premises sources (SharePoint, Microsoft 365, Dynamics 365, SQL Server, and many more). Apps run responsively in browsers and on mobile (Power Apps mobile for phone/tablet). Dynamics 365 apps run on the same Dataverse platform, so Power Apps can build directly against D365 business data with no integration.

## What makers can build

| Type | What it is | Design experience | Best for |
|---|---|---|---|
| **Canvas app** | Pixel-level-controlled app on a blank design surface; drag-and-drop controls, like building a slide deck | Power Apps Studio | Task/image-heavy apps, custom UX, any data source |
| **Model-driven app** | Data-first app generated from Dataverse (and dynamics) tables; layout largely determined by components you add (forms, views, dashboards, sitemap) | App designer | Complex data/business processes, consistent UX |
| **Plans** | Copilot-first development: describe your business use case in natural language (add images like process flows or screenshots of legacy apps) and it generates a complete Power Platform solution | Plans in Power Apps | Fast full-solution generation, automation included |
| **New Power Apps experience (preview)** | AI-native app creation | New maker experience | Simpler app/workflow creation without advanced coding |

Channels/behaviors: model-driven apps require Dataverse; canvas apps can use hundreds of sources or Dataverse for full logic/security benefits.

## Roles

- **Makers**: build at https://make.powerapps.com (default environment initially); Developer Plan available for a free developer environment with Dataverse (now used as managed developer environments; unmanaged developer environments deprecated).
- **Users**: run apps in browser or Power Apps mobile; can request a license from within an app.
- **Admins**: manage via Power Platform admin center.
- **Developers**: extend with code — Azure Functions and plug-ins (server-side), JavaScript (client-side), web hooks, virtual tables (external data surfaced as Dataverse tables), custom connectors, website embedding.

## Key maker concepts

- **Controls**: galleries (data rows), forms (create/edit/view), screens, formulas.
- **Power Fx** everywhere in canvas apps (Excel-like formulas; e.g., Filter, Patch, Navigate, OnSelect).
- **Copilot in Power Apps**: describe the app you want and AI designs it; make edits, add automation, and write code with Copilot.
- **Model-driven components**: forms, views, charts, dashboards, business process flows (model-driven only), sitemap.
- **Sharing**: share canvas apps with Entra groups; model-driven security is governed by Dataverse security roles (see `dataverse.md`).
- **Solutions**: apps live in environments; add canvas apps and cloud flows to solutions for ALM (managed/unmanaged, pipelines).
- **Offline and mobile**: Power Apps mobile supports offline-capable canvas apps and model-driven apps.

## Licensing checkpoints

- A license is needed to *play* apps (30-day trial available). Per user plans; per app SKU unavailable to new customers in some channels since January 2, 2026.
- Model-driven apps and Dataverse use = premium Power Apps plan (or D365 license with use rights).
- US Government plans (GCC, GCC High, DoD) exist with their own compliance scope (FedRAMP High, DISA IL2, CJI).

## Common patterns and good practice

- Start from data: generate a canvas app from an Excel workbook, SharePoint list, or Dataverse table, then customize ("Generate an app from data").
- Plan first: use "Planning a Power Apps project" guidance for multi-maker projects.
- Prefer Dataverse over raw sources when you need row-level security, business logic, reuse across apps/flows/agents.
- Use environment strategy (dev → test → prod) and solutions from day one; avoid customizations outside solutions in production.
- Use App Checker / Solution Checker for best-practice validation before deploy.
