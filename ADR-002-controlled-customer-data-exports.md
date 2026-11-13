# ADR-002: Permit controlled customer-data exports with tracking and automatic expiry

- **Status:** Accepted
- **Date:** 2026-11-12
- **Decision owner:** Data consultant, Kloud Kart engagement

## Context

Marketing exports customer information from a list of about 300,000 people without tracking the resulting copies. Kloud Kart also faces a Data Protection Commission complaint concerning a deleted customer's information, with a stated 90-day response period. Marketing has legitimate reasons to use customer contact data, but Kloud Kart must know where copies are held and whether deletion requests have been handled.

## Decision

We will permit exports only to authorized employees through approved company-managed systems and destinations. We will record each export and its included customer IDs, apply purpose-based retention periods, automatically delete files from controlled storage when due, and verify deletion requests across relevant systems and recipients.

## Alternatives considered

### Alternative A: Prohibit all customer-data exports

- **How it would work:** Remove export permissions for all employees, including Marketing.
- **Why it is attractive:** It sharply reduces new downloadable copies and simplifies access control.
- **Why rejected:** It would unnecessarily obstruct legitimate campaigns and customer communications. It would not eliminate privacy duties for data already stored in the main database or previously exported.

### Alternative B: Replace file exports with direct integrations to approved marketing providers

- **How it would work:** Send approved customer segments directly from company systems to marketing providers through controlled integrations, without downloadable campaign files.
- **Why it is attractive:** It could reduce file copies and make transfers easier to audit and restrict.
- **Why rejected:** Building and validating integrations now would take extra development effort. Controlled exports are a more practical first step; direct integrations can be revisited later.

## Consequences

- **What this buys:** Marketing can continue approved work while Kloud Kart gains records of where customer data goes, automatic expiry for controlled files, and evidence for deletion investigations.
- **What this costs:** Staff training, access management, a secure export register, deletion-job monitoring, and agreements with external recipients. Existing untracked files still require investigation.
- **What it costs the client if I am wrong:** Unrecorded copies or unsuccessful deletions could leave personal data exposed and weaken the complaint response; excessive restrictions could delay campaigns and reduce sales.
- **What would make me revisit this:** Repeated untracked exports, failed deletion checks, or a reliable approved integration that can eliminate routine downloadable files.

## What this survives

More campaigns, employees, and approved providers, as long as each transfer remains recorded and subject to retention controls. It does not by itself prove that historical copies outside company control were erased; those must be investigated separately, and lawful retention exceptions and backups must be documented.
