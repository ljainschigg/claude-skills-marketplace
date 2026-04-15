# example-mcp-node-skill

Demonstrates a skill backed by a Node.js MCP server. When invoked, it calls a running Node.js process via the Model Context Protocol and returns a figlet ASCII art greeting. Proof of life for the Node.js MCP plugin pattern.

---

## Prerequisites

[Node.js and npm](https://nodejs.org/) must be installed. Dependencies are installed automatically into a persistent data directory on first run.

---

## Install

If you haven't added the marketplace yet:

```
/plugin marketplace add https://jjainschigg-r.github.io/claude-skills-marketplace/marketplace.json
```

Then install the skill:

```
/plugin install example-mcp-node-skill@mirantis-skills
```

## Use

```
/example-mcp-node-skill
```

Claude will call the `hello_node` MCP tool and return a figlet ASCII art greeting.

---

## How it works

On install, a Node.js MCP server starts alongside Claude Code. The server declares a `hello_node` tool. The skill's only job is to call that tool — all the Node.js logic lives in the server, not the prompt.

A wrapper script (`run-server.sh`) handles dependency installation on first run, storing `node_modules` in `${CLAUDE_PLUGIN_DATA}` so they survive plugin updates. The server script is always copied fresh from the plugin on startup, so code changes take effect on reinstall.

---

## Details

| | |
|---|---|
| **Version** | 1.0.0 |
| **Runtime** | Node.js via `npm` |
| **External dependency** | `figlet` |
| **Maintained by** | Mirantis |
