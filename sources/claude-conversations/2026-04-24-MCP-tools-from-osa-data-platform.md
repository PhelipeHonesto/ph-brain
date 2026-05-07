---
title: MCP tools from osa-data-platform
created: 2026-04-24T02:10:55.779547Z
updated: 2026-04-24T02:31:25.401657Z
uuid: a5419927-2a46-4397-b716-a175af461a79
source: claude-conversation
type: source
message_count: 14
---

# MCP tools from osa-data-platform

## Phelipe

What MCP tools are available from osa-data-platform?

---

## Claude

```
This block is not supported on your current device yet.
```

The osa-data-platform MCP exposes two tools, both read-only against your public schema:

**`describe_schema`** — Returns table and column metadata. Call with no arguments to get everything; pass `table` to scope to a single one. Use this first to orient before writing SQL.

**`run_sql`** — Executes a read-only SQL query and returns rows as JSON. Takes `query` (required) and optional `limit` (default 100, cap 1000). The underlying role is SELECT-only, so INSERT/UPDATE/DELETE/DROP fail safely at the permission layer.

That's the whole surface — a schema introspector and a query runner. Anything richer (the typed action layer, ER entity lookups, FBO rollups) lives on the Dumont Intelligence side, not here. This is the raw SQL door into the platform.

---

## Phelipe

How many operators are in the OSA database?

---

## Claude

ꂅ
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

270 operators, spanning 5 distinct `operator_type` values. Want me to break that down by type, or pull the trust/confidence distribution?

That's well below the ~1,821 Part 135 universe you've been anchoring on, so either this table is mid-ingest or it's scoped to a subset (seeded sample, ARGUS-vetted only, etc.). Worth a sanity check.

---

## Phelipe

Using osa-data-platform:
1. Show me the operator_type distribution (count by type)
2. Show me the min and max created_at in the operators table
3. Are there other tables in public schema that look operator-related 
   (anything with "operator", "faa", "part135" in the name)?

---

## Claude

Running all three in parallel — and note the column is `first_seen_at`, not `created_at`, so I'll use that.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Here's what came back:

**1. `operator_type` distribution**

| operator_type | count |
|---|---|
| *(null)* | 265 |
| defunct | 1 |
| foreign_aoc | 1 |
| financier | 1 |
| billing_agent | 1 |
| broker | 1 |

98% of the table is untyped. The five classified rows look like hand-tagged edge cases, not a populated taxonomy. Whatever pipeline is supposed to assign `operator_type` either hasn't run against the bulk ingest or is still being built.

**2. Timestamp range**

- `first_seen_at`: **2026-04-10 → 2026-04-19** (a 9-day window)
- `last_updated_at`: all within **2026-04-19**, inside a ~11-minute span

So this is a very fresh ingest — everything landed in the last two weeks, with a single batch update run on Apr 19. No historical depth yet.

**3. Other operator-related tables**

Fourteen relevant tables. Grouping them:

- **FAA raw/reference:** `faa_operators`, `faa_aircraft`, `faa_aircraft_types`, `faa_airports`, `faa_deregistered`, `faa_docindex`, `faa_engine_types`, `faa_registry_changes`
- **ER / canonical layer:** `operators`, `operator_aliases`, `operator_identities`, `operator_match_review`
- **Derived / analytical:** `operator_profiles`, `operator_market_share`

**What this tells you:** The 270 in `operators` is almost certainly not your full Part 135 universe — it's the post-ER canonical set from an early pass. The real source-of-truth for the 1,821-operator anchor is probably `faa_operators`, with `operator_aliases` + `operator_identities` + `operator_match_review` doing the Senzing-style resolution work between them.

Want me to check `faa_operators` row count and compare it against `operators` to see how much of the universe has actually been resolved?

---

## Phelipe

Using osa-data-platform:
1. Count rows in faa_operators — this is the anchor for the Part 135 universe
2. Count rows in operator_match_review — tells us how many pending ER decisions there are
3. Show a sample of 5 rows from operator_match_review including the 
   relevant columns (whatever schema it has — operator_id, 
   candidate_id, score, decision, reviewed_at, or similar)

---

## Claude

