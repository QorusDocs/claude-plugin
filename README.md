# QorusDocs plugin for Claude

Connects Claude to your QorusDocs hub — pursuits, Smart Layouts (bios, experience) and content sources — and adds a **Create Pursuit** skill that guides a pursuit from set-up, through your hub's Assignments, to a drafted and delivered document.

For installation, permissions and usage, see [Set up and use the QorusDocs plugin for Claude](docs/qorusdocs-connector-for-claude.md).

## Install (Claude Code)

```
/plugin marketplace add QorusDocs/claude-plugin
/plugin install qorusdocs@qorusdocs
```

On first use, run `/mcp` and sign in to QorusDocs when the browser opens. Claude only sees what your QorusDocs account can see.

## What's included

| Component | Purpose |
|---|---|
| `qorusdocs` MCP server | `https://agent-mcp.qorushub.com` — OAuth sign-in, no API key |
| `create-pursuit` skill | Guides a pursuit through its pipeline: create, file documents, run Assignments, review selection, draft, deliver, close |

## Layout

```
.claude-plugin/marketplace.json     marketplace listing
docs/                               installation and usage guide
plugins/qorusdocs/
  .claude-plugin/plugin.json        plugin manifest
  .mcp.json                         MCP server connection
  skills/create-pursuit/            the skill
```
