---
title: Data platform status check
created: 2026-05-05T02:40:57.210692Z
updated: 2026-05-05T22:59:54.742165Z
uuid: 09c6af55-73a3-450e-9d02-c1f7b6ff4f86
source: claude-conversation
type: source
message_count: 22
---

# Data platform status check

## Phelipe

can you check data plataform status

---

## Claude

I'll check the OSA data platform status for you.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Platform is **red across the board**. Everything stopped around April 17 — that's ~18 days of silence.

**What's down:**
- **Pipeline** — last successful run April 17, 03:00 UTC. 431 hours stale.
- **ADS-B feed** — last position April 16, 23:45 UTC. 0 positions/hr, 0 legs today.
- **FAA registry** — last diff April 17. 18 days since last refresh.

**What this looks like:** all three sources stopped within a ~3-hour window on April 17. That's not three independent failures — that's one upstream break. Most likely candidates:
1. **Lightsail instance down or detached** — if the pipeline orchestrator is on Lightsail and it stopped, ADS-B ingest, FAA diff, and the pipeline job all die together.
2. **Cron/scheduler stopped** — systemd timer disabled, GitHub Actions workflow paused, or a billing issue suspended scheduled jobs.
3. **Outbound network / credentials** — adsb.lol fetch and FAA download both failing at the network layer.

**What's still intact:** knowledge graph state (104K tracked, 14K charter, 741 ghosts) and the last eval run (100% accuracy, April 13). The data is fine — nothing's writing to it.

**Suggested triage order:**
1. SSH to Lightsail, check `systemctl status` on the ingest services and `journalctl` for April 17 ~03:00 UTC.
2. Check adsb.lol manually — confirm the source isn't itself down (unlikely given 18 days, but cheap to verify).
3. Check Supabase Pro billing/quota — if you hit a row or storage limit, writes would fail silently.

Want me to pull recent pipeline logs from Supabase, or query for what the last successful ingest looked like to narrow down the failure point?

---

## Phelipe

osa data plataform

---

## Claude

```
This block is not supported on your current device yet.
```

Schema is intact — 56 tables, all the core entities present (operators, faa_aircraft, adsb_*, validation_*, ER tables). Now let me check what's actually moving in the database to confirm the freshness picture from the Dumont health check.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Big aggregate timed out. Let me hit the tables individually — much faster.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

No index on `created_at` for `adsb_completed_legs`, or it's huge. Let me try the indexed columns and check the other key tables.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

I have a clear picture now. Here's the OSA data platform status as of right now:

## Status: 🔴 Stalled — but warmer than Dumont reports

**Where each layer last moved (UTC):**

| Layer | Last activity | Days stale |
|---|---|---|
| `pipeline_runs` (last `faa_nightly`) | 2026-04-12 23:44 | ~22d |
| `faa_registry_changes` | 2026-04-12 23:38 | ~22d |
| `eval_run_summaries` | 2026-04-13 00:46 | ~22d |
| `adsb_positions` | 2026-04-16 23:55 | ~17d |
| `faa_aircraft.updated_at` | **2026-04-23 03:08** | ~11d |
| `operators.last_updated_at` | **2026-04-25 22:23** | ~9d |
| `operator_llm_er_checkpoint` | **2026-04-25 23:51** | ~9d |

**Counts of record:** 314,813 FAA aircraft, 1,947 canonical operators, 352-row LLM ER queue (351 queued, 1 completed — the gate-passing one).

**What this is actually telling you:**

1. **The scheduled pipeline is dead** since April 12. Only 2 rows ever in `pipeline_runs`, both `faa_nightly`, both successful — so it looks like the cron/orchestrator never ran consistently, or those are just the rows that landed after a schema change. Either way, `faa_nightly` has not run in 22 days.

2. **ADS-B ingest stopped April 16-17** — exactly matches what Dumont reported. 0 positions in the last 7 days.

