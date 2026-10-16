# EVOF — MRP Supply Recovery & Project Cost Decision | Methodology v0.4

**Status:** documented prototype methodology; synthetic-data pilot, not production deployed. **Date:** 2026-10-16.

## Design rule
EVOF must not recommend a supply recovery action solely from shortage quantity or due date. Every alternative must be evaluated for **incremental total cost, project budget impact, delivery feasibility and operational consequences of waiting or intervening**. Unconfirmed supply is never treated as guaranteed. ERP/MRP remains the system of record and approval.

## Workflow
1. Ingest authorized MPS, BOM, inventory, open PO and project-financial snapshots with extract timestamps and keys.
2. Recalculate gross component demand and time-phased net requirements; identify first shortage date.
3. Separate baseline shortage from the **increment attributable to the MPS change**. Do not assume previously proposed expedites are confirmed receipts.
4. Construct mutually comparable scenarios: wait/replan, expedite, alternate supplier, partial delivery (future), or cross-project reallocation (future).
5. Calculate costs and delivery feasibility for each scenario, using identical baseline and costing scope.
6. Report projected project cost and budget variance, confirmation status, material and production risk.
7. Recommend only **among verified feasible options**; otherwise mark conditional, escalate or request more information. Log scenario, inputs, rationale, owner and approval requirement.

## Key definitions and formulas
- Gross requirements = finished-good MPS quantity × component BOM usage.
- Time-phased projected availability before proposed recovery = prior availability + **confirmed** receipts − gross demand.
- Net recovery requirement at date t = MAX(0, demand at t + applicable safety stock − opening available − confirmed receipts at t). Evaluate chronologically to avoid counting future receipts early.
- Incremental MPS-driven material requirement = change in FG units × BOM usage, adjusted for timing and other changes.
- Incremental scenario cost = additional material spend + incremental freight/premium + verified cancellation/change/production costs + applicable delay impact **without double-counting**. Distinguish cash expenditure, cost exposure and cost avoided.
- Project projected cost = existing project committed/forecast cost baseline + **nonduplicated incremental scenario cost**.
- Budget variance = projected project cost − approved budget. Negative = within budget; positive = overrun under the stated baseline.
- Feasibility is constrained by required date, quantity, supplier confirmation, technical qualification, capacity, logistics and authorization. A plausible date alone is **potential**, not confirmed, feasibility.
- Prioritization: P0 active/unrecoverable disruption; P1 imminent critical risk or unconfirmed critical supply; P2 actionable with sufficient lead-time; P3 covered/monitor. Thresholds are configurable, not universal.

## Pilot baseline and traceability
Synthetic scenario: FG-B MPS 25→45; BOM usage 3 ITM-001/FG; additional demand 60 components; usable stock 90; earlier demand 60 on 2026-10-23; new demand 135 on 2026-10-30; resulting cumulative uncovered demand 105 on 2026-10-30. A prior expedite proposal for 45 is **not confirmed**; therefore 60 is the **conditional additional recovery quantity**, not a stand-alone guaranteed solution.

Project PRJ-200 budget $25,000; existing commitments $20,000; additional 60 components at $52 standard cost = $3,120. Illustrative alternatives:
| Scenario | Extra / delay USD | Total incremental USD | Project projected USD | Due-date test | Status |
|---|---:|---:|---:|---|---|
| Wait until Nov 5 | 2,000 hypothetical delay impact | 5,120 | 25,120 | Late | Not on time; may be chosen if replan is authorized |
| Expedite by Oct 29 | 850 | 3,970 | 23,970 | On time in scenario | Potential; supplier confirmation pending |
| Alternate by Oct 28 | 300 logistics; unit cost $64 | 4,140 | 24,140 | On time in scenario | Potential; qualification and confirmation pending |

**Costing caveat:** The $2,000 waiting impact is an unverified scenario assumption, not a realized cost. The workbook attributes the additional 60 units to PRJ-200 and excludes costs already committed from the incremental comparison. No evidence of supplier quotes, production approvals or actual financial data.

## Out of scope / next increments
Actual ERP integration, real supplier commitments, dynamic MOQ and multiples, full multi-level BOM, plant calendars, production capacity, cross-project inventory allocation, cost allocation governance, full Excel-engine regression and operational deployment.