Let me check the schema of `operator_match_review` first so the sample query uses real column names, then run all three.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

**1. `faa_operators`: 3,898 rows**

That's 2x your ~1,821 Part 135 anchor. Either this table is a broader FAA certificate superset (Part 121 + 135 + 141 + repair stations + whatever else the raw FAA dump contains), or it's a historical pull that includes deregistered/surrendered certificates. Worth a `SELECT DISTINCT` on whatever cert/type column lives in there to find out.

**2. `operator_match_review`: 74 rows, all pending**

All 74 are `status = 'pending'`. No human has reviewed a single one yet — `reviewed_at` is null across the board in the sample, and the pending-count equals the total count. This is your backlog.

**3. Sample of 5 pending reviews**

All five are Wyvern scrapes from the same Apr 19 batch run (timestamps cluster within ~4 seconds). Scores are telling:

| scraped_name | top candidate | score | n_candidates |
|---|---|---|---|
| Wheels Up Partners LLC | Wheels Up | 0.88 | 1 |
| Tradewind Charter LLC | Tradewind Aviation | 0.85 | 1 |
| Sky Quest, LLC | SkyWest Charter, LLC | **0.80** | 3 |
| West Coast Worldwide, LLC | SkyWest Charter, LLC | **0.73** | 3 |
| Southern Sky Aviation LLC | Southern Airways Express | **0.65** | 1 |

**The first two are auto-merge candidates.** Wheels Up Partners → Wheels Up at 0.88 and Tradewind Charter → Tradewind Aviation at 0.85 are almost certainly correct; these are the same operator under a slightly different legal name. If you set an auto-accept threshold at ~0.85 with single-candidate gating, you clear these without human touch.

**The middle three are the trap.** "Sky Quest" and "West Coast Worldwide" both top-matching to SkyWest Charter is pure token overlap noise — Sky Quest is a Cleveland-based Part 135 operator, completely unrelated to SkyWest. "Southern Sky" → "Southern Airways Express" at 0.65 is the same failure mode. A naive threshold would merge three genuinely distinct operators into one. This is exactly the kind of thing Senzing's principle-based approach is designed to catch (name similarity alone is not identity — you need corroborating features like address, certificate number, officers).

**Two things worth looking at next:**

1. Whether `faa_operators` actually is the 1,821 Part 135 anchor or a broader superset — determines whether your universe count is right.
2. The score distribution across all 74 pending reviews — tells you how many are auto-mergeable vs. genuinely ambiguous vs. obvious non-matches that should be new-operator creates.

Want either of those?

---

## Phelipe

Using osa-data-platform:
1. SHOW ME THE CERT TYPE BREAKDOWN in faa_operators. Whatever column 
   holds certificate type/class (could be cert_type, operation_type, 
   certificate_class, part_135_flag, etc.) — group by it and count. 
   Tell me which column you used.
2. SCORE DISTRIBUTION across all 74 operator_match_review rows. Bucket them:
   - 0.90+ (high confidence auto-merge)
   - 0.80-0.89 (likely auto-merge with single-candidate gating)
   - 0.70-0.79 (ambiguous — needs review)
   - <0.70 (likely distinct operators, probably new-operator creates)
   Return count per bucket.
3. For the 3 rows with multiple candidates (n_candidates > 1 in the 
   sample), show me ALL the candidates for each — not just the top. 
   I want to see what the #2 and #3 candidates were for Sky Quest 
   and West Coast Worldwide specifically.

---

## Claude

Starting with schema on `faa_operators` so I pick the right column, then running everything in parallel.
```
This block is not supported on your current device yet.
```

Interesting — no explicit cert-type column. `status` is the closest thing to a cert-class signal, and `certificate_number` prefix may also encode type. I'll break down both in one query. Running all three in parallel.
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Those prefixes aren't cert-type codes — they're the first 3 letters of the operator *name*. The `certificate_number` column clearly contains name strings, not certificate numbers. Let me verify and check a sample.
```
This block is not supported on your current device yet.
```

OK — `certificate_number` is actually populated, but these are **not real FAA cert numbers** (those follow format like "ABC123D" assigned by FSDO). These look like internal/synthetic IDs. `1OCA082A` and `7OCA297N` share the `OCA` pattern — possibly an ARGUS/Wyvern-assigned code or a synthetic dedup key. Either way, there's no cert-class signal in this table.