3. **But the platform isn't fully cold.** Three tables show activity *after* the April 17 cutoff:
   - `faa_aircraft` updated April 23 (manual partial refresh? a script you ran?)
   - `operators` and `operator_llm_er_checkpoint` updated April 25 — that lines up with you working on Phase 2 ER.

4. **Phase 2 ER queue is paused.** 351 of 352 queued, 1 completed (the zero-false-match gate). Nothing has moved through in 9 days.

**What's broken vs. what's just idle:**
- Broken: ADS-B ingest cron, FAA nightly cron, eval scheduler.
- Idle (waiting on you): the ER queue runner — that's not a system failure, that's a job you haven't kicked off again.

**Recommended next move:** SSH to Lightsail and check `systemctl --failed` plus `journalctl --since "2026-04-12"` for the ingest services. The fact that all three scheduled jobs died in the same ~12-hour window points to a host-level failure (instance reboot without service auto-start, disk full, or credentials rotation) rather than three independent breaks.

Want me to check S3 archive progress, or dig into whether any tables hit a row/storage ceiling that could've triggered the silent stop?

---

## Phelipe

can you track aircraft by operators?

---

## Claude

Let me check what the operator → aircraft linkage actually looks like in the platform right now.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Confirmed — no `operator_aircraft_link` table yet. So linkage today goes through string-match on names. Let me show you what that gets you in practice.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Two findings worth flagging immediately. Let me confirm one more thing — whether ADS-B legs at least give us a usable fleet view by string-matching.
```
This block is not supported on your current device yet.
```

Yes — but with a major asterisk. Here's the honest answer.

## Can the platform track aircraft by operator? Partially, and roughly.

**What works today (string-match path):**

You can get a usable count for the obvious incumbents by joining on `certificate_holder` (FAA) or `operator_name` (ADS-B). Examples from your live data:

| Operator (string match) | FAA cert holder | ADS-B sightings |
|---|---|---|
| United Airlines | 1,151 | — |
| Delta | 1,029 | — |
| SkyWest | 505 | — |
| Flexjet | — | 104+ tails |
| NetJets | — | 63 + 14 (joint reg) |
| Wheels Up | — | 44 + 4 + 2 |

**What's structurally broken (the finding you flagged before):**

Three problems make this unreliable past the top ~50 names:

1. **The 0.05% linkage problem is real and visible.** No `operator_aircraft_link` table exists. The `knowledge_graph` table has an `operator_name` column but it's reflecting the FAA-registered owner (often a trustee bank, not the operator). 2,032 aircraft have `certificate_holder = "-"`, 1,547 are registered to "BANK OF UTAH TRUSTEE", 601 to "WILMINGTON TRUST CO TRUSTEE" — those banks don't operate anything; they hold title for whoever actually flies the airplane.

2. **The trustee chains are messy.** Look at row 4 above: "NETJETS SALES INC, NETJETS AVIATION INC" — that's two entities concatenated. Or "FLEXJET LLC, ANTON MIDWAY LLC, KINGS HAWAIIAN BAKERY, 352 CORP" — that's Flexjet plus four fractional owners stuffed in one field. Standard string aggregation will undercount Flexjet's true managed fleet by a wide margin.

3. **Your canonical operators table has dupes.** NetJets Aviation appears twice (confidence 0.77 and 1.00). Flexjet twice. Wheels Up twice. FlyExclusive twice. VistaJet shows as both "VistaJet" and "VistaJet US." You have 1,947 operator rows but the dedup-by-canonical-name pass hasn't been applied — these are exactly the kind of records the Phase 2 LLM ER queue (351 still queued) is supposed to resolve.

**What's needed to do this properly** (matches the fix plan already in your notes):

