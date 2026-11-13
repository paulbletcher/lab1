# ADR-003: Preserve selected historical data in a separate store on the second server

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Kloud Kart may later use machine learning for demand forecasting. However, the brief does not confirm what sales, price, or stock history the operational database already retains. A read replica reflects current source changes and does not automatically preserve earlier values. Kloud Kart has limited staff and approximately 40 GB of structured operational data.

**Proposed historical-store field policy:** Preserve product demand at product/date level, without customer-level linkage. No source schema was provided, so the following are logical fields to map and review before implementation, not verified MySQL column names.

| Treatment | Logical fields |
| --- | --- |
| Allow for the stated purpose | Business date and snapshot time; product/SKU identifier; quantities sold, cancelled, returned, and in stock; product price and sales value. Keep currency with monetary values. |
| Allow only if the Ghana/Nigeria comparison needs it | Aggregate market/country, without delivery addresses or customer identifiers. |
| Exclude | Customer IDs, names, emails, phone numbers, delivery/billing addresses, account/payment credentials, payment identifiers, IP/device identifiers, free-text notes, and individual order IDs. |

Do not introduce hashed or pseudonymous customer IDs for this product-level purpose. Any future need for customer linkage requires a separately documented purpose, field review, access controls, and deletion/retention handling before collection. Product-level aggregation is not a claim that every possible re-identification risk has been eliminated. This policy applies to the historical store; the operational replica still requires protection as a copy of the source database.

## Decision

After checking existing history and second-server capacity, we will schedule collection of selected sales, price, and inventory records from the read replica into a separate writable historical-data store on that server. We will enforce the product-level field policy above and defer a dedicated warehouse or lakehouse.

## Alternatives considered

### Alternative A: Introduce a dedicated data warehouse or lakehouse now

- **How it would work:** Move or copy relevant operational data into a purpose-built analytics platform and maintain historical datasets there.
- **Why it is attractive:** It provides room for additional data sources, larger analytical workloads, and future forecasting models.
- **Why rejected:** Kloud Kart has not yet demonstrated that its current data volume or reporting needs justify the extra cost, skills, and maintenance. Reliable business definitions and source history must first be assessed.

### Alternative B: Rely on the read replica alone for future forecasting

- **How it would work:** Query the replicated operational tables whenever historical analysis is required.
- **Why it is attractive:** It requires no additional storage process and is cheaper to maintain initially.
- **Why rejected:** Updates or deletions in operational tables may remove values needed to understand historical demand. The replica cannot recover history that the source does not retain.

## Consequences

- **What this buys:** A growing, structured record of product demand that can support future analysis without new heavy queries on production. The data can be migrated later if a warehouse becomes justified.
- **What this costs:** A separate writable database or instance, scheduled collection jobs, storage, security, quality checks, and monitoring on the second server.
- **What it costs the client if I am wrong:** Collection jobs may consume too much of the second server's capacity and degrade reporting; incomplete or misleading history could produce poor forecasts and inventory decisions.
- **What would make me revisit this:** Historical collection that causes a reporting deadline to be missed is paused or reduced immediately. A forecast that storage will run out within 30 days at the measured growth rate triggers a capacity and retention review. Resume collection only after checking that reporting can meet its target and sufficient space is available. New sources that cannot be accommodated, or a verified need for changes that daily snapshots miss, trigger a review of separate storage or more detailed change capture.

## What this survives

Gradual growth can be accommodated by collecting only the selected product history, scheduling collection outside reporting windows, and applying agreed retention periods. If history competes with daily reporting, protect reporting first, pause historical jobs, and record the resulting gaps. Assess rescheduling, storage capacity, and separate hosting before committing to a larger platform; do not invent missing history or remove records outside the approved retention policy to hide a capacity problem.

Daily snapshots cannot reveal every within-day price or stock change. An initial forecasting pilot remains conditional on verifying suitable history and quality; neither capacity nor forecasting readiness has been demonstrated with Kloud Kart data. The 30-day storage-headroom trigger is a proposed operating rule, not a measured result.
