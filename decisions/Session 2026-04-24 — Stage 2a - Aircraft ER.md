 Shipped - canonical schema + aircraft canonical tables - operator_aircraft_link temporal link table (first use of pattern) - 3 docs, 1 ADR, CLAUDE.md conventions 
 Commits - 67abbb9 — aircraft ER tables + docs expansion - 03efc47 — operator_aircraft_link first temporal link - eeed483 — data-sources map + CLAUDE.md conventions ## Key decisions locked - canonical schema as home for new ER - wingx-engine frozen until Phase 12 - Five-entity discipline - Seven-role model for aircraft relationships - Temporal link pattern: close-then-insert, never UPDATE state fields - ARGUS/Wyvern → Tier E (subjects pay auditors) ## Lesson - Local Docker rollback test ≠ Supabase migration. Both required. - Stage 2a schema NOT applied to prod this session — Stage 2b Step 0. ## Deferred / next - Firecrawl (Option C: Mac-local, separate ops session later) - DB split (osa-data-platform rename + dumont-agent extraction) - operator_aliases audit (dead infra or resolver bug?) - Test count reconciliation (375 vs 640 baseline)
## FAA ingestion: manufacturer column not populated

**Discovered**: 2026-04-24, Stage 2b Checkpoint 1.

**Finding**: `faa_aircraft.manufacturer` is NULL for all 314,813 rows.
The manufacturer name is embedded in `common_name` ("GULFSTREAM G200",
"BEECHCRAFT Super King Air 350") and a code in `model` ("GALX", "B350").

**Impact**: aircraft resolver (Stage 2c) cannot match on manufacturer
directly. Downstream analytics queries like "show me all Gulfstreams"
must parse `common_name` or `model` instead of filtering on a clean
manufacturer field. This is source-side (FAA ingest script), not
backfill-side.

**Fix**: update `src/ingestion/faa-ingest.ts` to extract the
manufacturer prefix from the first token of the FAA master file's
model name field, write to `manufacturer` column. Re-run daily-diff
pipeline.

**Priority**: not blocking Checkpoint 2-4 (we're not matching on
manufacturer in this session). Resolve before Stage 2c (aircraft ER
resolver) so the resolver has clean manufacturer signal.

"Canonical operator coverage via certificate_holder" is structurally capped at ~1-3% because the charter industry registers aircraft to trustees by design. The resolvable-via-registry population is small-Part-135-direct-registrations (a minority). Getting to meaningful operator→aircraft coverage requires:

- Track 1 Stage 3: expand operators canonical via FAA GENOT, DOT Part 295, OpSpec D085 ingestion (adds the airlines we correctly didn't match)
- Stage 2c: trustee-unmask pathway (ADS-B callsign patterns, charter operator self-disclosure, OpSpec D085 operator fleets)
- ARGUS/Wyvern aircraft lists (already show some operator→aircraft mapping, underused)