---
title: Fleet stats current display
created: 2026-04-13T03:14:32.133896Z
updated: 2026-04-13T03:19:42.604022Z
uuid: 53920ecd-d095-4c70-b003-1bcd13d8d5df
source: claude-conversation
type: source
message_count: 8
---

# Fleet stats current display

*Summary: **Conversation Overview**

The person is working with a platform called Dumont Intelligence, which appears to be a private aviation data and business intelligence tool. The conversation focused entirely on querying live fleet and market data to support what appears to be charter sales and aircraft advisory work at a company referred to as OSA. The person asked four sequential data queries with no follow-up questions, suggesting familiarity with both the tools and the domain.

The session covered four distinct data pulls: a live fleet snapshot via fleet_stats (showing 73,088 ADS-B-tracked aircraft, 19 ghost candidates, with notable positioning at KEWR); a tail number lookup for N143QS (a NetJets-operated Bombardier Global 6000 with high utilization at 543 legs since December 2023); route intelligence for KTEB to KPBI (a high-volume, heavy/super-mid dominated corridor with strong Thursday demand spikes and clear snowbird seasonality); and recent ownership/transaction data (a bulk FAA deregistration sync event flagged as a batch artifact, with notable heavy-class aircraft including GLEX and CL60 clusters identified as potential advisory leads).

Claude consistently translated raw data into business-relevant commentary, including pricing anchors for the KTEB-KPBI route, cold-call opportunities from ghost aircraft positioning, and advisory pipeline signals from deregistration events. Domain terminology used throughout includes: ghost candidates, OSA, ADS-B, fractional ownership, super mid, heavy class, Charter Index, deregistration events, and trust structures.

**Tool Knowledge**

The dumont-intelligence MCP integration was used directly with tools including `fleet_stats` (no parameters required), `lookup_aircraft` (parameter: `tail_number`), `route_intel` (parameters: `origin` and `destination` as ICAO airport codes), and `recent_transactions` (parameter: `limit` as integer). A `tool_search` query was used before `route_intel` to locate the correct tool name, suggesting tool discovery may not always be immediate and a preliminary search step can help. The `recent_transactions` tool with `limit: 50` returned a batch sync event rather than organic activity — all 50 results shared an identical timestamp (2026-04-12 23:38:19 UTC), indicating that identical timestamps across results signal a bulk FAA registry sync rather than real-time market transactions, and results should be interpreted accordingly.*

## Phelipe

What does fleet_stats show right now?

---

## Claude

Let me search for the fleet_stats tool.
```
This block is not supported on your current device yet.
```

Now I can call fleet_stats.
```
This block is not supported on your current device yet.
```

Let me present this cleanly.Here's the live snapshot:

**ADS-B Tracked: 73,088 aircraft**
- Airborne: 65,665 (89.8%)
- Idle/Transient: 7,423
- Registry total: 314,809

**By Class (charter-relevant)**
- Turboprop: 3,182
- Super Mid: 2,247
- Light: 2,058
- Heavy: 2,055
- Midsize: 1,699

**Ghost Candidates: 19**
Top airports with ghosts: KSAN (San Diego), KMSY (New Orleans), KEWR (Newark) — each showing 1.

Notably thin ghost count right now (19 is low), which suggests most of the transient-idle fleet is either home-based or the feed is catching a quieter Sunday afternoon lull. The KEWR ghost is interesting — Newark is a pricey positioning market, could be a discount opportunity worth a cold call.

---

## Phelipe

Look up tail number N143QS

---

## Claude

Let me look up that tail number.
```
This block is not supported on your current device yet.
```

Here's the profile on **N143QS**:

**Aircraft**
- Bombardier Global 6000/6500 (GLEX)
- 2012 manufacture, heavy class
- Status: Active

**Operator**
NetJets (NETJETS SALES INC) — held in trust via Bank of Utah, with Microsoft Finance listed as a certificate holder. Typical fractional ownership structure.

**Current Position**
Airborne right now, near KBOS (Boston). Coordinates put it over western Connecticut, so likely inbound to Boston or transiting the Northeast corridor.

