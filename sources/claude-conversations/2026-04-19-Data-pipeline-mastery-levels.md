---
title: Data pipeline mastery levels
created: 2026-04-19T04:01:23.674782Z
updated: 2026-04-19T04:10:10.016357Z
uuid: 1efdd2b0-4b93-42c7-8eb4-3564bc70fece
source: claude-conversation
type: source
message_count: 6
---

# Data pipeline mastery levels

*Summary: **Conversation Overview**

The conversation covered data pipeline fundamentals through an educational framework the person shared, spanning four levels from basic ETL/ELT concepts through advanced topics like data mesh, CDC, and streaming joins. The person asked Claude to explain two specific tools from the framework — Airflow (an orchestration layer that schedules and sequences jobs without processing data itself) and Spark (a distributed compute engine for processing large datasets across multiple machines). Claude explained both with a practical mental model: Airflow is the conductor, Spark is one of the musicians, and the two work together in a typical pipeline flow.

The conversation then shifted to a practical evaluation of the person's actual project, JetNet 4.7, specifically a platform called Dumont. The person asked Claude to search prior conversations about JetNet to assess whether their existing pipeline architecture aligns with the data pipeline framework they had just shared. Claude used search tools to retrieve context from prior JetNet conversations and found that Dumont is an aviation data platform processing ADS-B flight data, FAA registry information, UCC filings, and operator data. The architecture follows a four-layer medallion pattern: raw data lands in S3 (approximately 1.3TB), moves to organized storage in Supabase Postgres (7.86M rows across 42 tables), then to analytics tables, and finally to a pgvector layer for route similarity search.

Claude assessed Dumont against each level of the framework: Level 0 and the ELT pattern are fully implemented; Level 1 tooling is partially in place with Supabase and S3 but lacks a named orchestrator (currently using Node scripts, bash, and PM2); Level 2 modular design is mixed, with good layering but no formal DAG or dependency graph; and Level 3 data quality is identified as the primary gap, with no row-count checks, freshness tests, or lineage tracking running in the pipeline. Claude noted that 640 passing unit tests on the codebase do not substitute for in-pipeline data quality checks. The recommended next steps were to add freshness and row-count checks to ADS-B ingestion and to migrate archive progress tracking from SQLite to Supabase to resolve a known SQLITE_BUSY issue already flagged in the project.

**Tool Knowledge**

Claude performed three searches using the conversation search tool. The query "building jetnet 4.7" returned insufficient context on its own. The more specific query "JetNet pipeline ADS-B S3 Supabase ELT architecture" with max_results set to 5 returned the substantive architectural details needed. A third search using "ADS-B ingestion worker cron schedule orchestration pipeline" with max_results set to 3 retrieved operational details about the ingestion setup. The pattern that worked: lead with project name plus specific technical components (storage layer, data source, database) rather than project name alone, as the latter was too broad to surface relevant pipeline architecture context.*

## Phelipe

Building Data Pipelines has levels to it:

- level 0

Understand the basic flow: Extract → Transform → Load (ETL) or ELT

This is the foundation.
- Extract: Pull data from sources (APIs, DBs, files)
- Transform: Clean, filter, join, or enrich the data
- Load: Store into a warehouse or lake for analysis
You’re not a data engineer until you’ve scheduled a job to pull CSVs off an SFTP server at 3AM!

level 1

Master the tools:
- Airflow for orchestration
- dbt for transformations
- Spark or PySpark for big data
- Snowflake, BigQuery, Redshift for warehouses
- Kafka or Kinesis for streaming

Understand when to batch vs stream. Most companies think they need real-time data. They usually don’t.

level 2
Handle complexity with modular design:
- DAGs should be atomic, idempotent, and parameterized
- Use task dependencies and sensors wisely
- Break transformations into layers (staging → clean → marts)
- Design for failure recovery. If a step fails, how do you re-run it? From scratch or just that part?

Learn how to backfill without breaking the world.

level 3
Data quality and observability:
- Add tests for nulls, duplicates, and business logic
- Use tools like Great Expectations, Monte Carlo, or built-in dbt tests
- Track lineage so you know what downstream will break if upstream changes