- Build `operator_aircraft_link` with `(operator_id, tail_number, valid_from, valid_to)` so it's temporally bounded.
- Run ER on `faa_aircraft.certificate_holder`, then on the parsed components of comma-delimited `adsb_aircraft_state.operator_name`.
- Resolve trustee → beneficial operator (the Bank of Utah / Wilmington / TVPX cases). This needs the LLM ER queue running, plus the FAA Aircraft Registration Inquiry follow-up — trustees usually file an operating agreement that names the actual operator.
- Dedup the `operators` table — the dupes I just surfaced should resolve to single canonical IDs.

**Bottom line:** I can give you fleet counts for the top 30-50 known operators right now with reasonable confidence (within ~10-15% margin from trustee leakage). Below that, the data isn't reliable until the link table and ER queue run.

Want me to (a) pull a top-100 operator fleet ranking using the best string match available now, with a confidence flag per row, or (b) draft the schema for `operator_aircraft_link` so you can drop it in when you're ready to wire up the ER pipeline?

---

## Phelipe

can you tell me how many legs flexjet did last month?

---

## Claude

```
This block is not supported on your current device yet.
```

Two issues to flag before I give you a number — let me work through them.

The feed died April 16-17, so "last month" (April 2026) is incomplete. And `operator_name` here is the messy ADS-B string, which we just established undercounts Flexjet (single LLC + concatenated trustee chains). Let me run it both ways.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

## Flexjet — April 2026 legs

**Headline number: ~1,309 legs across ~200 tails** (broad ILIKE '%flexjet%' match)

But two big caveats you need to know before quoting it anywhere:

**Caveat 1: April is only ~13 days of data, not 30.**

The feed stopped April 13. Daily counts:

| Date range | Legs | Notes |
|---|---|---|
| Apr 1–12 | 1,273 | full days |
| Apr 13 | 36 | partial — feed died mid-day |
| Apr 14–30 | **0** | feed dead |

Mean across the 12 full days is ~106 legs/day. **Extrapolated full month: ~3,180 legs.** Treat that as a back-of-envelope, not a measurement.

**Caveat 2: The strict vs. broad match gap is huge.**

- `operator_name = 'FLEXJET LLC'` exact: **623 legs / 106 tails**
- `operator_name ILIKE '%flexjet%'` broad: **1,309 legs / 200 tails**

The 686-leg gap is fractional-owner trustee chains — rows like `FLEXJET LLC, ANTON MIDWAY LLC, KINGS HAWAIIAN BAKERY...` where Flexjet is the operator but the FAA-registered owner is the fractional. Broad ILIKE catches most of these but is brittle (no whole-word boundary; would also match e.g. "FLEXJETAVIATION INC" if it existed).

**My read:**

- The 1,309 broad figure is closer to operational truth.
- The 623 strict figure is what a naive `GROUP BY operator_name` would return — and is exactly the kind of undercount that the operator ER work is designed to fix. Once you have a real `operator_aircraft_link` table, this becomes a clean `JOIN` instead of an ILIKE guess.
- Real Flexjet-managed fleet runs ~270+ aircraft. The 200 tails seen here is plausible for ~13 days of activity (not every airframe flies every day).

**Useful comparison number for benchmarking:** at ~106 legs/day mid-week, Flexjet is doing ~38,000 legs/year by this rough cut. WINGX/JETNET typically reports the top 4 fractionals (NetJets, Flexjet, Wheels Up, Vista) at 100K–500K legs/year combined, with Flexjet usually in the 35K–50K range — so the order of magnitude checks out.

Want me to do the same pull for NetJets and Wheels Up so you have a comparable April snapshot for the top three fractionals while we still have the data window?

---

## Phelipe

look in march

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

## Flexjet — March 2026 (full month, clean data)

**Headline: 3,851 legs across 217 tails** (broad match)

| Match method | Legs | Unique tails |
|---|---|---|
| `operator_name = 'FLEXJET LLC'` (strict) | 1,878 | 115 |
| `operator_name ILIKE '%flexjet%'` (broad) | **3,851** | **217** |

**31 days of complete data — all daily counts present, no gaps.** Range: 51 (Mar 27, low) to 170 (Mar 19, high). Mean ~124 legs/day.