Now the score buckets and full candidate lists:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

**1. Cert-type breakdown in `faa_operators` — doesn't exist**

There's no cert-class column. I grouped by `status` (all 3,898 are `active`) and tried the `certificate_number` prefix, but those values are synthetic IDs like `1OCA082A`, `SOLA001`, `XOJE001` — not real FAA certificate numbers. Real Part 135 certs follow an FSDO-assigned format. This means:

- You cannot filter Part 121 vs 135 vs 141 from this table.
- The 3,898 count is almost certainly a broader operator universe (likely ARGUS + Wyvern rated + additional FAA-pulled operators), not a clean Part 135 subset.
- **If the 1,821 Part 135 anchor matters to OSA positioning, a `cert_part` or `operation_type` column needs to be added to the ingest** — probably sourced from the FAA's Operations Specifications database or the Part 135 list directly. Right now there's no way to answer "is this a Part 135 operator" from the data.

**2. Score distribution — 74 total, 0 above 0.90**

| bucket | total | single cand | multi cand |
|---|---|---|---|
| ≥0.90 auto-merge | **0** | 0 | 0 |
| 0.80–0.89 likely merge | 27 | 12 | 15 |
| 0.70–0.79 ambiguous | 13 | 1 | 12 |
| <0.70 likely new | 34 | 15 | 19 |

Not a single match clears 0.90. That tells you the blocking/scoring is doing a reasonable job of *not* generating false-confidence matches, but it also means there's no "just accept these" tier — every merge needs some form of gating.

**Realistic auto-merge rule:** score ≥ 0.80 AND n_candidates = 1 → **12 clean auto-merges**. The 15 multi-candidate rows in the 0.80–0.89 bucket are the dangerous ones; high top-score but competing alternatives means the token overlap is driving the match, not identity.

**46% (34 of 74) are likely new-operator creates** — below 0.70 suggests no plausible existing match in the canonical set. These should flow to a "create new operator" path, not sit in review.

**3. Full candidate lists for the two multi-candidate ambiguous cases**

**Sky Quest, LLC** (Cleveland-based Part 135 operator, unrelated to any of these):

| rank | candidate | score |
|---|---|---|
| 1 | SkyWest Charter, LLC | 0.796 |
| 2 | Sky Partners, Inc. | 0.659 |
| 3 | Skyvision Aviation Corp. | 0.593 |

All three are "Sky*" name-token matches. None is actually Sky Quest. This is a **new-operator create**, not a merge — the scorer simply doesn't have Sky Quest in `operators` yet.

**West Coast Worldwide, LLC**:

| rank | candidate | score |
|---|---|---|
| 1 | SkyWest Charter, LLC | 0.728 |
| 2 | Freeman Holdings of West Texas, LLC | 0.649 |
| 3 | Pak West Airlines Inc | 0.585 |

Zero semantic overlap in any of these. "West" as a common token is doing all the work. Classic n-gram / Jaccard failure — this is **exactly the scenario Senzing's principle-based approach solves** with corroborating features (address, phone, officers). Right now your scorer has only the name to work with, so anything with a common token ("Sky", "West", "Jet", "Air") will get spurious 0.65–0.80 matches.

**What this tells you about the ER state:**

1. **The scorer is name-only.** If you had address/phone/officer matching layered on top, SkyWest would drop off these lists immediately (different HQ, different certificate, different officers). The single biggest unlock is adding `operator_aliases` or matching against `faa_operators.address/city/state` in the candidate-generation step.

2. **There's no "auto-accept" tier yet, and there shouldn't be until a second feature comes online.** Even 0.88 single-candidate matches can be wrong when name is the only signal.

3. **Your backlog is actually smaller than it looks.** 34 of 74 should never have been routed to human review — they're below any plausible merge threshold. Route `<0.70` to auto-create-new and your review queue drops to 40.

Want me to check whether `operator_aliases` or `operator_identities` has address/phone/officer features that could be wired into the scorer, or pull the full 74-row review list so you can triage it?

---

