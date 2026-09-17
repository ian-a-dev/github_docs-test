# Payroll Strategy

> **Test fixture.** Synthetic content written to exercise a data connector.
> This is not a real strategy document and describes no real product.

## Purpose

Payroll is the system of record for what people are paid and when. This document
states what we are building toward over the next four quarters and, just as
importantly, what we are not.

## Where we are

Three things are true today:

1. Pay runs are reliable but slow to correct. A mistake found after submission
  requires a manual off-cycle run.
2. Multi-state tax handling works, but the rules live in code rather than config,
  so a jurisdiction change is a deploy.
3. Reporting is exportable but not queryable. Customers pull CSVs and rebuild the
  same pivot tables by hand.

## Bets

| # | Bet | Why now |
|---|---|---|
| A | Correction without an off-cycle run | Highest-volume support driver |
| B | Move tax rules from code to configuration | Removes deploys from the compliance path |
| C | Queryable payroll history | Unblocks analytics without a second data store |

## Non-goals

We are explicitly **not** doing these, and saying so here so the question does
not get re-litigated each quarter:

1. Building our own tax-filing engine. We integrate, and we do not file.
2. International payroll. Out of scope until the domestic corrections work lands.
3. A general-purpose report builder. Bet 3 exposes data; it does not ship a UI.

## Dependencies

Bet C depends on the platform data team exposing payroll history through the
warehouse. That dependency is stated here but not yet committed to on their side.

## Sequencing

Bets A and B are independent and can run in parallel. Bet C should not start
until bet B ships, because moving tax rules to configuration changes the shape
of what gets recorded per pay run.