**Worth noting:**

- The strict-vs-broad gap is even more telling here: **2× more legs and ~2× more tails** when you include the trustee/fractional-owner concatenations. Same brittle ILIKE caveat as before — but March confirms the pattern, it wasn't a partial-month artifact.
- **217 unique tails** is now closer to the real Flexjet managed fleet (~270+). With a full month of data, you're seeing the long tail of fractional-owned airframes that fly only a few times/month.
- **Annualized run-rate from March: ~46,800 legs/year.** That puts Flexjet roughly on par with what JETNET/WINGX-equivalent reporting would show for the #2 fractional after NetJets.
- **Day-of-week pattern is visible.** The lows (Mar 10 = 62, Mar 26 = 62, Mar 27 = 51) cluster around midweek troughs / Fridays going into weekends. The highs (Mar 19, 20, 25, 29) skew Thursday/Sunday — classic business-aviation pattern.

**For your April comparison:** April's first 12 full days averaged 106 legs/day vs March's 124 legs/day. That's a ~15% drop, but only on a partial sample — could be noise, could be real. With the feed back online you'd be able to tell.

Want me to run the same March pull for NetJets and Wheels Up so you have a clean fractional-tier benchmark, or break Flexjet's March down by aircraft class / route pairs?

---

## Phelipe

what is the route they do the most

---

## Claude

```
This block is not supported on your current device yet.
```

## Top Flexjet route — March 2026: **KPBI ↔ KTEB**

The single most-flown directional leg was **West Palm Beach (KPBI) → Teterboro (KTEB)** at 29 legs. But if you collapse direction and look at it as a corridor, the answer is unambiguously **Palm Beach ↔ Teterboro**:

| Corridor | Legs (both directions) |
|---|---|
| **KPBI ↔ KTEB** (Palm Beach ↔ Teterboro) | **56** |
| KIAD ↔ KTEB (Dulles ↔ Teterboro) | 40 |
| KTEB ↔ KBOS (Teterboro ↔ Boston) | 36 |
| KDAL ↔ KAUS (Dallas Love ↔ Austin) | 28 |

That's almost two flights a day, every day of March, on the Palm Beach–Teterboro pair alone.

**Why this checks out as real (not a data artifact):**

