# Visual Studio Code tooling: Copilot Studio extension, Power Platform Tools, and Dataverse MCP

Distilled from official Microsoft Learn docs and Microsoft's GitHub repos (November 2026). This file covers the three official VS Code developer surfaces for the platform:
1. The **Copilot Studio extension** (GA) — clone/edit/sync Copilot Studio agents as YAML (below).
2. The **Power Platform Tools extension** — the recommended way to install the Power Platform CLI (pac) for Dataverse, solutions, and environments (see the section near the end).
3. The **Dataverse MCP server** with GitHub Copilot in VS Code and Copilot CLI (see the last section).

## Part 1 — Copilot Studio extension for Visual Studio Code

The extension is generally available (GA). Docs:
- Overview: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-overview
- Install: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-install-configure
- Clone: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-clone-agent
- Edit: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-edit-agent-components
- Sync: https://learn.microsoft.com/en-us/microsoft-copilot-studio/visual-studio-code-extension-synchronization
- Repo: https://github.com/microsoft/vscode-copilotstudio
- Marketplace: https://marketplace.visualstudio.com/items?itemName=ms-CopilotStudio.vscode-copilotstudio

## What it is and why

The extension brings Copilot Studio agent authoring (standard harness) into VS Code: clone cloud agents to local YAML, edit with IntelliSense and validation, sync changes back, and use Git/PR workflows. Treat agents as first-class software artifacts: version them, review changes, promote across environments.

Key capabilities: agent cloning, YAML editing (IntelliSense), component management (knowledge sources, files, tools, topics, triggers, Azure Bot Service skills), sync (preview/get/apply), and creating/updating agents in a Dataverse environment.

Typical use cases: IDE-based agent development instead of the web UI; large agents (dozens of topics/tools) where text search and fast navigation beat web navigation; team collaboration via Git with pull-request review; agent-driven development with GitHub Copilot or Claude Code editing the YAML.

## Setup

Prerequisites: Windows 10 1809+ / Windows 11 (x64) or macOS; VS Code 1.80+ (latest recommended); internet; Microsoft account with a Copilot Studio license, access to at least one environment, and read/write permission on target agents.

Install: Extensions pane (`Ctrl+Shift+X`), search "Copilot Studio", publisher **Microsoft**, Install, reload when prompted; or install from the Marketplace page (item `ms-CopilotStudio.vscode-copilotstudio`). Verify the Copilot Studio icon in the activity bar.

First launch: select the Copilot Studio icon → **Sign In** → **Allow** → complete Microsoft authentication (incl. MFA) in the default browser → review permissions (read/write Copilot Studio agents, access environment information, sync files to cloud) → Accept. The Agents pane then shows environment groups → environments → agents.

Troubleshooting: icon missing → reload VS Code, check the extension is installed/enabled, update VS Code, reinstall. Auth failures → clear microsoft.com browser cache/cookies, switch default browser, disable blocking browser extensions, check firewall/proxy. Marketplace search empty → check org restrictions on marketplace access. Uninstalling the extension does NOT delete locally cloned agent files.

## Clone an agent

Choose a local workspace folder with disk space (a Git-tracked location is ideal; spaces in paths supported but avoid if possible). Cloning downloads the full agent definition, typically in 10–30 seconds.

Cloned structure:

```
my-agent/
├── actions/                  # Connector actions (*.mcs.yml)
├── knowledge/files/          # Knowledge sources (source YAMLs)
├── topics/                   # Conversation topics (*.mcs.yaml, e.g., greeting, help, escalate)
├── workflows/                # Agent tools/actions (GetItems/ = metadata.yaml + workflow.json)
├── trigger/                  # Event triggers (e.g., welcometrigger.mcs.yaml)
├── agent.mcs.yaml            # Main agent definition
├── icon.png                  # Agent icon (test panel & channels)
├── settings.mcs.yml          # Agent configuration settings
└── connectionreferences.mcs.yml  # Connection references for connectors/actions
```

Methods:
1. **Agents pane (recommended)**: Copilot Studio icon (or `Ctrl+Shift+P` → "Copilot Studio: Focus on Agents View") → pick environment → right-click the agent → **Clone agent** → choose destination folder → wait for "Agent cloned successfully".
2. **Command palette**: `Ctrl+Shift+P` → "Copilot Studio: Clone Agent" → follow prompts (environment, agent, folder).
3. **Agent URL**: in the Copilot Studio web portal → Settings → Agent details → copy URL (`https://copilotstudio.microsoft.com/environments/{guid}/bots/{guid}`); back in VS Code select **Clone agent**; the clipboard URL is detected and shown as "(from clipboard)".

