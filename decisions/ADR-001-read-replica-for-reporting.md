# ADR-001: Use a MySQL read replica on a second server for reporting

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Kloud Kart's live website and MySQL database share one server. Large Monday exports slowed the website twice last month, putting customer orders and revenue at risk. A second server is already approved, and the existing developer has MySQL experience. Reporting must be separated without interrupting live orders or stock updates.

**Evidence basis and limits:** These are facts supplied by the brief, not independently observed incidents. Moving reporting queries to another server is an engineering judgement supported by MySQL's documented [replica setup with existing data](https://dev.mysql.com/doc/refman/8.4/en/replication-setup-replicas.html). That documentation establishes an available mechanism, not proof that Kloud Kart's hardware can meet the target. The reference is for MySQL 8.4; the installed version, configuration, table types, and safe initial-copy method remain unverified. No dataset, server access, pipeline demonstration, or capacity benchmark was supplied. The developer and Data Engineer must confirm compatibility and a non-disruptive setup method before copying; the reporting and pressure-test acceptance checks below remain future work.

## Decision

We will configure a MySQL read replica on a second server and direct reporting queries to it. The production database will remain responsible for customer transactions and live inventory.

## Alternatives considered

### Alternative A: Scheduled extraction directly from production into a second reporting database

- **How it would work:** Run scheduled SQL jobs that copy selected records from the main database into a reporting database on the second server.
- **Why it is attractive:** It can transfer only the data required for reports and avoids maintaining continuous replication. Off-peak, incremental extracts could be relatively inexpensive.
- **Why rejected:** Extraction queries would still use production resources. Large or poorly optimized jobs could recreate the slowdown problem, particularly as order volumes grow.

### Alternative B: Load a managed data warehouse immediately

- **How it would work:** Extract MySQL data into a managed warehouse and run reporting there.
- **Why it is attractive:** It separates analytical workloads, supports growth, and could eventually combine new data sources.
- **Why rejected:** Kloud Kart's approximately 40 GB of structured data and small team do not yet justify the additional pipeline, cost, and operational complexity. Data location and privacy arrangements would also need review.

## Consequences

- **What this buys:** Heavy reporting queries move off the live database, reducing the risk of customer-facing slowdowns while retaining familiar MySQL technology.
- **What this costs:** A second server, replication setup and monitoring, possible replication lag, and another protected copy of customer information. Initial synchronization must be planned to avoid disrupting production.
- **What it costs the client if I am wrong:** Replication could still overload production or fail, leaving reporting unreliable and potentially causing more website slowdowns and lost sales. Using lagging replica data for checkout stock could cause overselling; live stock must therefore stay on production.
- **What would make me revisit this:** Any setup, replication, or reporting activity that disrupts checkout or blocks live orders requires the offending background work to stop immediately. Two missed 08:00 Ghana-time reporting deadlines within any 30-day period, incomplete source data at reporting time, or a representative capacity test that cannot meet the reporting target triggers a review of queries, scheduling, and server capacity before considering a dedicated analytical platform. A failed report is marked delayed or replaced with the last successful, dated report; heavy exports must not be redirected to production.

## What this survives

The design separates reporting from customer transactions as order volume and reporting use increase. Doubling from approximately 4,000 to 8,000 orders/day is a proposed pressure-test scenario, not a demonstrated capacity claim. Before relying on that level of growth, the Data Engineer must test representative reporting and replication workloads at current and doubled activity, including busy periods, and record report completion, data completeness, replication delay, and checkout performance.

If the test fails, first adjust queries, schedules, or server resources and retest; use a costed platform review if those measures cannot meet the target. Live stock remains on production under either outcome. No Kloud Kart capacity test has been performed for this submission.