## Phelipe

Which operators flew the most hours last month?"

---

## Claude

Before I write a query, I need to check whether flight-hours data even exists in this database. Nothing we've seen so far (operators, faa_operators, operator_match_review, etc.) holds flight activity — and the ADS-B archive you've described lives on Lightsail/Glacier, not in this Postgres.
```
This block is not supported on your current device yet.
```

`adsb_completed_legs` is what we want. Let me check its schema and whether it has an operator link.
```
This block is not supported on your current device yet.
```

Good — `flight_time_min` is the field I want, and there's an `operator_name` column but no FK to `operators.id`. That means the answer will be grouped by the raw ADS-B operator string, not your canonical ER'd operator. Worth flagging.

Also noting: `departure_time` and `arrival_time` are `text`, not timestamps. I'll cast with care.

Let me first check what "last month" even means in this data — need to see the date range before I write the filter.
```
This block is not supported on your current device yet.
```

Statement timeout — table is large. Let me use a smaller probe and rely on the `id` ordering instead of scanning everything.
```
This block is not supported on your current device yet.
```

Data goes back to Dec 2023 and forward through Apr 13, 2026. Today is Apr 23, 2026 — so "last month" = **March 2026**. The departure_time strings are ISO format, which string-compares correctly for range filtering (no cast needed, avoids a full scan).

One more thing to notice: `flight_time_min` hits 484 on an American Airlines leg — 8 hours is transcon-plausible, so the units check out. The `operator_name` on the newest rows is messy ("GLOBAL FOUNDRIES... BROOKVIEW CAPITAL... ANTOI" — truncated concatenation of registered owners), which is exactly the noise your ER layer is supposed to clean up. Aggregating on that raw string will give you a muddy answer, but it's the best we have without a join path to canonical operators.
```
This block is not supported on your current device yet.
```

Timeout again — no index on `departure_time` is my guess, so range filtering is doing a full scan. Let me try narrowing through `id` with a probe to find the March 2026 id range, which should use the primary key.
```
This block is not supported on your current device yet.
```

~21M rows. That's why unindexed scans are timing out. I need to bisect by `id` to find the March 2026 window, then run the aggregate against a bounded id range.
```
This block is not supported on your current device yet.
```

id 26M ≈ Feb 26, id 27M ≈ Mar 28. March 2026 lives roughly in the **26,000,000–27,100,000** range. I'll widen slightly to be safe and filter inside with the date predicate.
```
This block is not supported on your current device yet.
```

## Top 20 operators by flight hours, March 2026

| # | operator_name | legs | hours | avg leg |
|---|---|---:|---:|---:|
| 1 | Delta Air Lines | 62,803 | 209,750 | 3.3 |
| 2 | United Airlines | 45,321 | 178,765 | 3.9 |
| 3 | American Airlines | 50,102 | 178,603 | 3.6 |
| 4 | Southwest Airlines | 60,686 | 174,159 | 2.9 |
| 5 | **Bank of Utah Trustee** | 38,264 | 122,649 | 3.2 |
| 6 | SkyWest Airlines | 32,566 | 103,479 | 3.2 |
| 7 | **UMB Bank NA Trustee** | 20,458 | 71,322 | 3.5 |
| 8 | **Wilmington Trust Co Trustee** | 18,955 | 68,566 | 3.6 |
| 9 | JetBlue Airways | 12,914 | 50,004 | 3.9 |
| 10 | Alaska Airlines | 12,221 | 41,329 | 3.4 |
| 11 | Republic Airways | 14,014 | 37,064 | 2.6 |
| 12 | FedEx | 6,696 | 22,584 | 3.4 |
| 13 | UPS | 3,673 | 19,123 | 5.2 |
| 14 | Horizon Air | 4,927 | 12,300 | 2.5 |
| 15 | **TVPX Aircraft Solutions Trustee** | 5,108 | 11,866 | 2.3 |
| 16 | **Wells Fargo Trust Co Trustee** | 3,143 | 10,875 | 3.5 |
| 17 | Air Methods (HEMS) | 5,245 | 10,748 | 2.1 |
| 18 | Christiansen Aviation | 10,745 | 9,708 | 0.9 |
| 19 | Spirit Airlines | 2,982 | 9,179 | 3.1 |
| 20 | Sunrise Asset Management | 2,323 | 8,541 | 3.7 |