**Flight History**
- 543 legs logged since December 2023
- Average flight time: ~165 minutes (2h45m) — consistent with mid-range heavy usage
- Latest logged flight: December 30, 2025

**Liens:** Clean — no encumbrances on record.

**Ghost:** Not a candidate — this one stays busy.

NetJets fractional on a Global 6000, 543 legs in ~2 years is solid utilization. That's roughly one flight every 1.3 days. Nothing actionable for OSA directly, but good benchmark data for what heavy fractional utilization looks like at scale.

---

## Phelipe

What's the route intelligence for KTEB to KPBI?

---

## Claude

Let me search for the route_intel tool.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

**KTEB → KPBI Route Intel**

**Volume:** 3,315 total flights logged — this is a high-frequency corridor.

**Flight Time**
- Average: 155 min (2h35m)
- Min: 113 min | Max: 1,466 min (outlier, likely a divert or data artifact)
- Distance: ~902 nm

**Aircraft Class Mix**
- Super Mid: 43.6% (1,446 flights) — dominant
- Heavy: 40.5% (1,344) — nearly tied
- Midsize: 13.2%
- Light + Turboprop: ~2% combined

Super mid and heavy account for 84% of this route. Nobody's slumming it on a light jet from Teterboro to Palm Beach. That's your pricing anchor — quote Challenger 350 / Citation Longitude / Global as the standard, not the exception.

**Busiest Days**
Thu → Fri → Wed. Classic corporate flow with a Florida leisure tail. Saturday is the dead day (284 flights vs 676 on Thursday). That Thursday spike is a strong sell signal — demand is predictable and you can price accordingly.

**Monthly Trend**
Clear seasonality: peaks in Dec (207) and Nov (152), drops hard in summer (June–August lows of 41–52), starts climbing again in September. April is mid-season at ~100/month pace. This is textbook snowbird corridor behavior.

**OSA application:** This route is a perfect candidate for your Charter Index. Predictable demand, heavy/super-mid dominated, clear seasonal curve — you have enough data to publish a confident price range and rank on "Teterboro to Palm Beach charter" before anyone else does.

---

## Phelipe

Show me recent ownership changes

---

## Claude

Let me call recent_transactions.
```
This block is not supported on your current device yet.
```

Something notable here: all 50 results are deregistrations, all detected at the same timestamp (2026-04-12 23:38:19). This looks like a bulk FAA registry sync/purge event rather than organic ownership changes. The notable ones from a charter perspective are the heavies — several GLF5, GLF6, GLEX, CL60 aircraft deregistered. Let me flag this clearly.Something notable here worth flagging before the breakdown.

**All 50 results are deregistrations, all timestamped identically at 23:38:19 UTC tonight.** That's a bulk FAA registry sync — not 50 individual transactions happening organically. This is likely a periodic purge of expired or re-registered tail numbers hitting the pipeline at once. The data isn't wrong, but it's a batch event, not a live market signal.

**That said, here's what deregistered:**

| Class | Count | Notable Models |
|---|---|---|
| Turboprop | 18 | PC12 (5x), C208 (6x), BE9L (3x), TBM7 |
| Heavy | 11 | GLF5, GLF6 (3x), GLEX (4x), CL60 (4x) |
| Midsize | 8 | E55P (4x), BE40 (3x), C560 |
| Super Mid | 4 | H25B, LJ45 (2x), C680 |
| Light | 4 | C25A, C25B, C25C (2x) |

The heavy count is the most interesting — 4 Global Expresses (GLEX) and 4 Challengers (CL60) deregistered in one batch is a meaningful signal if these aren't re-registrations. Those aircraft don't quietly disappear — they either moved to a foreign registry, changed trust structures, or are mid-sale. The GLF6 trio (N655GA, N660GA, N663GA) with sequential registration numbers suggests a fleet restructuring, possibly a fractional or management company reorganizing.

For OSA Aircraft advisory: deregistration events are exactly the buy-side signal you want to track. An owner who just deregistered a GLEX is either selling, re-flagging, or restructuring — any of those creates an advisory conversation. Worth building an alert layer in Dumont around heavy-class deregistration clusters.

---