- It's the textbook seasonal NYC ↔ Florida snowbird corridor in peak return-north season — March is exactly when wealthy NY/CT residents start moving back from Palm Beach.
- KTEB is *the* NYC-area private aviation hub, KPBI is the dominant Palm Beach option.
- KFLL → KPBI at 25 legs (#3) is consistent — that's ferry/repositioning between South Florida bases.

**Two anomalies worth flagging:**

- **KTEB → KTEB at 18 legs** — same-airport "legs." These are almost certainly maintenance flights, repositioning hops, or ADS-B leg-detection errors where a brief landing was missed. Worth a data-quality flag for the leg-stitching algorithm.
- **KDAL → KDAL at 15 legs** — same issue at Dallas Love.

Together those 33 same-airport "legs" represent ~1% of the broad-match volume; not a huge deal, but a real signal that the leg-detection logic has a known bug class.

**For your route-page strategy:** Palm Beach ↔ Teterboro is one of the most valuable corridor pages you could build. High volume, high-spend clientele, real seasonal pricing dynamics, and the operator concentration is published-able insider knowledge.

Want me to (a) pull the same top-routes view for NetJets and Wheels Up so you can compare which fractional dominates which corridor, or (b) zoom into the KPBI ↔ KTEB pair specifically — aircraft classes used, day-of-week pattern, time-of-day distribution — so you have everything you'd need for a Loud Hawk piece or a route page?

---

## Phelipe

so this a round trips so people go in the morning come back in the afternoon?

---

## Claude

Smart hypothesis — let me actually check the time-of-day pattern instead of guessing.
```
This block is not supported on your current device yet.
```

Not really. The data says something different and more interesting.

## It's not commute traffic. It's repositioning + relocations.

Let me convert UTC to local times so this makes sense. Both KTEB and KPBI are Eastern Time, so during March (EDT after Mar 9): subtract 4 hours.

**KPBI → KTEB (southbound origin, departing Florida):**

| Local time (EDT) | Legs |
|---|---|
| 7am | 1 |
| 8am | 4 |
| 9am | 2 |
| **10am** | **5** ← peak |
| 11am | 2 |
| 12pm | 1 |
| **1pm** | **5** ← second peak |
| 2pm | 3 |
| 3pm | 2 |
| 4pm | 2 |
| 5pm | 1 |

**KTEB → KPBI (northbound origin, departing NY):**

| Local time (EDT) | Legs |
|---|---|
| 8am | 1 |
| **10am** | **5** ← peak |
| 11am | 2 |
| 12pm | 3 |
| **1pm** | **4** ← second peak |
| 2pm | 2 |
| 3pm | 3 |

**Both directions peak mid-morning to early afternoon — there is no morning-out / evening-back commute pattern.**

If this were daily commuting, you'd see a sharp morning spike one way and a sharp evening spike the other way. Instead both directions look nearly identical. **This isn't day-trip commuting. It's longer-stay relocations** — people heading down for a weekend or a week, others heading back. Combined with the corridor being snowbird-season Florida↔NY in March, that's exactly what you'd expect: families and individuals rebalancing between two homes, not commuting.

**The other tell:** the flight is ~2.5 hours block time. A morning-out / evening-back commute on a 2.5-hour leg would mean ~5 hours in the air for a working day. Possible for a CEO with a specific reason, but rare as a daily pattern. Almost no one does PBI↔TEB as a same-day round trip.

**What's actually happening** (most likely):
- ~50% of these are owner trips (fractional clients heading to/from their second home or a multi-day stay)
- A meaningful chunk are **repositioning legs** — empty aircraft moving to where the next paying passenger is. The fact that early-morning and late-evening departures exist (1am, 2am, 3am UTC = 9pm-11pm EDT) is consistent with overnight repositioning.

**The few same-day round trips that do exist** would be visible in the data if I cross-checked individual aircraft tail movements within 24 hours. Want me to pull that — actual same-tail same-day round trips on this corridor — to put a real number on how much is genuine round-trip vs. one-way?

---

## Phelipe

yes

---

## Claude

```
This block is not supported on your current device yet.
```

Now let me also check for **same-tail round trips within 24 hours** (not just same calendar day, since redeyes cross dates) to make sure we're not missing late-night returns.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

## Verdict: round trips are vanishingly rare on this corridor.

**Out of 56 total Flexjet PBI↔TEB legs in March, only 4 same-tail round trips happened within a 24-hour window — and the pattern says they're almost certainly not passenger round trips:**

| Tail | Pattern | Time on ground in middle | What it really is |
|---|---|---|---|
| N532FX | TEB→PBI→TEB on Mar 9 | **1.2h** | Drop & turn — landed PBI, dropped pax, ferried right back |
| N477FX | TEB→PBI→TEB on Mar 9 | **1.4h** | Same — drop & turn |
| N582FX | PBI→TEB→PBI on Mar 13 | **14.7h** | Overnight — could be either |
| N582FX | TEB→PBI→TEB on Mar 14 | **17.3h** | Overnight — same airframe, day 2 |

**A genuine same-day passenger round trip would have ~4-8 hours on the ground in the middle** (drop pax in morning, pick them up in afternoon/evening for the return). Zero of these match that profile.

The two 1.2-1.4h turns are almost certainly **operator repositioning** — the aircraft delivered passengers, then immediately deadheaded back empty to be ready for the next charter. That's classic fractional ops, not a passenger round trip.

The two ~15-17h turns on N582FX are the same airframe doing PBI→TEB→PBI→TEB across two days. That's most likely the airframe shuttling between passenger trips (different passengers each direction), not one party round-tripping.

## Confirmed picture for this corridor

**~3.6% same-tail return rate within 24 hours, and 0% genuine same-day passenger round trips.** The KPBI↔KTEB corridor is overwhelmingly **one-way relocations**, not commuting. The mid-morning + early-afternoon double peak you saw isn't morning-out / evening-back — it's just the conventional preferred private-aviation departure windows (post-coffee morning, post-lunch afternoon), and they happen in *both* directions independently because different parties are flying each way.

**This is exactly the kind of insight Loud Hawk could publish well.** The "people commute by jet between Florida and NYC" trope is widely assumed and, on this data, mostly wrong — the real story is that fractional clients use these aircraft for asymmetric multi-day stays, and operators eat a lot of empty repositioning to keep the network balanced.

That repositioning gap — the 2 same-day deadheads visible in just 56 legs — is also exactly where **Ghost Positioning** has commercial value: a charter buyer in PBI on Mar 9 at ~10pm could have caught N532FX heading back to TEB empty for a fraction of the on-demand price.

Want me to count total empty repositioning legs across all Flexjet flights in March (any aircraft turning around within 2 hours of arrival), or pivot to the same drop-and-turn analysis for NetJets and Wheels Up to see whose network has the most repositioning slack?

---

## Phelipe

check the data now

---

## Claude

## Status check — Tuesday May 5, 2026
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

## Still down. Nothing has moved.

| Source | Last activity | Stale |
|---|---|---|
| `adsb_positions` | 2026-04-16 23:55 UTC | **18 days, 16 hours** |
| `adsb_completed_legs` | 2026-04-13 23:54 UTC | **21 days, 16 hours** |
| `pipeline_runs` | 2026-04-12 23:44 UTC | **22 days, 17 hours** |

Identical to what we saw earlier in this conversation. **No new data has landed.** Nothing has been silently restored in the background — whatever broke on April 12-17 is still broken.

**Why the 4-day gap between last leg (Apr 13) and last position (Apr 16):** raw positions kept arriving for a few days after leg-stitching stopped, then positions stopped too. That's a useful diagnostic — it means the failure cascade was *not* simultaneous. The leg-stitching job died first (Apr 13), then ADS-B ingest itself died ~3 days later (Apr 16-17). Two separate breaks, not one.

That changes the triage picture from earlier:

**Most likely scenario now:** the leg-stitching service crashed or hit an error on Apr 13. Positions kept flowing into `adsb_positions` for 3 more days while the stitcher backlogged. Then around Apr 16-17, either (a) the position ingest also broke independently, or (b) the disk filled up because legs weren't being stitched and rolling off, eventually choking everything. The latter is a common failure mode and worth checking first.

**Suggested SSH check, in order:**
1. `df -h` on Lightsail — disk full is my new top suspicion given the staggered failure.
2. `systemctl status` on whatever runs the leg-stitching pipeline — check the journal around April 13 ~23:54 UTC for the original crash.
3. Once you've fixed root cause, the recovery path is: re-enable position ingest first, then stitch the backlog. **But you may have lost ~3 weeks of ADS-B history permanently** if adsb.lol's daily tarballs aren't still available — they typically retain ~7-14 days. Worth checking S3 Glacier to see if the raw tars at least made it to archive before the break.

Want me to query for the actual error on the last pipeline run, or check whether anything in the FAA/operator tables moved during these 22 days (which would indicate parts of the stack are still alive)?

---

## Phelipe

the database of operators?

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

## The operators table is **alive and active.** Updated minutes ago.

| Metric | Value |
|---|---|
| Total operators | 1,947 |
| **Latest update** | **2026-05-05 22:09 UTC** ← today, ~30 minutes ago |
| Updated in last 7 days | 1,427 (73%) |
| Updated in last 30 days | 1,947 (100%) |
| First record created | 2026-04-25 22:23 UTC |

So the picture splits cleanly in two:

**Dead** (since Apr 12-17): ADS-B ingest, leg stitching, scheduled pipeline runs. Real-time flight intelligence is offline.

**Alive and being actively built** (May 5, today): the operators canonical table. Something — either a script you've been running, or the LLM ER work — has been touching this table within the last hour.

This is consistent with how you've been working: hand-running ER passes on the 352-record queue while the upstream feed is broken. The operators table existing entirely within the last 10 days (`first_seen_at` max is Apr 25) suggests this is a **fresh canonical operators build**, possibly a rebuild from scratch or a Phase 2 cutover.

A few questions worth asking the data:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

## Operator database — full picture

**Today's activity:** 1,427 operator rows updated today (May 5). That's a 73% rewrite of the table in one batch.

**Build pattern from the timestamps:**
- Apr 25: 344 rows created/updated (likely the initial Phase 2 ER seed batch — recall the 352-record queue)
- May 5 (today): 1,427 rows updated — likely a bulk classification or enrichment pass

**Composition:**

| operator_type | Count | Avg confidence | Avg trust |
|---|---|---|---|
| part_135 | **1,461** | 0.951 | 0.046 |
| *(null/unclassified)* | 481 | 0.712 | 0.247 |
| broker | 1 | 0.830 | 0.830 |
| financier | 1 | 0.770 | 0.390 |
| foreign_aoc | 1 | 0.710 | 0.730 |
| billing_agent | 1 | 0.730 | 0.750 |
| defunct | 1 | 0.830 | 0.830 |

**A few things worth flagging:**

1. **1,461 part_135 operators is sane.** FAA's actual Part 135 certificate count is ~1,800-1,900 active. You're at ~77% coverage of the universe, which lines up with the typical signal-to-noise from FAA's open Part 135 list (some are cargo, some are air ambulance, some are dormant — your 481 unclassified bucket likely has more part_135s in it that haven't been confirmed yet).