Know the difference between:
- a late-arriving dimension
- a broken SCD2
- and a pipeline silently dropping rows

At this level, you understand that reliability > cleverness.

level 4
Build for scale and maintainability:
- Version control your pipeline configs
- Use feature flags to toggle behavior in prod
- Push vs pull architecture
- Decouple compute and storage (e.g. Iceberg and Delta Lake)
- Data mesh, data contracts, streaming joins, and CDC are words you throw around because you know how and when to use them.

What else belongs in the journey to mastering data pipelines?

Explain

---

## Claude

Great framework. A few things missing from the ladder that separate competent pipeline builders from the people running data platforms:

**Cost awareness.** Somewhere around level 2-3, you start realizing that a query that works isn't the same as a query that should run. A poorly partitioned Snowflake table or a Spark job reading full history every night can burn six figures a year. Mastery means understanding warehouse credits, S3 request costs, egress fees, and when to denormalize vs recompute. The best data engineers read the bill.

**Security and governance.** PII handling, column-level encryption, row-level access, GDPR/CCPA deletion requests, audit logs. At scale, "who can see what" becomes its own engineering problem. Tools like Unity Catalog, Immuta, or Lake Formation exist because this is hard. Bonus: tokenization strategies so analysts can join on a customer_id without ever seeing the raw identifier.

**Schema evolution and contracts.** Upstream teams will change a column type on a Tuesday and break your warehouse on Wednesday. Learning to handle additive vs breaking changes, versioning schemas (Avro, Protobuf), and enforcing contracts at the producer level is what separates "I clean up messes" from "I prevent them."

**Idempotency at the storage layer, not just the task layer.** Your DAG can be idempotent and your data can still be corrupt if you're appending instead of merging, or if your CDC stream has duplicate events. Understanding MERGE semantics, watermarks, exactly-once vs at-least-once, and deduplication windows matters.

**Operational maturity.** On-call rotations, runbooks, SLOs for data freshness, blameless postmortems. "The pipeline broke" becomes "the dashboard was stale for 4 hours, here's the RCA, here's the fix, here's the prevention." Data platforms are products with users.

**Knowing the business.** The most senior data engineers I've seen can tell you why a metric matters, not just how it's computed. They push back on bad requirements instead of building what was asked. That's level 5 — when you stop being a plumber and start being an architect of how the company thinks about its data.

One meta-point worth adding: the tool list at level 1 is already shifting. Iceberg/Delta + DuckDB + lightweight orchestrators (Dagster, Prefect) are eating parts of what Airflow + Spark + warehouse used to own. Mastery means betting on abstractions over specific vendors.

---

## Phelipe

What is airflow and spark?

---

## Claude

**Airflow** is an orchestrator. It's the thing that decides *when* and *in what order* your data jobs run. You write pipelines as DAGs (directed acyclic graphs) in Python — "run task A, then B and C in parallel, then D after both finish, at 3AM every day." Airflow handles the scheduling, retries, dependencies, and gives you a UI to see what ran, what failed, and why. It doesn't process data itself. It tells other things to process data.

**Spark** is a distributed compute engine. It's the thing that actually *does the work* on large datasets. If you have 500GB of logs and need to aggregate them, a single machine chokes — Spark splits the data across a cluster of machines, processes each chunk in parallel, then combines the results. PySpark is just the Python API for it. You write code that looks like pandas, and Spark figures out how to run it across 50 machines.

The way they fit together: Airflow triggers a Spark job at 3AM → Spark reads raw data from S3, transforms it, writes results to a warehouse → Airflow sees the job finished and kicks off the next task. Airflow is the conductor; Spark is one of the musicians.

Quick mental model: if your data fits comfortably in memory on your laptop, you don't need Spark — pandas or DuckDB will be faster and simpler. Spark earns its complexity when data is too big for one machine, which is a much higher bar than most people assume.

---

## Phelipe

Look at building jetnet 4.7 latest chat. See if we are doing a pipeline that makes sense with what i pasted

---

## Claude

```
This block is not supported on your current device yet.
```

Let me pull the most recent JetNet chat to see the actual pipeline architecture you're building.
```
This block is not supported on your current device yet.
```