Team/lifecycle scenarios: solo dev (clone → git init → commit → apply); team (first dev pushes to shared GitHub/Azure DevOps repo; others clone the repo then run **Copilot Studio: Reattach Agent** to connect the local folder to Copilot Studio); multiple environments (recommended path is solutions + pipelines; the extension alternative is **Reattach Agent** to a different environment, then apply and test).

## Edit agent components

- IntelliSense: `Ctrl+Space` for context-aware suggestions; invalid values highlighted; `Ctrl+F` to search across the agent. Problems: `Ctrl+Shift+M` (View → Problems), red underlines in files; saved changes show in a different color.
- **Topics** are `AdaptiveDialog` YAML files. Building blocks: `OnConversationStart` triggers, `SendActivity` (text + speak for voice), `Question` nodes (entities, `alwaysPrompt`, `variable: init:Topic.X`), Power Fx conditions via `ConditionGroup` (e.g., `condition: =Topic.Continue = true`), HTTP nodes, Adaptive Cards. Example greeting:

```yaml
kind: AdaptiveDialog
beginDialog:
  kind: OnConversationStart
  id: main
  actions:
    - kind: SendActivity
      id: sendMessage_M0LuhV
      activity:
        text:
          - Hello, I'm {System.Bot.Name}. How can I help?
```

- **Tools**: prompts, workflows (Power Automate), CUA tools, custom connectors, REST APIs, MCP connectors. They live in `/actions` (with extra metadata folders like `/workflows`).
- **Triggers**: `kind: ExternalTriggerConfiguration` with `externalTriggerSource: kind: WorkflowExternalTrigger`; schedules, events, or conditional types; typically reference a workflow.
- **Knowledge files**: uploaded documents appear under Remote Knowledge Files (download manually by selecting them); new files placed in `knowledge/files` are uploaded when you apply changes.
- Conventions: kebab-case filenames with type suffixes (`create-ticket.tool.yaml`), camelCase descriptive IDs/variables (`customerEmail`, not `custEmail`), YAML comments for complex logic.

## Synchronize (Preview / Get / Apply)

Three operations via the Agent Changes pane or command palette:

| Operation | Direction | What it does | Safety |
|---|---|---|---|
| **Preview** | Cloud → Local | Shows remote changes without applying | No local changes |
| **Get** | Cloud → Local | Downloads and applies remote changes; same-component conflicts show both versions, you choose local or remote ("latest change") | Overwrites prompt/warning; confirm |
| **Apply** | Local → Cloud | Uploads local changes and immediately modifies the live agent in the environment | Blocked if remote changes weren't retrieved yet; **not** a publish |

Workflow rhythm: Preview at session start and every 30–60 minutes (or before major work, or in teams); Get after preview shows remote changes or before pushing; Apply when a feature/fix is complete, after checking: no unresolved conflicts, preview/get done, Problems pane clean, changes committed to Git, permissions in place. After Apply, test in the Copilot Studio browser test pane (start a conversation or trigger the workflow). Apply ≠ publish; publishing still happens in Copilot Studio.

## Related developer tooling

- **Copilot Studio MCP** connects VS Code and similar tools to Copilot Studio for create/test/deploy/monitor flows beyond the extension.
- **microsoft/skills-for-copilot-studio** (GitHub): downloadable skills for AI coding agents (GitHub Copilot CLI, Claude Code, etc.) to author/edit Copilot Studio agent YAML with schema validation and templates, including `copilot-studio:author`, `copilot-studio:manage`, `copilot-studio:test`, and `copilot-studio:advisor` skills. Repo: https://github.com/microsoft/skills-for-copilot-studio

## Part 2 — Power Platform Tools extension (Dataverse, solutions, environments)

Docs: https://learn.microsoft.com/en-us/power-platform/developer/howto/install-vs-code-extension ; developer tools overview: https://learn.microsoft.com/en-us/power-platform/developer/tools ; repo: https://github.com/microsoft/powerplatform-vscode ; marketplace: https://marketplace.visualstudio.com/items?itemName=microsoft-IsvExpTools.powerplatform-vscode

