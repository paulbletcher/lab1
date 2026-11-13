# Kloud Kart Data Strategy

Kloud Kart Data Strategy Engagement - DE01 lab submission.

## Reading order

| Order | File | Contents |
| --- | --- | --- |
| 1 | [Main lab report](kloud-kart-data-strategy.md) | Situation diagnosis, ranked risks and illustrative costs; recommendation, hiring order and first 90 days; quarterly 12-month roadmap. |
| 2 | [Improvement beyond the brief](improvement.md) | Improvement write-up and completed Weekly Business Performance Exception Report example, together in one document. |
| 3 | [Decision records](decisions/) | Five separate ADRs using the supplied shared template. |
| 4 | [Board presentation](presentations/Kloud-Kart-Building-a-Stronger-Data-Foundation.pptx) | Final submission deck and speaker notes for the live walkthrough. |

## Decision records

1. [Reporting on a second server](decisions/ADR-001-read-replica-for-reporting.md)
2. [Controlled customer-data exports](decisions/ADR-002-controlled-customer-data-exports.md)
3. [Preserving historical data](decisions/ADR-003-preserve-historical-data.md)
4. [Scheduled reporting](decisions/ADR-004-scheduled-sql-reporting.md)
5. [Two data hires](decisions/ADR-005-data-team-hiring.md)

The lab requires one file per decision in `decisions/`, so these remain separate.

## Submission files and status

- **Main report:** The current, authoritative strategy write-up. It contains the diagnosis, concise recommendation, quarterly roadmap, and supporting details, including the complaint-response plan.
- **Improvement:** The current, authoritative improvement write-up and completed exception-report example. The figures are fictional; no automated reporting system has been deployed.
- **Decision records:** Five separate Markdown files containing the choices, rejected alternatives, costs, and responses to increased pressure. All five have complete Consequences and What this survives sections.
- **Presentation:** The final eight-slide PowerPoint is present in `presentations/`. It covers the problems, proposed approach, immediate and deferred work, two hires, quarterly roadmap, budget, and limitations, with speaker notes. Live delivery remains outstanding.

The two main narrative documents are in the project root; the ADRs and deck are additional deliverables. The original Word draft is superseded by the current Markdown documents and is not included in this submission. The ADRs follow the supplied template; the template itself is not included. There is no `docs/` folder.

## Budget and evidence

The [budget table](kloud-kart-data-strategy.md#estimated-first-year-implementation-budget) and [calculation and input sources](kloud-kart-data-strategy.md#budget-calculation-and-input-sources) show how to reproduce the first-year estimate:

| Component | Calculation | GHS |
| --- | --- | ---: |
| Two salaries | 12,000 x 12 + 10,000 x 10 | 244,000 |
| Employer pension allowance | 244,000 x 13% | 31,720 |
| Second server | 1,000 x 12 | 12,000 |
| Backup storage and monitoring | 500 x 12 | 6,000 |
| Recruitment, training, limited setup advice | One-time planning allowance | 7,500 |
| Subtotal | Sum of the five rows above | 301,220 |
| Contingency | 301,220 x 5% | 15,061 |
| **Estimated total** | **301,220 + 15,061** | **316,281** |

The GHS 320,000 planning allowance rounds the total up to the next GHS 10,000, leaving GHS 3,719 above the estimate. Salaries and supplier allowances are unverified planning inputs selected for this proposal, not market research or quotations. The employer rate is supported by [SSNIT's published guidance](https://www.ssnit.org.gh/become-an-employer/). Confirm actual costs and reconcile already-funded items before requesting additional funding.

## Before submission

- Print checks used Google Chrome 157.0.8103.78 in headless mode, with HTML generated using Python Markdown's `tables` and `sane_lists` extensions. At A4, Arial 11 pt, 1.15 line spacing, 20 mm margins, and browser headers/footers disabled, the recommendation is two pages and the roadmap one page. Each section was printed separately, excluding appendices, with the budget heading and table kept together. These counts apply to that print setup; Markdown itself has no fixed pagination.
- Confirm salary, supplier-cost, equipment, and employment-term assumptions before commitments; reconcile amounts already funded.
- Present the slide deck live during the walkthrough and follow the instructor's Markdown guidance and Evalu8 submission requirements.

## Walkthrough preparation

Practise explaining the problem, chosen approach, two hires, budget, quarterly outcomes, and limitations. Show the completed improvement report and trace one example from its warning rule to its priority, responsible department, and action. The recommendation is a plan; the exception report is an illustrative written prototype. No production system, automated pipeline, or capacity test has been demonstrated.

| Likely question | Answer to practise |
| --- | --- |
| Why spend approximately GHS 320,000 when the illustrative losses total around GHS 30,000? | Even recovering all approximately GHS 29,880 of the illustrative annual loss and time value would leave about GHS 286,401 of the GHS 316,281 estimate uncovered. This is not a demonstrated payback case. The [bounded value case](kloud-kart-data-strategy.md#value-case-and-spending-review) specifies reliability, reporting, and privacy outcomes and an end-Q2 spending review. Salaries and pensions account for GHS 275,720 of the estimate. Confirm actual benefits and costs before discretionary expansion. |
| Why a reporting replica rather than a warehouse or real-time dashboards? | The approved second server, existing MySQL skills, two hires, and daily management needs support this first step. The [evidence basis](kloud-kart-data-strategy.md#evidence-basis-and-acceptance-checks) separates brief facts and documented feasibility from untested capacity. A larger platform needs a specific business justification and costed comparison. Live stock stays current on the operational system. |
| What if Nigeria doubles the workload? | Test representative current and doubled activity before making a capacity claim. Review completion times, data completeness, replication delay, and checkout performance. Adjust queries, schedules, or capacity and retest; do not claim the 8,000-order scenario has passed. |
| How can you prove the customer's data was deleted? | Show search and verification records, recipient confirmations, retention exceptions, unresolved gaps, and proof of response. The [proposed audit-trail policy](kloud-kart-data-strategy.md#audit-trail-location-access-and-retention) stores this in company-managed `Governance/Complaints/<case-id>/`, restricted to Nana, the designated privacy lead, and scoped technical contributors. This location is proposed, not deployed. Do not claim every historical copy was erased without evidence. |
| What did you actually build? | A completed written exception-report prototype with explicit rules, fictional weekly figures, priorities, owners, and actions. In the illustrative example, the cancellation rate rises from 5.1% to 8.2%: 8.2 - 5.1 = 3.1 percentage points, meeting the provisional High threshold of at least 2 points. The [fictional inputs and calculation rules](improvement.md#provisional-warning-rules) are provided so the result can be reproduced; no real dataset was used. |

The final deck checked for this submission is `presentations/Kloud-Kart-Building-a-Stronger-Data-Foundation.pptx` (8 slides; SHA-256: `a995d600c61fd7a8903b6be2e37a265b43f72fb090eabea3c2b80d9c12d9bb89`). Rehearse using its speaker notes. Live delivery remains a required step; a file review cannot complete it.
