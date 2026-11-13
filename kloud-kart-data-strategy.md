# lab1

## Contents

- [1. SITUATION DIAGNOSIS](#1-situation-diagnosis)
- [2. RECOMMENDATION](#2-recommendation)
- [3. 12-MONTH IMPLEMENTATION ROADMAP](#3-12-month-implementation-roadmap)
- [Supporting recommendation detail](#appendix-supporting-recommendation-detail)
- [Detailed quarterly actions](#appendix-detailed-quarterly-actions)
- [Complaint response plan](#appendix-complaint-response-plan)

## 1. SITUATION DIAGNOSIS

Kloud Kart's main problems are not caused by a lack of modern data tools. They come from how the company currently processes, manages, and uses its data.

The company stores orders, inventory, and customer information in one MySQL database, which shares a server with the live website. Nana manually exports data to prepare her Monday reports, Finance produces different figures, and Marketing exports customer information without tracking the copies.

These problems can be traced to four identified or suspected root causes, ranked by their potential impact on the business.

### Root Causes, Ranked by Risk

The data protection issue is ranked first because of the outstanding complaint and its 90-day response deadline, which creates immediate regulatory and reputational exposure. The website slowdown follows closely because it has already disrupted business operations and could result in lost revenue. Both issues are classified as critical and should be addressed simultaneously.

#### 1. Lack of Control Over Customer-Data Copies — Critical

**Root Cause:** Kloud Kart lacks an effective system for tracking and managing copies of customer information, making it difficult to ensure that data is properly handled and deleted when required.

**Evidence and Business Impact:** Marketing exports customer information from a list of approximately 300,000 people without tracking how many copies exist or where they are stored. Kloud Kart also has 90 days to respond to a Data Protection Commission complaint concerning a deleted customer's data.

Without knowing where customer information exists, the company may struggle to prove that the relevant records have been deleted. This creates legal and reputational risks, especially following the recent funding round.

**Cost of Ignoring It:** Potential regulatory penalties, investigation costs, reputational damage, and loss of customer trust. The exact financial exposure cannot be determined from the brief.

#### 2. Reporting and Live Operations Share the Same Computing Resources — Critical

**Root Cause:** The live website and reporting activities depend on the same database server, causing competition for computing resources.

**Evidence and Business Impact:** Large Monday exports compete with customer transactions for processing resources and slowed the website twice last month.

This could cause customers to abandon purchases, resulting in lost revenue. The problem may become more serious as Kloud Kart expands into Nigeria and order volumes increase.

**Cost of Ignoring It:** An estimated GHS 7,000 annually in lost contribution under an illustrative scenario. Actual losses are unknown.

#### 3. Lack of Standardized Business Reporting Definitions — High

**Likely Root Cause:** The absence of agreed reporting definitions or calculation methods may be responsible for the differences between Operations' and Finance's figures.

**Evidence and Business Impact:** Nana's reports consistently differ from Finance's. Possible causes include different reporting periods, treatment of cancellations and refunds, or whether sales are counted when orders are placed, paid for, or delivered.

These explanations have not been verified, but the disagreement makes it difficult for management to determine which figures accurately represent business performance.

**Cost of Ignoring It:** Continued time spent reconciling reports, reduced confidence in financial results, and business decisions based on inconsistent information.

#### 4. Dependence on Manual Reporting Without Sufficient Quality Checks — High

**Root Cause:** Kloud Kart relies on manual exports and spreadsheet calculations instead of a repeatable reporting process with automated validation.

**Evidence and Business Impact:** Nana rebuilds her Monday reports from CSV exports. This creates opportunities for missing records, duplicate entries, incorrect formulas, and inconsistent calculations.

The brief provides no evidence of automated checks that identify these problems before management uses the reports.

**Cost of Ignoring It:** Approximately GHS 22,880 annually in staff time under an illustrative scenario, alongside the risk of making decisions using incorrect information.

### Estimated Financial Impact

The brief does not provide actual salaries, order values, profit margins, or incident durations. Therefore, the following figures are assumptions used to illustrate the possible financial impact.

#### 1. Manual Reporting

Assume Nana spends three hours weekly preparing reports at an estimated staff cost of GHS 100 per hour, while Finance spends two hours reconciling reports at GHS 70 per hour.

Annual cost:

(3 × 100 + 2 × 70) × 52 = GHS 22,880

This represents the estimated value of staff time used for reporting and reconciliation, not a confirmed cash loss.

#### 2. Website Slowdowns

Kloud Kart processes approximately 4,000 orders daily, equivalent to an average of 167 orders per hour.

Assume two slowdowns per month, each lasting 30 minutes, with 10% of expected orders during those periods permanently lost and an average contribution of GHS 35 per lost order.

Estimated annual loss:

167 × 1 hour × 10% × GHS 35 × 12 months = approximately GHS 7,000

This assumes order activity is evenly distributed throughout the day and that similar website slowdowns continue twice monthly.

The actual annual loss may be higher or lower depending on the frequency, duration, and impact of future incidents. Website performance and transaction records would be needed to verify the estimate.

#### 3. Data Protection Risks

The financial exposure cannot be reliably calculated. Costs may include legal advice, complaint investigations, corrective actions, possible regulatory consequences, and reputational damage.

The outstanding complaint makes this a more urgent risk than the estimated reporting costs, even though its financial impact is unknown.

### What I Could Not Verify

- The exact cause, duration, and financial impact of the website slowdowns.
- Why Nana's and Finance's reported figures differ.
- How much time employees actually spend preparing and reconciling reports.
- How many copies of customer information exist and where they are stored.
- Kloud Kart's existing data protection procedures and registration status.
- Whether historical inventory records are already retained.
- The capacity of the existing server and the cost of operating a second one.
- The actual financial effect of the Nigeria pilot.
- Whether Nana prepares reports only on Mondays or also produces reports on other days of the week.
- The exact dates of the two website slowdown incidents, whether they occurred on separate or consecutive Mondays, and how long each incident lasted.

No transactional dataset or actual Finance and Operations reports were provided, so the differences between their figures could not be independently reconciled.

## 2. RECOMMENDATION

Build reliable reporting on the approved second server, control customer-data copies, and hire two people who can operate the system. Kloud Kart's approximately 40 GB of structured data, daily reporting needs, and existing MySQL skills favour this phased approach over introducing a warehouse or lakehouse immediately.

### Protect the website and customer information

Use a MySQL read replica for reporting; orders, checkout, and live inventory stay on the main database. Before the next Monday export, the existing developer restricts essential live-database exports to small batches in monitored quiet periods. Stop jobs that disrupt checkout or orders. After safe setup and testing, target moving Monday exports by the end of Month 1 and complete the reporting move in Q1. If reporting fails, show the last successful report with its date or delay it; do not resume unrestricted production exports.

Nana owns the complaint response. The developer starts tracing records immediately; Marketing and Finance locate their copies. Confirm the notice's actual deadline: project kickoff does not restart the brief's 90-day clock. Track export owners, purposes, destinations, recipients, included customers, and retention periods; verify required deletions and record lawful retention exceptions and unresolved gaps. Management checks registration, renewal, privacy notices, and the responsible data-protection supervisor in the first week. Detailed checkpoints and backup handling are in the [complaint-response plan](#appendix-complaint-response-plan).

### Hire in this order

| Hire and planned start | Skills and first 90 days |
| --- | --- |
| **Data Engineer: Month 1** | SQL/MySQL, performance, and security. Work with the developer on safeguards, safe replica setup, the Q1 reporting move, monitoring, and four Monday exports without reporting-related website slowdowns. |
| **Analytics Engineer: Month 3** | SQL, reporting, quality, and business communication. Reconcile Operations and Finance, document agreed definitions, automate Nana's Monday report, and introduce quality checks. |

These are planning starts, not confirmed appointments. Both hires work with the PHP/MySQL developer; a Data Scientist is deferred. Agree orders, sales, payments, cancellations, refunds, and reporting periods before automating calculations. Operations and Finance validate the results.

### Estimated first-year implementation budget

Planning estimates in GHS, not salary offers or supplier quotations:

| Item | Assumption | First-year cost (GHS) |
| --- | --- | ---: |
| Data Engineer | 12,000/month for 12 months | 144,000 |
| Analytics Engineer | 10,000/month for 10 months | 100,000 |
| Employer pension contributions | 13% of the two salaries | 31,720 |
| Second-server operation | 1,000/month for 12 months | 12,000 |
| Backup storage and monitoring | 500/month for 12 months | 6,000 |
| Recruitment, training, and limited setup advice | One-time allowance | 7,500 |
| **Subtotal** | | **301,220** |
| Contingency | 5% of subtotal | 15,061 |
| **Estimated total** | **Approximately GHS 320,000, rounded up** | **316,281** |

Salaries are gross basic pay: GHS 12,000/month for 12 months and GHS 10,000/month for 10 months. The pension allowance follows [SSNIT's published employer rate](https://www.ssnit.org.gh/become-an-employer/). Existing equipment is assumed reusable; discretionary bonuses and extra benefits are excluded. Confirm employment terms and supplier charges before commitments. Reconcile already-funded hires and server costs before requesting additional money. The illustrative reporting-time savings alone do not establish payback; the investment also addresses reliability and customer-data protection.

### Review before expanding

Target daily reports by 08:00 Ghana time with complete previous-day data and a refresh within 24 hours. Flag the first failure; two missed deadlines in 30 days trigger review. A hiring delay over 30 days triggers reprioritization, protecting website and complaint work. Doubling to 8,000 orders/day is a proposed test, not demonstrated capacity.

Once stable, collect selected sales, price, and inventory history with minimal personal data, subject to capacity. Defer a warehouse, continuous reporting, and forecasting until a specific decision, suitable history, measured capacity, and a costed assessment justify them. Faster reporting needs a named time-sensitive decision and benefits that justify its cost; live stock stays current through the operational system. The trade-offs are another protected data copy, replication delay, operating costs, staff procedures, and maintenance. The [ADRs](README.md#decision-records) and supporting notes retain the detailed alternatives and triggers.

## 3. 12-MONTH IMPLEMENTATION ROADMAP

The complaint deadline follows the Commission's notice, not the project calendar. Hiring and migration dates below are planning targets subject to recruitment and safety checks; immediate safeguards do not wait for either.

| Quarter | Outcomes and responsible people | Evidence Nana verifies |
| --- | --- | --- |
| **Q1: Months 1-3** | **Owners: management, existing developer, Data Engineer; Nana for the complaint.** Protect the website before the next Monday export. Target hires in Months 1 and 3. Safely test the replica, target Monday exports moving by Month 1, and complete the reporting move in Q1; live stock stays on production. Track customer exports. Begin the complaint investigation immediately with Marketing and Finance; check registration and privacy responsibilities in Week 1 and follow the response checkpoints. | Four consecutive Monday exports without reporting-related website slowdowns, with performance records; export register; complaint evidence pack and proof of submission before the confirmed deadline. |
| **Q2: Months 4-6** | **Owners: both hires, Operations, Finance.** Agree business calculations, automate Monday reporting and quality checks, and verify reporting stays on the replica. Monitor reliability and introduce automatic expiry of controlled export files. | Four validated Monday reports; website-performance records; verified deletion logs. |
| **Q3: Months 7-9** | **Owners: both hires.** Assess existing history and server capacity. Collect selected sales, prices, and inventory history in a separate writable store. Monitor quality and storage; pause history jobs if they impair reporting. | At least 30 days of historical records, successful collection jobs, quality results, and storage records. |
| **Q4: Months 10-12** | **Owners: management and both hires.** Review reliability, reporting accuracy, time saved, privacy controls, and ADR triggers. Assess current and proposed doubled-volume test results; disclose unperformed tests. Cost any proposal for extra capacity, a warehouse, faster reporting, or forecasting. | Year-end performance report, trigger log, available workload-test results and untested assumptions, and documented, costed investment decisions. |

## Appendix: Supporting recommendation detail

Supporting safeguards, responsibilities, assumptions, benefits, and trade-offs for the concise recommendation above. The budget table appears in the main recommendation.

### 1. Separate Reporting from the Live Website

Kloud Kart should introduce a MySQL read replica on a second server to handle reporting queries without overloading the live website. The main database will continue processing transactions and inventory updates, while the replica handles reporting. This uses existing MySQL expertise and the approved additional server.

Management reports can refresh daily, while live inventory must continue using the main database. The second server should also have capacity for a future historical-data store.

The existing developer must apply safeguards before the next Monday export, without waiting for recruitment: stop unrestricted large exports and allow essential exports only in small batches during monitored quiet periods. Stop any export or setup job that disrupts checkout, blocks orders, or causes sustained website slowdowns.

The Data Engineer and developer will check the MySQL version, table types, backup method, and a restore test before the initial copy. They must establish a method that avoids disruptive locks or restarting the live database; if this cannot be demonstrated, postpone the copy and use the budgeted setup advice. Target moving Monday exports to the tested replica by the end of Month 1, then complete the reporting move during Q1. These are planning targets, subject to safety checks. If reporting fails, provide the last successful report with its date displayed or delay reporting; do not resume unrestricted exports against production.

**Benefits:** Reduced website slowdowns and more reliable reporting.

**Trade-offs:** Additional server costs, replication delays, monitoring, and security requirements.

### 2. Strengthen Customer-Data Protection

Customer-data exports should be limited to authorized employees using approved company systems. Files must be stored securely and shared only through approved platforms.

A central register should track each export's owner, purpose, location, recipients, retention period, and customer records included. Files should be automatically deleted after their approved retention periods, with deletion results recorded and failures investigated.

Customer deletion requests should be traced across the main database, replica, exports, external platforms, and applicable backups. Required deletions must be verified, with lawful retention exceptions documented.

Kloud Kart must investigate the outstanding Data Protection Commission complaint and respond within the stated 90-day deadline.

Nana owns the response. The existing developer starts tracing records immediately; Marketing and Finance locate their copies, and the Data Engineer supports technical verification after joining. Follow the [complaint-response plan](#appendix-complaint-response-plan) for checkpoints and evidence. Confirm the actual deadline from the Commission's notice; neither recruitment nor project kickoff resets the clock.

**Benefits:** Better data control, fewer unauthorized copies, and verifiable deletions.

**Trade-offs:** Additional employee procedures, training, and monitoring.

### 3. Hire Two Employees with Complementary Skills

**Data Engineer (First Hire):** Strong SQL/MySQL, database performance, security, and pipeline skills.

**First 90 days:** Support the existing developer's immediate export safeguards, investigate slowdowns, safely configure and test the replica, target moving Monday exports by the end of Month 1, and complete the reporting move in Q1. Establish performance and security monitoring and verify four consecutive Monday exports without reporting-related website slowdowns.

**Analytics Engineer (Second Hire):** Strong SQL, reporting, data quality, and business communication skills.

**First 90 days:** Reconcile Operations' and Finance's figures, document agreed definitions, automate Nana's Monday report, and introduce data quality checks.

Both hires should work with the existing PHP/MySQL developer. A data scientist is not a current priority.

### 4. Standardize and Automate Business Reporting

Operations and Finance should review their calculations and agree on definitions for orders, sales, payments, cancellations, refunds, and reporting periods.

The Analytics Engineer should automate the agreed calculations using scheduled SQL queries on the replica, beginning with Nana's Monday report. Both departments must validate the results before adoption. Automated checks should identify missing records, duplicates, and discrepancies.

**Benefits:** Fewer manual errors, reduced reporting time, and consistent figures.

**Trade-offs:** Time needed to agree on definitions, test calculations, and maintain reports.

### 5. Prepare for Future Analytics

Kloud Kart should defer a dedicated warehouse, lakehouse, streaming platform, and machine learning system. Its approximately 40 GB of structured data and daily reporting needs do not currently justify the added complexity.

Once the replica is stable, selected historical data, including product sales, prices, and inventory levels, should be collected on a schedule into a separate historical-data store on the second server, after assessing existing records. This will support future demand forecasting without unnecessary customer information.

Advanced technologies should be reconsidered when business needs and system capacity justify them.

Use 08:00 Ghana time as the provisional daily reporting target, with complete previous-day data and a successful refresh within 24 hours. Flag the first failure; two missed deadlines in 30 days trigger a capacity review. Test a proposed increase from 4,000 to 8,000 orders/day before claiming the design supports it. A hire delayed by more than 30 days triggers reprioritization: protect website and complaint work, and defer history expansion or forecasting. The ADRs define the responses; these targets and tests are proposed, not verified results.

Reconsider faster reporting only for a named business decision that needs action before the daily report and whose expected benefit justifies the extra cost and maintenance. Live stock continues to use the operational system.

**Trade-offs:** Additional storage, processing, and maintenance.

### Budget assumptions and qualifications

The following GHS figures are planning assumptions, not confirmed salaries or supplier quotations. The Data Engineer starts in Month 1 and the Analytics Engineer in Month 3 for budgeting purposes; both amounts are gross basic pay.

The employer pension allowance follows [SSNIT's published 13% contribution](https://www.ssnit.org.gh/become-an-employer/). No discretionary bonuses or extra benefits allowance are included. Implementation uses the two hires and existing developer; existing employee equipment is assumed reusable. Actual employment terms, supplier charges, and equipment availability require confirmation before commitments.

This total includes the approved hires and second server; reconcile funding already allocated before requesting additional money. The illustrative reporting-time savings alone do not repay this investment, which also addresses operational reliability and customer-data protection.

### Expected Outcomes and Verification

- **Website:** Reporting queries moved off production in Q1; four consecutive Monday exports without reporting-related website slowdowns, supported by checkout-performance and error records compared with the pre-change baseline.
- **Data protection:** Nana submits an evidence-backed complaint response before the confirmed deadline; exports are tracked, required deletions are verified, and unresolved gaps are disclosed.
- **Reporting:** Agreed definitions and a validated, automated Monday report.
- **Operations:** Accurate live inventory and daily management reporting.
- **Future analytics:** Historical business data preserved for forecasting.

## Appendix: Detailed quarterly actions

Detailed actions and responsibilities supporting the one-page roadmap above.

### Quarter 1 (Months 1–3): Address Critical Risks

**Responsible:** Management, existing developer, and Data Engineer; Nana owns the complaint response, with Marketing and Finance responsible for locating their copies.

- Apply the developer-owned export safeguards immediately, before the next Monday export; protection must not wait for recruitment.
- Target the Data Engineer starting in Month 1 and the Analytics Engineer in Month 3, consistent with the budget assumptions.
- Safely set up and test the read replica; target moving Monday exports by the end of Month 1 and complete the reporting move in Q1. Live inventory stays on the main database.
- Restrict customer-data exports, identify existing copies, and establish an export register.
- Start the complaint investigation immediately under Nana's ownership. In the first week, management checks registration, renewal, privacy notices, and the responsible data-protection supervisor. Follow the complaint-response checkpoints and submit before the confirmed deadline.

**Nana verifies:** Four consecutive Monday exports from the replica without reporting-related website slowdowns, supported by performance records; the export register; and the complaint evidence pack with proof of submission.

### Quarter 2 (Months 4–6): Automate Reporting and Data Protection

**Responsible:** Data Engineer, Analytics Engineer, Operations, and Finance.

- Monitor website performance and reporting reliability, and confirm routine reporting continues to read from the replica.
- Agree on reporting definitions and automate Nana's Monday report with data quality checks.
- Implement automatic deletion of exported files after approved retention periods.

**Nana verifies:** Four validated Monday reports, website performance records, and deletion logs.

### Quarter 3 (Months 7–9): Preserve Historical Data

**Responsible:** Data Engineer and Analytics Engineer.

- Assess existing historical records and establish a separate historical-data store on the second server, subject to capacity.
- Collect selected product sales, prices, and inventory data through scheduled processes.
- Monitor data quality, storage usage, and reporting reliability.

**Nana verifies:** At least 30 days of historical records, successful scheduled jobs, and data quality results.

### Quarter 4 (Months 10–12): Review Performance and Future Needs

**Responsible:** Management, Data Engineer, and Analytics Engineer.

- Review website performance, reporting accuracy, staff time saved, and data protection compliance.
- Review the ADR triggers: missed reporting deadlines, any untracked exports or failed deletions, storage headroom, and hiring delays. Review results of representative current-volume and proposed doubled-volume tests; disclose any tests not yet performed.
- Decide whether extra capacity, a data warehouse, faster reporting, or forecasting is justified by the evidence, a specific business decision, and a costed assessment.

**Nana verifies:** A year-end performance report with the trigger log, available workload-test results and untested assumptions, and documented, costed decisions on future investments.

## Appendix: Complaint response plan

### Ownership and timing

Nana coordinates the investigation, obtains management review, and submits the response. The existing developer starts the technical search immediately; Marketing and Finance locate exports, spreadsheets, email attachments, and shared copies. The Data Engineer supports technical verification after joining. The investigation does not wait for recruitment, and Nana's business ownership does not establish that she is a qualified data-protection supervisor or legal adviser.

The brief's 90-day period is the case constraint, not a claim about a general statutory response period. Confirm the actual response-period dates from the Commission's notice immediately. Day 30, Day 60, and Day 75 below are proposed internal checkpoints within that period. If the clock is already running, complete overdue steps immediately and compress the remaining schedule; project kickoff does not restart it.

| Checkpoint | Action and evidence |
| --- | --- |
| Immediately | Confirm the deadline, open a restricted complaint log, assign owners, and preserve relevant correspondence and necessary investigation evidence. |
| Within 7 days, or sooner if the deadline requires | List known locations of the customer's data: main database, replica, exports, spreadsheets, email attachments, external providers, and backups. Record unknown locations and who is investigating them. |
| By Day 30 | Establish what was deleted, what remains, and why. Complete required corrective actions and record deletion results and justified retention exceptions. |
| By Day 60 | Verify corrective actions, obtain relevant recipient confirmations, and escalate unresolved copies or missing evidence to Nana and management. |
| By Day 75 | Prepare a management-reviewed response with supporting evidence, remaining limitations, and follow-up actions. |
| Before the confirmed deadline | Submit the response and retain proof of submission. Disclose unresolved gaps rather than claiming that every copy was erased without evidence. |

### Evidence pack

- Complaint correspondence, confirmed deadline, assigned owners, and investigation log.
- A record of locations searched, customer-data copies found, recipients contacted, and unresolved locations.
- Deletion or correction results, verification records, and relevant recipient confirmations.
- Documented reasons for any lawful retention exceptions, restricted access, and applicable retention periods.
- Remaining gaps, further actions and owners, the submitted response, and proof of submission.

For backups, document retention and access restrictions. Ensure deletion instructions are reapplied before restored data returns to use. Distinguish verified removal from data that remains in a restricted backup; do not claim physical erasure without evidence.

### First-week compliance checks

Management checks the registration certificate and renewal status, identifies the responsible data-protection supervisor and any qualification or training gaps, and reviews privacy notices, security procedures, and breach-response arrangements. Record each gap with an owner and corrective deadline. Do not assume the company is unregistered merely because its status was not provided, or that assigning Nana the complaint automatically fulfils the supervisor role. These checks follow the Commission's [organisational guidance](https://dpc.gov.gh/for-organisations/) and [compliance guidance](https://dpc.gov.gh/compliance/); they do not certify legal compliance.