2. **The avg_trust of 0.046 for part_135 is striking and probably wrong-by-design.** Either trust scoring hasn't run yet for the bulk of the table (default-zero), or the trust signal is intentionally still being computed. The 481 unclassified ops have 5x higher trust (0.247) — that suggests trust is being calculated only on a subset, not on the bulk-imported part_135 list. Worth checking if trust_score has a separate run cadence.

3. **The 1-row classes (broker, financier, billing_agent, defunct, foreign_aoc) look like manual test inserts** or category seeds. Almost certainly not the final shape — you wouldn't have 1 broker globally.

4. **No fractional class.** NetJets, Flexjet, Wheels Up, VistaJet are presumably all classified as `part_135` right now, but they're commercially distinct from on-demand 135 operators. Might be worth a `fractional` or `program` type tag.

5. **The 481 nulls are probably your highest-leverage cleanup target** — that's the bucket where the LLM ER queue would resolve real classifications. They're also showing low confidence (0.712) and elevated trust (0.247) which is an unusual combination — these are records the system is *uncertain* about but somehow trusts more than confirmed Part 135s. Smells like a normalization issue.

**Bottom line:** the operator database is in active build mode and has been touched as recently as 30 minutes ago. The ADS-B side of the platform is dead and untouched for 22 days. Two completely different states, one platform — which matches what you've been doing manually.

