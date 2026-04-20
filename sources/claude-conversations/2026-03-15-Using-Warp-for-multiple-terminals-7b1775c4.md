---
title: Using Warp for multiple terminals
created: 2026-03-15T15:22:41.107486Z
updated: 2026-03-15T15:35:01.495886Z
uuid: 7b1775c4-b8ac-4b6d-9f0b-51164896b3fb
source: claude-conversation
type: source
message_count: 24
---

# Using Warp for multiple terminals

## Phelipe

how to use warp for multiples terminal claude

---

## Claude

Warp is a modern terminal application that supports multiple terminal sessions in several ways. Here's how to work with multiple terminals in Warp:

**Tabs** — Use `Cmd+T` (Mac) or `Ctrl+Shift+T` (Linux) to open new tabs. Switch between them with `Cmd+1`, `Cmd+2`, etc.

**Split Panes** — This is probably what you're after for running multiple Claude Code sessions side by side. Use `Cmd+D` for a vertical split and `Cmd+Shift+D` for a horizontal split. Navigate between panes with `Cmd+Option+Arrow`.

**Windows** — `Cmd+N` opens an entirely new Warp window.

For running **multiple Claude Code instances** specifically, split panes work great — you can have one pane per OSA workstream (say, one for the CRM artifact, one for Loud Hawk content skills, one for Growth Marketing HQ) and see them all at once.

A couple of practical tips: Warp lets you rename tabs (right-click the tab), which helps when you're juggling multiple Claude Code sessions across different project directories. And each pane runs its own independent shell, so you can `cd` into different project folders and run `claude` in each one without conflict.

Want me to dig into anything more specific — like Warp configuration, or how to organize multiple Claude Code workspaces effectively?

---

## Phelipe

yes. the pricing. i have claude max 20x. i need to pay them as well?

---

## Claude

Good question. Let me look up the current details on Claude Code pricing and how it works with your Max subscription.
```
This block is not supported on your current device yet.
```

Good news, Phelipe — **your Max 20x plan ($200/month) already includes full Claude Code access**. There's no separate charge.

Both the $100 and $200 Max tiers include full access to Claude Code, and Max 20x provides 20x the Pro usage limits, maximum priority access, and full Claude Code capabilities.

So you can install Warp, open as many split panes as you want, run `claude` in each one, and it all draws from your existing Max 20x allocation. No API billing, no extra cost.

The only thing to keep in mind is that Claude Code calls are heavier than regular chat — they include large system instructions, full file contexts, and often multiple steps per interaction, so running multiple concurrent sessions will burn through your weekly usage faster. One heavy user tracked 10 billion tokens across 8 months and found the API equivalent would have been $15,000 versus $800 on Max — so the subscription is a massive value advantage for heavy Claude Code usage.

Bottom line: you're already covered. Just install Claude Code (`npm install -g @anthropic-ai/claude-code`), authenticate with your Anthropic account, and go.

---

## Phelipe

but if i stack with warp to have multiple claude codes. i have to pay them, too?

---

## Claude

No, Warp itself is free for individual use. You don't need to pay Warp anything.

Warp is a terminal app — it's just a fancy replacement for the default Terminal or iTerm. When you open multiple panes in Warp and run `claude` in each one, every session authenticates against your Anthropic Max 20x account. Warp is just the window; Anthropic is the engine.

So your total cost stays at $200/month. Warp charges $0. Whether you run one Claude Code session or five side by side, it's all drawing from the same Max 20x usage pool.

The only thing Warp charges for is their Team plan (for businesses that want shared workflows, session sharing, etc.), which you don't need as a solo operator.

---

## Phelipe

teach me to setup

---

## Claude

Let me check what OS you're running Claude Code on so I give you the right steps.
```
This block is not supported on your current device yet.
```

---

## Phelipe

Q: What are you running on?
A: Mac

---

## Claude

Here's the full setup, step by step.

**1. Install Warp**

Download from [warp.dev](https://warp.dev) and drag it to your Applications folder. Open it and create a free account (or sign in with Google/GitHub).

**2. Install Claude Code (if you haven't already)**

Open Warp and run:

```bash
npm install -g @anthropic-ai/claude-code
```

If you don't have Node.js installed yet, install it first with:

```bash
brew install node
```

**3. Authenticate Claude Code**

Run `claude` in Warp. The first time, it'll open a browser window to authenticate with your Anthropic account (your Max 20x). Once you log in, you're set — the auth persists.

**4. Use multiple panes**

This is where it gets good:

- `Cmd + D` — split vertically (side by side)
- `Cmd + Shift + D` — split horizontally (stacked)
- `Cmd + Option + Arrow` — move between panes
- `Cmd + W` — close a pane

So your workflow would look like: open Warp, hit `Cmd+D` a couple times, then `cd` into different project folders in each pane and run `claude` in each one.

**5. Rename your tabs**

Right-click any tab to rename it. I'd label them by workstream — "OSA Connect," "Loud Hawk," "Growth HQ" — so you always know which is which.

That's it. Want me to walk through anything else, like setting up your CLAUDE.md files for each project so each session has the right context automatically?

---

## Claude

Go with **Classic terminal**. 

The "Agent driven development" option is Warp's own built-in AI agent, which is a separate thing from Claude Code. You don't need it — you'll be running Claude Code directly in the terminal yourself. Classic terminal gives you a clean, fast shell without Warp's AI layer getting in the way.

Hit that, then Next, and keep going through the setup. Let me know when you're at the terminal prompt and I'll walk you through the rest.

---

## Claude

You're in. Click "Don't show again" on that tips panel to clear it out, then click into the command line at the bottom (where it says "Run commands") and type:

```
node --version
```

This checks if Node.js is installed. Send me what it says and we'll go from there.

---

## Claude

Node v22.16.0 — you're good. Now install Claude Code. Type:

```
npm install -g @anthropic-ai/claude-code
```

Once that finishes, type `claude` and hit enter. It'll open your browser to authenticate with your Anthropic account. Show me what you get.

---

## Claude

Classic permissions error. Warp is already suggesting the fix at the bottom. Run:

```
sudo npm install -g @anthropic-ai/claude-code
```

It'll ask for your Mac password (the one you use to log in). Type it — nothing will show on screen as you type, that's normal — then hit enter.

---

## Claude

Installed. Now type:

```
claude
```

It should launch and open your browser to log in with your Anthropic account. Show me what comes up.

---

## Claude

You're live. Claude Code v2.1.76, authenticated with your account. 

One thing I notice — it says "Sonnet 4.6 · Claude Pro." Your Max 20x should give you access to Opus 4.6 too. You can switch models inside Claude Code by typing `/model` and selecting Opus when you need the heavier reasoning.

Now to split panes and run multiple sessions:

1. Hit `Cmd + D` — you'll get a second pane side by side
2. In the new pane, `cd` into a project folder (e.g. `cd ~/Projects/osa-connect`) and run `claude`
3. Split again with `Cmd + D` or `Cmd + Shift + D` for a horizontal split

Each pane runs its own independent Claude Code session. You're all set.

---

## Claude

That's it. Left pane has Claude Code running, right pane is a fresh terminal ready for another session. Type `claude` in that right pane and you'll have two instances running side by side.

You can keep splitting — `Cmd+D` for more vertical splits, `Cmd+Shift+D` for horizontal. Use `Cmd+Option+Arrow` to jump between panes.

You're fully set up. Zero extra cost, all running off your Max 20x.

---
