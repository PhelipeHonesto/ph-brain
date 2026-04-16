---
title: Fleet statistics overview
created: 2026-04-13T03:12:19.447017Z
updated: 2026-04-13T03:12:38.225409Z
uuid: 0572f0c0-4824-499a-9731-d0fec2a3de7b
source: claude-conversation
type: source
message_count: 2
---

# Fleet statistics overview

*Summary: **Conversation Overview**

The person requested fleet statistics using a Dumont Intelligence integration. Claude attempted to retrieve the data by calling the `dumont-intelligence:fleet_stats` tool, but the tool returned an infrastructure error indicating that a required `/data` directory was unavailable in the current environment. Claude clarified that the issue was on Dumont's end rather than the user's, and offered to run diagnostic tools (`data_health` or `feed_health`) to check whether the underlying pipeline was operational. The conversation ended without a response from the person.

**Tool Knowledge**

The `dumont-intelligence:fleet_stats` tool failed with an infrastructure error tied to a missing `/data` directory, suggesting an environment configuration issue on Dumont's side rather than a query syntax problem. When this error occurs, Claude suggested using `data_health` or `feed_health` as diagnostic alternatives to assess pipeline availability before retrying `fleet_stats`. No successful query syntax was established in this session.*

## Phelipe

Show me fleet stats

---

## Claude

Let me search for the fleet stats tool.
```
This block is not supported on your current device yet.
```

Let me call fleet_stats.
```
This block is not supported on your current device yet.
```

Looks like the Dumont feed is throwing an infrastructure error on their end — the `/data` directory it needs isn't available in this environment right now. Nothing on your side to fix.

Want me to try `data_health` or `feed_health` to see if the pipeline itself is alive?

---