Want me to look at what the 481 unclassified operators look like (sample names, type_tags), or see whether the major fractionals show up as a single canonical row each or have dedup issues?

---

## Phelipe

what abput aircraft to operator

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

Confirmed: there is **no operator → aircraft link table**. `fleet_snapshot` and `fleet_stats` are aggregate-by-aircraft-class only (light jet, midsize, heavy, etc.), not per-operator. `pilot_aircraft_link` is the wrong direction (people, not operators).

So the answer to "can the platform link aircraft to specific operators?" is: **not yet, structurally.**

Let me confirm what tables touch on aircraft and operators in any form, to map what raw signals you actually have to work with:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

## Aircraft → Operator linkage state

**Bottom line: still 0% structural linkage.** The `operator_aircraft_link` table you've planned doesn't exist yet. There are 1,947 canonical operators and 314,813 FAA aircraft sitting on opposite sides of the database with no formal join between them.

**What you have to work with right now (raw signals, no canonical IDs):**

| Source | Field | Coverage | Quality |
|---|---|---|---|
| `faa_aircraft` | `certificate_holder` | 182,052 / 314,813 (58%) | 127,538 unique strings — heavily duplicated, no ER applied |
| `adsb_aircraft_state` | `operator_name` | 70,843 / 77,332 (92%) | Reflects FAA registered owner, often a trustee or fractional shell |
| `adsb_completed_legs` | `operator_name` | high (per-leg) | Same trustee leakage problem |
| `knowledge_graph` | `operator_name` | partial | Same problem |
| `aircraft_utilization` | `operator_name` | aggregate | Same problem |

