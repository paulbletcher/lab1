# ADR-004: Automate management reports with scheduled SQL instead of continuous streaming

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Nana manually prepares Monday reports, and her figures differ from Finance's. The brief permits daily refreshes for management reporting, while live stock must remain current to prevent overselling. Kloud Kart has only two approved data hires and limited experience operating advanced analytics systems.

## Decision

Operations and Finance will approve clear definitions for business measures. We will automate those calculations through scheduled SQL jobs on the read replica, starting with Nana's Monday report, and add reconciliation and data quality checks. Checkout and stock updates will continue using the live operational database.

## Alternatives considered

### Alternative A: Stream every transaction into real-time analytical reports

- **How it would work:** Continuously transmit transaction changes to a streaming system and update dashboards as events occur.
- **Why it is attractive:** Managers could see new orders and sales almost immediately and respond to changing activity during the day.
- **Why rejected:** Most requested management decisions do not require second-by-second figures. Continuous streaming adds cost, integration work, and failure points without resolving the existing disagreement over definitions.

### Alternative B: Keep manual CSV exports and spreadsheet calculations

- **How it would work:** Nana and Finance continue exporting data and preparing their own reports, with additional manual checks.
- **Why it is attractive:** It avoids development work and lets employees keep familiar processes.
- **Why rejected:** It preserves repeated manual effort, inconsistent calculations, and opportunities for errors. Large exports from production have already disrupted the live website.

## Consequences

- **What this buys:** Repeatable calculations, less manual work, and figures that can be reconciled using agreed definitions. Daily freshness is sufficient for management reports.
- **What this costs:** Time for business agreement, SQL development, scheduling, testing, alerts, and ongoing quality reviews.
- **What it costs the client if I am wrong:** An incorrect agreed definition could be repeated automatically across reports, leading to poor management decisions. Failed scheduled jobs could also leave Nana without her Monday numbers.
- **What would make me revisit this:** A verified business decision requiring fresher-than-daily analytics, repeated missed reporting deadlines, or data volumes that prevent scheduled jobs from finishing reliably.

## What this survives

Additional routine reports and growth in transaction volumes while daily jobs complete within their reporting windows. It does not replace the operational system's requirement for current inventory at checkout.
