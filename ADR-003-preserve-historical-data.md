# ADR-003: Preserve selected historical data in a separate store on the second server

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Kloud Kart may later use machine learning for demand forecasting. However, the brief does not confirm what sales, price, or stock history the operational database already retains. A read replica reflects current source changes and does not automatically preserve earlier values. Kloud Kart has limited staff and approximately 40 GB of structured operational data.

## Decision

After checking existing history and second-server capacity, we will schedule collection of selected sales, price, and inventory records from the read replica into a separate writable historical-data store on that server. We will avoid unnecessary customer-identifying information and defer a dedicated warehouse or lakehouse.

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
- **What would make me revisit this:** Insufficient server capacity, new data sources or analytical demands that exceed this design, or a need to capture changes that daily collection misses.

## What this survives

Gradual business growth and an initial forecasting pilot, provided capacity and data quality remain acceptable. Daily snapshots cannot reveal every within-day price or stock change; more detailed change capture may be needed if the business later requires it.
