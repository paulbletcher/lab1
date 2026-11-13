# ADR-001: Use a MySQL read replica on a second server for reporting

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Kloud Kart's live website and MySQL database share one server. Large Monday exports slowed the website twice last month, putting customer orders and revenue at risk. A second server is already approved, and the existing developer has MySQL experience. Reporting must be separated without interrupting live orders or stock updates.

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
- **What would make me revisit this:** Repeated production slowdowns after migration, persistent replica lag that affects reporting, or reporting workloads exceeding the second server's measured capacity.

## What this survives

Growth in orders and additional reporting users, provided measured replication and server capacity remain adequate. If that capacity is exceeded, Kloud Kart can reassess a dedicated analytical platform without changing where live stock is managed.