I have the full picture now. Let me check one more thing — the specific pipeline architecture and what orchestration looks like today.
```
This block is not supported on your current device yet.
```

I have everything I need. Let me answer your question.

---

# Yes — what you're building is a real pipeline, and it fits the ladder

Here's where Dumont sits on the ladder from your pasted levels:

**Level 0 (ETL/ELT basics)** — ✅ Done, and it's ELT, not ETL.

- **Extract**: FAA registry CSV (daily), ADS-B from adsb.lol/OpenSky (continuous + quarterly parquet backfills), UCC filings, operator data
- **Load**: Raw lands in S3 Glacier (~1.3TB, 2024–2025), then organized into Supabase Postgres (7.86M rows, 42 tables)
- **Transform**: Happens *after* load in Postgres — staging tables → cleaned tables → analytics tables → pgvector route similarities

This is textbook modern ELT. The S3-as-immutable-raw layer is exactly what Kleppmann calls the "log" pattern — you can rebuild everything downstream from raw if something breaks.

**Level 1 (tools)** — Partial. You have the warehouse (Supabase/Postgres) and storage (S3). You're missing the named orchestrator. You're using Node scripts + bash + PM2 instead of Airflow/Dagster/Prefect. That's fine for now — Airflow for a solo founder is overkill. But it's the gap to name honestly.

**Level 2 (modular design)** — Mixed. The four layers (Raw → Organized → Analytics → Serving) are clean. The ingestion scripts are resumable (the `ingested-days.txt` tracking file is idempotency done right). But there's no DAG, no dependency graph between jobs, no sensors. The 2026 daily backfill script you wrote is a loop, not a DAG.

**Level 3 (quality/observability)** — This is the real gap. 640 passing tests on the code is great, but there are no **data quality** tests running in the pipeline:

- No nulls/duplicates/freshness checks at ingestion
- No lineage tracking (which downstream analytics break if a raw table changes?)
- No alerting when the FAA registry diff fails or ADS-B ingestion drops rows
- The SQLITE_BUSY bug flagged for "later" is exactly the kind of silent failure this level catches

**Level 4 (scale/maintainability)** — You're ahead on some of this and behind on others. Ahead: storage and compute are decoupled (S3 + Postgres), version control exists, the raw/organized/analytics separation is essentially a medallion architecture (bronze/silver/gold). Behind: no CDC on the FAA registry (you download, not diff), no feature flags, no streaming joins.

---

## The honest assessment

**What you're building is a real data platform, not a toy.** The four-layer architecture with S3 as immutable raw, Postgres as organized, analytics as derived, and pgvector as search index is the same shape Stripe, Airbnb, and Netflix use — just at a smaller scale.

**The two things missing before you call it production-grade:**

1. **An orchestration layer.** Right now your pipeline is "bash scripts + PM2 + vibes." You don't need Airflow, but you need *something* that knows: "FAA diff runs at 4AM, ADS-B worker runs continuously, analytics rebuild runs at 5AM *after* FAA succeeds, alert me when any of these fail." Dagster or Prefect would be the right fit for your scale. Even a single cron + a status table in Supabase would be better than what you have.

2. **Data quality tests in the pipeline, not just unit tests on the code.** The difference: unit tests check if your function works. Data quality tests check if today's ingestion actually landed 20K legs instead of 200. Great Expectations, dbt tests, or even hand-rolled SQL assertions running after each load. This is Level 3 and it's where the Charter Index credibility lives — if your prices are wrong because a silent drop happened upstream, you lose trust fast.

The rest of the ladder (cost controls, schema contracts, CDC, data mesh) is Year 2+ stuff. Don't build it now.

**Next move if you want to close the gap:** pick one Level 3 test and one Level 2 orchestration improvement. The highest-leverage pair is probably (a) add freshness + row-count checks to the ADS-B ingestion that alert you if a day is missing or short, and (b) move the `archive_progress` writes off SQLite to Supabase to kill the SQLITE_BUSY issue — which was already on your list.

That's a weekend of work and it moves Dumont from "works on my machine" to "I'd show this to a CTO candidate without flinching."

---
