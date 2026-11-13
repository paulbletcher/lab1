# Improvement Beyond the Brief: Weekly Business Performance Exception Report

## The problem it solves

Nana currently spends time rebuilding Monday business figures from CSV exports. Finance's figures also differ from hers, making it difficult to know which numbers to trust.

The proposed reporting solution will establish consistent business figures and automate the weekly reporting process. However, having accurate reports does not automatically tell Nana which problems require immediate attention.

For example, a report might show that cancellations increased or refunds were unusually high, but Nana would still need to examine the figures to identify these changes and decide which departments should investigate them.

To address this, I propose a Weekly Business Performance Exception Report. It highlights unusual changes in business performance and directs management's attention to the issues that need investigation.

## What I built

I created a completed example of a Weekly Business Performance Exception Report using illustrative business figures.

The report compares the current week with the previous week and identifies changes that meet the provisional warning rules below. It covers:

- Weekly order volumes.
- Sales performance.
- Order cancellation rates.
- Refund values.
- Product sales performance.

Each identified exception includes its priority, responsible department and recommended next action.

### Provisional warning rules

I selected the following rules for this illustrative prototype. They are planning decisions, not thresholds validated against actual Kloud Kart history. Cancellation-rate increases receive earlier escalation because they directly affect the share of orders completed; the other measures prompt investigation when their changes are larger.

| Business measure | Medium priority | High priority |
| --- | --- | --- |
| Total orders | Decrease of 10% to under 20% | Decrease of 20% or more |
| Sales | Decrease of 10% to under 20% | Decrease of 20% or more |
| Cancellation rate | Increase of 1 to under 2 percentage points | Increase of 2 percentage points or more |
| Refund value | Increase of 15% to under 30% | Increase of 30% or more |
| Product units sold | Decrease of 15% to under 30% | Decrease of 30% or more |

For these rules, apply High priority first; otherwise apply Medium priority if its threshold is met. Changes outside the warning bands receive "No warning". Compare complete, equivalent weeks using consistent business definitions.

For orders, sales, refunds, and product units, percentage change is `(current week - previous week) / previous week x 100`. Use unrounded values to assign priorities and round only the displayed change. A cancellation-rate change uses percentage points: `8.2% - 5.1% = 3.1 percentage points`, which meets the High threshold.

If a required figure is missing, mark the measure "Manual review" rather than assigning a priority. For percentage-change measures, a zero previous-week value also requires manual review because the percentage change is undefined. A valid cancellation rate of zero can still be compared using percentage points.

### Example: Weekly Business Performance Exception Report

The following figures are fictional and demonstrate how the report would work. They are not actual Kloud Kart business results.

**Reporting period:** Illustrative weekly reporting period  
**Prepared for:** Nana Adjei, Head of Operations

| Business measure | Previous week | Current week | Change | Priority |
| --- | --- | --- | --- | --- |
| Total orders | 26,600 | 28,000 | +5.3% | No warning |
| Sales | GH₵432,000 | GH₵485,000 | +12.3% | No warning |
| Cancellation rate | 5.1% | 8.2% | +3.1 percentage points | High |
| Refund value | GH₵15,200 | GH₵18,500 | +21.7% | Medium |
| Product A units sold | 510 | 420 | -17.6% | Medium |

#### Issues requiring management attention

| Identified issue | Priority | Responsible department | Recommended action |
| --- | --- | --- | --- |
| Cancellation rate increased by 3.1 percentage points. | High | Operations | Investigate cancellation reasons, payment failures and delivery issues. |
| Refund value increased by 21.7%. | Medium | Finance | Review refund reasons and identify recurring causes. |
| Product A units sold decreased by 17.6%. | Medium | Inventory / Commercial | Check stock availability, pricing, promotions and product performance. |

**Management follow-up:** Each department should investigate its assigned issue, report the cause and record the corrective action taken. Nana can review outstanding issues at the next weekly meeting.

**Important:** These are warning signals, not confirmed explanations of what caused the changes. I selected provisional rules for the prototype; they must be validated against historical performance and reviewed with management before operational use. Higher refund values may reflect higher sales, and a fall in units sold may reflect unavailable stock rather than lower customer demand.

## What it is worth to Nana

The main benefit is that Nana will spend less time searching through business figures and more time addressing problems that affect operations.

The report will help her:

- **Identify problems earlier:** Unusual increases in cancellations and refunds become easier to spot.
- **Save management time:** Nana receives a focused list of issues instead of having to examine every figure herself.
- **Improve accountability:** Each issue has a responsible department and a recommended action.
- **Make better decisions:** Nana can direct discussions towards the areas requiring attention.
- **Monitor progress:** Outstanding issues can be reviewed during subsequent weekly meetings.

This improvement goes beyond simply automating the Monday report. It adds a management follow-up process that turns reported figures into actions.

The actual time savings and financial benefits would need to be measured after implementation.

## What it cost

Creating this example required no paid analytics platform, database connection or additional server. It uses illustrative figures because no actual Kloud Kart dataset was provided.

For implementation, the report would use the scheduled reporting processes and agreed business calculations in the proposed data strategy.

The Analytics Engineer would validate and refine the provisional warning thresholds with Nana and the relevant departments, while the Data Engineer would support reliable data delivery and scheduled reporting.

The main additional cost would be staff time for configuring, testing and maintaining the warning rules. No separate analytics platform or additional hire would be required.

The report would use the agreed daily-refreshed business data. Live inventory counts and checkout decisions would remain on the operational system because stock information cannot become stale.

This gives Nana a practical way to identify and follow up on business problems without introducing unnecessary technology or infrastructure costs.