- Tooling to create Power Platform solutions and packages, manage Power Platform environments, and edit Power Apps Portals. It is the **recommended way to install the Power Platform CLI (pac)**; the extension upgrades automatically when new versions are released. Works on Windows, Linux, and macOS. Only VS Code is required.
- **Install**: from the Marketplace (Power Platform Tools → Install → Continue/Open → Install) or from VS Code Extensions pane (`Ctrl+Shift+X` → search "power platform tools" → Install). Previous versions can be pinned via "Install Another Version..." (clear "Ignore Updates" to resume auto-updates). For orgs that block web installs, side-load the VSIX (`Download Extension` on the Marketplace page → Extensions pane ellipsis → "Install from VSIX...").
- **CLI availability**: by default, pac commands are enabled only in the VS Code PowerShell terminal. To use pac in Windows Command Prompt (CMD) and standalone PowerShell, install the CLI as a .NET Tool or Windows MSI, or add the pac executable to the Windows PATH.
- **Authentication profile management**: the extension lets you view and manage authentication profiles (pac auth), connecting to Dataverse environments.
- Typical Dataverse/solution workflows with pac: create/audit solutions, export/import/unpack (convert solution to source-manageable files for Git and pro-dev ALM), package deployment, environment/org management.
- Companion article for Dataverse pro-code in VS Code: "Use PowerShell and Visual Studio Code with the Dataverse Web API" (https://learn.microsoft.com/en-us/power-apps/developer/data-platform/webapi/use-ps-and-vscode-web-api).

## Part 3 — Dataverse MCP with GitHub Copilot (VS Code and Copilot CLI)

Docs: https://learn.microsoft.com/en-us/power-apps/maker/data-platform/data-platform-mcp-vscode ; related: "Configure and manage the Dataverse MCP server for an environment" (admin allows the Microsoft GitHub Copilot MCP client per environment) and "Connect to Dataverse with Model Context Protocol".

- The Dataverse MCP server exposes your Dataverse environment at `{instance URL}/api/mcp` (generally available endpoint) or `/api/mcp_preview` (preview). Get the instance URL at make.powerapps.com → Settings (gear) → Session details → Instance URL (e.g., `https://contoso.crm.dynamics.com/`).
- **Prerequisites**: the Microsoft GitHub Copilot MCP client must be allowed in the environment; VS Code with the GitHub Copilot extension, or GitHub Copilot CLI.

### Connect in VS Code

1. `Ctrl+Shift+P` → **MCP: Add Server** → **HTTP or Server Sent Events**.
2. Paste the instance URL and append `/api/mcp` (e.g., `https://contoso.crm.dynamics.com/api/mcp`), press Enter. This generates the MCP server configuration.
3. Name the server (or accept default) and choose **Global** or **workspace** scope.
4. `Ctrl+Alt+I` and select agent mode; Copilot can now use Dataverse tools (query tables, metadata, and rows against your environment).

### Connect in GitHub Copilot CLI

Option 1 (manual config): edit `~/.copilot/mcp-config.json` (global) or `.mcp/copilot/mcp.json` (project):

```json
{
  "mcpServers": {
    "DataverseMcp": {
      "type": "http",
      "url": "<your org URL>/api/mcp"
    }
  }
}
```

Save and restart Copilot CLI.

Option 2 (interactive): add the Awesome Copilot marketplace and install the Dataverse plugin, which includes an `mcp-configure` skill:

```bash
copilot plugin marketplace add github/awesome-copilot
copilot plugin install dataverse@awesome-copilot
```

Then in a Copilot chat session run `/dataverse:mcp-configure` to select the environment and choose between the GA (`/api/mcp`) and preview (`/api/mcp_preview`) endpoints.

## VS Code tooling comparison

| Need | Use |
|---|---|
| Author Copilot Studio agents as code (topics, tools, triggers), sync to cloud | Copilot Studio extension (Part 1) |
| Solution/pac-based Dataverse ALM, pack/unpack, auth profiles, portals | Power Platform Tools extension (Part 2) |
| Natural-language querying/acting on Dataverse data from the editor | Dataverse MCP + GitHub Copilot (Part 3) |
| Dataverse Web API scripts in the editor | PowerShell extension / REST client in VS Code |
