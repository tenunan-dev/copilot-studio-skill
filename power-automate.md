# Power Automate

Distilled from Microsoft Learn (November 2026). Overview: https://learn.microsoft.com/en-us/power-automate/flow-types

## What it is

Power Automate streamlines repetitive, manual business processes. Workflows are built by drag-and-drop with many prebuilt connectors, with little or no coding. It is the automation product of Power Platform. Requires Microsoft work or school email for the web service; included with some Microsoft 365 plans (standard connectors), premium plans unlock premium connectors and RPA.

## Types of flows

| Type | Trigger | Best for | Docs |
|---|---|---|---|
| **Cloud flow: automated** | Event in a connected service (e.g., new email, Dataverse row created, SharePoint item added) | Event-driven automation | https://learn.microsoft.com/en-us/power-automate/overview-cloud |
| **Cloud flow: instant** | User manually runs it (button, from app or Teams) | One-off approvals/refreshes | |
| **Cloud flow: scheduled** | Time-based schedule (recurrence, cron-like) | Recurring jobs | |
| **Desktop flow** (RPA) | Triggered by cloud flow, schedule, or user; runs on a Windows machine with Power Automate for desktop | Automating legacy/on-prem apps and web UIs via UI recordings and actions, attended or unattended | https://learn.microsoft.com/en-us/power-automate/desktop-flows/introduction ; trigger from cloud: https://learn.microsoft.com/en-us/power-automate/desktop-flows/trigger-desktop-flows |
| **Generative actions (preview)** | Inside a flow: specify only the *intent* of the action and AI chooses the right set of actions in the right order based on input, context, and intent | Adaptive, AI-driven steps | |

Approval flows (start-and-wait-approval) with Microsoft Approvals unify human-in-the-loop across Teams and email; business process flows are Dataverse's own concept (model-driven apps only).

## Copilot and AI in Power Automate

- Copilot in Power Automate helps describe a flow and get it built, edit with natural language.
- Generative actions (preview) let the flow reason about intent and synthesize a plan of actions instead of hard-coding steps.
- AI Builder adds AI steps to flows (document processing, sentiment, prediction, extraction).

## Power Apps and Copilot Studio relationships

- Your Power Automate license gives rights to create/manage flows from within Power Apps (Flows nav / pane in Power Apps Studio).
- **Copilot Studio agent flows** are a sibling: same Power Automate-like authoring, native to Copilot Studio, runnable standalone or attached to agents as tools; they differ from Power Automate cloud flows (which are also usable as agent tools via connectors).
- Cloud flows vs agent flows rule of thumb: cloud flows for classic connector-based automation on the Power Automate service; agent flows for automation that runs within (or hands back to) a Copilot Studio agent, with agent nodes, prompt nodes, and human review steps.

## Key maker concepts

- Triggers (first step) and actions (subsequent steps) from connectors; dynamic content from previous steps.
- Conditions, loops (apply to each), switch, scope/terminate for error handling (configure run-after), expressions (Workflow Definition Language functions).
- Templates library for common scenarios.
- Process Mining (Power Automate Process Mining) analyzes and visualizes actual processes from system logs to find automation opportunities.
- Approvals; Adaptive Cards in Teams; Robotic process automation for attended/unattended scenarios.

## Governance notes

- Desktop flow governance controls (registry keys) influence storage location/behavior of recordings.
- DLP data policies classify connectors (business/non-business) and can block connectors per environment, restricting what flows (and Copilot Studio agents) may call.
- Flow limits and throttling per plan/license; use solutions to move flows through environments.

## Determining which automation to use

Decision aid from the docs ("Determine which automation method (flow type) to use"):
- Attended/unattended desktop automation → desktop flows.
- Event/button/timed cloud automation → cloud flows (automated/instant/scheduled).
- Goal-based with AI-chosen steps → generative actions (preview) or Copilot Studio agent flows/workflows.
- Full agent conversations with reasoning and channels → build in Copilot Studio instead.