Note: 127,538 unique strings against 1,947 canonical operators is a **65:1 dedup ratio.** That's the size of the ER problem. Even after dedup most of those will be private owners and corporate flight departments, not commercial operators — so the real ratio for charter-relevant entities is probably more like 5:1, but it's still a lot of normalization work.

**Why aircraft → operator hasn't been built yet:**

You need *both* sides clean before the link table is useful. The operators side just got rebuilt today (1,427 rows touched). The FAA aircraft side hasn't had ER run on `certificate_holder` yet. Linking now would just propagate the trustee-leakage problem you already identified — Bank of Utah Trustee, Wilmington Trust, the comma-concatenated fractional chains.

**The dependency chain looks like this:**

1. **Done:** Operators table canonicalized (1,947 rows, ~today)
2. **In progress:** LLM ER queue on operators (351 of 352 still queued — paused)
3. **Not started:** ER on `faa_aircraft.certificate_holder` to map 127,538 strings → ~3,000 canonical operator IDs
4. **Not started:** Trustee resolution layer (Bank of Utah → actual operating entity, requires FAA Aircraft Registration Inquiry data or scraping)
5. **Not started:** `operator_aircraft_link` schema + populate (one row per aircraft per time-bounded operator relationship)
6. **Not started:** Reconciliation against ADS-B `operator_name` to validate

**The right shape for `operator_aircraft_link`:**

```
operator_id          uuid (FK -> operators.id)
n_number             text  
icao_hex             text
relationship_type    enum (managed, owned, leased, fractional, trustee_held)
valid_from           timestamptz
valid_to             timestamptz nullable
source               enum (faa_cert_holder, adsb_observed, manual, public_filing)
confidence           numeric
provenance           jsonb
```

**Realistic interim path** if you need *some* aircraft → operator data working before the full ER pipeline runs: you could ship a "best-effort" view that does fuzzy string matching between `operators.canonical_name` and `faa_aircraft.certificate_holder` for the top 50-100 known operators (NetJets, Flexjet, Wheels Up, FlyExclusive, VistaJet, the major Part 135s). That covers ~70% of charter-relevant flying with maybe ~85% precision — good enough for Charter Index v0 if you flag confidence on the output.

The remaining long tail (regional operators, single-tail Part 135s, dormant certificates) requires real ER and isn't worth racing for v0.

**My read on prioritization:** the Phase 2 LLM ER queue stalling at 1 of 352 completed is the actual bottleneck here. Once that runs, you have clean operator IDs to anchor the link table to. Without it, building `operator_aircraft_link` against the duplicate-laden operators table just creates work you'll have to redo.

Want me to (a) draft the SQL DDL for `operator_aircraft_link` so it's ready to drop in, (b) do the interim fuzzy-match exercise for the top 50 operators so you have *something* working before the full pipeline runs, or (c) audit the ER queue to figure out why only 1 of 352 has been processed?

---
