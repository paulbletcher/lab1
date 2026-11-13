# ADR-005: Hire a Data Engineer and an Analytics Engineer before a Data Scientist

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Kloud Kart can add only two data employees this year. Its immediate needs are protecting the live website, controlling data copies, and replacing inconsistent manual reports. Investors are interested in demand forecasting, but the availability and quality of historical training data have not been verified. The existing team has one PHP/MySQL developer and no professional warehouse or Python experience.

## Decision

We will hire a Data Engineer first to establish the read replica, secure data movement, and monitoring, followed by an Analytics Engineer to agree on business definitions, automate reports, and validate data quality. We will defer a dedicated Data Scientist role until forecasting data and requirements are ready.

## Alternatives considered

### Alternative A: Hire a Data Engineer and a Data Scientist

- **How it would work:** The Data Engineer builds reliable data infrastructure while the Data Scientist explores demand forecasting and develops predictive models.
- **Why it is attractive:** It responds directly to investor interest and could start forecasting experiments sooner.
- **Why rejected:** It would leave no dedicated owner for standardizing Operations' and Finance's measures, automating Nana's reports, and maintaining reporting quality. Forecasting work may also be limited by unverified historical data.

### Alternative B: Hire two general-purpose data professionals

- **How it would work:** Both hires divide infrastructure, reporting, quality, and analysis tasks between them.
- **Why it is attractive:** It offers flexibility when the company's priorities change.
- **Why rejected:** Clear ownership of infrastructure reliability and reporting definitions is more important during the first year. Broad roles could leave critical tasks without accountability.

## Consequences

- **What this buys:** Focused ownership of the two immediate technical needs and a foundation of documented, trustworthy historical data for later forecasting.
- **What this costs:** Recruitment time and salaries for two different skill sets. Specialized forecasting work will be postponed or require temporary external help.
- **What it costs the client if I am wrong:** The company might delay a valuable forecasting opportunity, or hiring the wrong skill mix could slow the replica rollout and reporting improvements.
- **What would make me revisit this:** A funded, urgent forecasting use case with measurable value and suitable historical data, or evidence that the chosen hires cannot cover the reporting and infrastructure workload.

## What this survives

The first year of reporting improvements and gradual expansion into Nigeria if responsibilities remain manageable. Once dependable historical data and a validated forecasting need exist, Kloud Kart can reassess specialist hiring.
