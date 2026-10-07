# QorusDocs plugin for Claude

Connects Claude to your QorusDocs hub — pursuits, Smart Layouts (bios, experience) and content sources — and adds a **Capability Statement** skill that walks a pursuit from set-up to a delivered PDF.

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
| `capability-statement` skill | Guides a capability statement through the pursuit pipeline: create, file documents, run Assignments, review selection, draft, deliver |

## Layout

```
.claude-plugin/marketplace.json     marketplace listing
plugins/qorusdocs/
  .claude-plugin/plugin.json        plugin manifest
  .mcp.json                         MCP server connection
  skills/capability-statement/      the skill
```
