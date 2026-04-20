---
title: Figma and Claude code integration
created: 2026-03-08T23:12:01.759643Z
updated: 2026-03-08T23:12:32.143653Z
uuid: dacd58e4-d99d-4d47-b583-84ecc4f63e09
source: claude-conversation
type: source
message_count: 2
---

# Figma and Claude code integration

## Phelipe

how to use figma and claude code

---

## Claude

```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's a comprehensive overview of how Figma and Claude Code work together:

---

## Figma + Claude Code Integration

The integration works through **Figma's MCP (Model Context Protocol) Server**, which acts as a bridge between your Figma designs and Claude Code running in your terminal.

### What You Can Do

There are two main directions to the workflow:

**Figma → Code:** Select a Figma frame and turn it into code — great for product teams building new flows or iterating on app features. You can pull in variables, components, and layout data directly into your IDE.

**Code → Figma:** You can capture live UI from a browser (production, staging, or localhost) and convert it into editable Figma frames — letting you move from a working interface back into the design canvas without losing context.

---

### Setup: The Easiest Method (Claude Code Plugin)

The recommended way to set up the Figma MCP server in Claude Code is by installing the Figma plugin, which includes MCP server settings as well as Agent Skills for common workflows. Run the following command:

```
claude plugin install figma@claude-plugins-official
```

### Setup: Manual (Desktop App Method)

1. Open the Figma **desktop app** preferences and turn on "Dev Mode MCP Server." It runs locally at `http://127.0.0.1:3845/sse`.
2. Connect Claude Code by running:
   ```
   claude mcp add --transport sse figma-dev-mode-mcp-server http://127.0.0.1:3845/sse
   ```
3. Start working — reference Figma designs by selecting frames in the desktop app, or paste design links into Claude Code prompts.

**Requirements:** Figma desktop app (not the browser version), a Figma Dev or Full seat, and Claude Code installed via npm.

---

### How to Use It Day-to-Day

**Design to code:** Copy the link to a frame or layer in Figma from the browser address bar, paste the URL into your MCP client (Claude Code), and prompt it to help you implement the design.

**Code to Figma:** Prompt Claude Code: *"Start a local server for my app and capture the UI in a new Figma file."* Follow the steps it provides — Claude will open a browser window where you can capture pages, elements, and states, then send them back to Figma.

---

### What Claude Code Can Do with Figma Designs

The MCP server doesn't just pass screenshots — it reads components, variables, styles, and layout structure so Claude understands your design system semantically. Common tasks include:

- Converting Figma frames to React/Vue components
- Extracting design tokens (colors, typography, spacing) as CSS variables
- Building responsive layouts from Figma specs
- Keeping component libraries in sync via **Code Connect**

---

### Key Limitation to Know

Rate limits apply: users on the Starter plan or with View/Collab seats are limited to up to **6 tool calls per month**. Users with a Dev or Full seat on paid plans get per-minute rate limits aligned with Figma's REST API tier.

For the full docs, Figma's official guide is at [help.figma.com](https://help.figma.com/hc/en-us/articles/32132100833559-Guide-to-the-Figma-MCP-server) and Anthropic's Claude Code docs are at [docs.claude.com](https://docs.claude.com/en/docs/claude-code/overview).

---