## What this actually tells you

**The answer is dominated by airlines and trustees, not by operators in any meaningful OSA sense.** Five of the top 20 — Bank of Utah, UMB Bank, Wilmington Trust, TVPX, Wells Fargo — are **registration trustees**, not operators. They hold aircraft title for non-citizen owners, owner trusts, and leased aircraft. The FAA registry lists them as the "operator" because that's what the registration says, but the actual flying is done by dozens or hundreds of distinct Part 91/135 operators underneath each trustee name.

**Bank of Utah alone shows 122,649 hours and 38,264 legs in a single month.** That's not one operator — that's probably 1,500+ aircraft across the business aviation fleet lumped together because they all share the same title trustee.

This is the exact artifact I flagged earlier: the scorer in `operator_match_review` is name-only, and `adsb_completed_legs.operator_name` is an unresolved raw string from ADS-B / FAA registry. No canonical ER has been applied to this table yet. For OSA's purposes, this ranking is misleading without a join to `operators` via `icao_hex` or `tail_number`.

## What a better version of this query needs

1. **Tail-level ER:** resolve each `icao_hex`/`tail_number` to the *true* operating entity via ARGUS/Wyvern, fleet registrations, or callsign — not FAA title holder.
2. **Filter by segment:** commercial airlines vs Part 135 charter vs Part 91 corporate vs HEMS. Right now they're all mashed together, and comparing Delta to NetJets is nonsense.
3. **Drop trustees entirely** or pierce through them to the beneficial operator.

If you want, I can:
- re-run this filtered to just the trustee-held fleets (biz jet / Part 135 slice) by excluding airline operator names and HEMS
- show how `adsb_completed_legs.icao_hex` joins to your canonical `operators` table (if any tails have been ER'd yet)
- look at `airport_activity` for a different angle on March 2026 movement

Which direction?

---

## Phelipe

Using osa-data-platform:
1. How many DISTINCT icao_hex values appear in adsb_completed_legs 
   in March 2026?
2. Does the operators table have a way to link to icao_hex? Check 
   the operators schema for icao_hex, tail_number, or any FK-looking 
   column that could join to ADS-B.
3. Is there a separate table (aircraft, canonical_aircraft, 
   fleet_registry) that maps tail numbers or icao_hex codes to 
   operator_id? Check for any table in public schema with "aircraft" 
   or "fleet" in the name.
4. What fraction of distinct icao_hex codes in adsb_completed_legs 
   are findable in whatever aircraft/operator mapping table exists?

---

## Claude

Running the structural checks first (schema + table list) in parallel, then the counts, then the join coverage.
```
This block is not supported on your current device yet.
```

Confirmed — `operators` has no icao_hex, no tail_number, no aircraft FK. `headquarters_icao` is an airport code (home base), not an aircraft identifier. Zero direct join path to ADS-B.
```
This block is not supported on your current device yet.
```

`fleet_snapshot` and `faa_aircraft` are the likely join candidates. Let me see their schemas.
```
This block is not supported on your current device yet.
```

`fleet_snapshot` is rollup stats, not tail-level. Not a join path. Let me check `faa_aircraft`.
```
This block is not supported on your current device yet.
```

Good — `faa_aircraft` has `icao_hex`, `tail_number`, and `owner_name` / `certificate_holder`. So the join path is:

```
adsb_completed_legs.icao_hex
  → faa_aircraft.icao_hex
  → faa_aircraft.certificate_holder (text) → operators.canonical_name (fuzzy, via ER)
```

There is **no tail→operator_id foreign key anywhere**. The link is still string-level, has to go through ER. Now the counts:
```
This block is not supported on your current device yet.
```


```
This block is not supported on your current device yet.
```

Now the coverage query — what fraction of March's distinct hex codes are findable in `faa_aircraft`?
```
This block is not supported on your current device yet.
```

Note: the count shifted 52,693 → 52,697 between queries. That's because new March rows are still landing from the ADS-B ingest pipeline — real drift, not an error. Now let me test the final hop — can `certificate_holder` actually match anything in `operators.canonical_name`?
```
This block is not supported on your current device yet.
```

There it is. **0.05%.** 28 out of 52,697 distinct tails can be resolved to a canonical operator via exact string match on `certificate_holder → canonical_name`. That's the ER gap, in one number.

## Summary

**1. Distinct icao_hex in March 2026: 52,697**

This is a reasonable number. Global civil aviation has ~415–450K registered tails; US alone is ~320K per `faa_aircraft` (314,813 total). Roughly 52K unique aircraft flying at least one tracked leg in a month is consistent with known fleet utilization — most registered aircraft don't fly monthly (private/stored/maintenance).

**2. `operators` table: no join path to icao_hex, tail_number, or aircraft FK.**

The only geographic-ish field is `headquarters_icao`, which is an airport code for the operator's base — not aircraft identity. An operator→aircraft relationship simply doesn't exist in the canonical layer. There's no `operator_aircraft_link` or similar.

**3. Aircraft-shaped tables in public schema:**

| table | what it is | joinable? |
|---|---|---|
| `faa_aircraft` | FAA registry, 314,813 tails, 99.6% have icao_hex | **Yes — by `icao_hex`** |
| `fleet_snapshot` | Daily rollup stats by aircraft_class | No (aggregate) |
| `fleet_stats` | Same family, rollup | No |
| `aircraft_listings` | Probably for-sale inventory (OSA Aircraft) | Unknown — separate purpose |
| `aircraft_utilization` | Hours rollups | No (aggregate) |
| `pilot_aircraft_link` | Pilot↔aircraft, not operator↔aircraft | No |
| `adsb_aircraft_state` | Real-time position table | Same hex key, same problem |

**There is NO `operator_aircraft_link` or `fleet_registry` table.** The operator→aircraft relationship lives only implicitly, as a text string in `faa_aircraft.certificate_holder` that has to be ER'd against `operators.canonical_name`.

**4. Coverage of March hex codes into the operator layer:**

| stage | count | pct |
|---|---|---|
| Distinct icao_hex in March | 52,697 | 100% |
| Found in `faa_aircraft` | 52,697 | **100.0%** |
| Has `certificate_holder` populated | 52,497 | 99.6% |
| Exact-match to `operators.canonical_name` | **28** | **0.05%** |

## What this tells you

**The ADS-B data is 100% resolvable to a tail record.** Every hex that flew in March is in the FAA registry. That's a clean foundation.

**The operator layer is essentially disconnected from the fleet.** Only 28 aircraft of ~52K have a walkable path from "thing that flew" to "canonical operator." Your `operators` table at 270 rows and your `faa_operators` at 3,898 rows aren't wired to the aircraft via any key, and the one string that could wire them — `certificate_holder` — isn't normalized to match.

**This is the single biggest structural gap in the platform right now.** It's also, tactically, a relatively contained fix. Three things would close it:

1. **An `operator_aircraft_link` table** keyed on `(icao_hex, operator_id, effective_from, effective_to)`. This is the temporally-bounded link entity you've already architected in the ER model — it just hasn't been populated for aircraft yet.

2. **Run ER on `faa_aircraft.certificate_holder` against `operators.canonical_name`** — probably the same scorer that's populating `operator_match_review` today, just pointed at a different input. 52K tails × ~4K certificate holders is tractable.

3. **`faa_aircraft.owner_name` is only 55% populated (17,267/52,497)** but `certificate_holder` is 99.6%. Use cert_holder as the primary ER input; owner_name as a disambiguator when it exists.

Once that link table exists, the "most hours last month" question becomes `JOIN adsb_completed_legs → operator_aircraft_link → operators` and you get a clean, canonical answer instead of the trustee-dominated mess from the last query.

Want me to probe further? A few useful next moves:

- Sample 20 distinct `certificate_holder` strings from `faa_aircraft` to see how messy the input side is (trustee strings, DBA suffixes, case/whitespace variance)
- Check whether `operator_aliases` already covers any of the common certificate_holder patterns
- Estimate how many distinct `certificate_holder` values exist across all 52K flying tails — that's the actual workload size for the aircraft-side ER run

---
