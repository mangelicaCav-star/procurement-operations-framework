# EVOF simulator — current checkpoint 29 October 2026

The deployed private version is **1.1**, source commit `1d81473187489025282a0bf78a4bc4ae20b06f76`, aligned to the bounded corrective v0.4.2 core rules on 26 October. The guide below preserves original 1.0 scope/history; this current note takes precedence for version and evidence.

- 56/56 JavaScript reference cases passed again on 29 October: 38 retained historical cases and 18 corrective cases. [Current review](EVOF_Review_2026-10-29.md).
- Missing/invalid recovery dates do not cover demand. Missing delivery timing leaves the affected ETA unknown.
- Missing prices, charges, commitments or budget do not become zero. Explicit zero retains its meaning.
- Eligibility precedes cost comparison; equal lowest eligible costs require human review.
- Browser evidence dated 26 October is historical and separate from this Node rerun. No fresh browser or native Excel365 execution is claimed.
- The later rule that open-PO value is already included in project commitments (B23 informative) is not yet verified against the deployed committed-material credit extension. Do not infer approved parity from passing tests.
- No live ERP connection, authenticated supplier/Finance approval, multi-entity integration or full v2.0 completion.

---

# EVOF — Private MRP Decision Simulator 1.0

**Implementation described:** 22 October 2026. **Documentation checkpoint:** 26 October 2026. **Status:** deployed, owner-only prototype using synthetic data. The simulator is a separate implementation of a bounded decision case, not a release of the complete EVOF v2.0 architecture.

[Open the private simulator](https://evof-decision-simulator.humblerobin2048.chatgpt.site) · [Scenario validation](EVOF_Simulator_Validation_2026-10-22.md) · [Published corrected workbook](EVOF_MRP_Project_Cost_Decision_v0_4_1_Coverage_Corrected_LOCAL.xlsx)

The documentation is public. The simulator requires the owner's account; its source and assets are not included in this public repository. Linking to it does not grant access. Public visitors can review this guide and the existing bounded examples on the [portfolio](https://angelica-martinez.humblerobin2048.chatgpt.site).

## Workbook alignment status — 26 October 2026

The [v0.4.2 workbook](../workbooks/EVOF_MRP_Project_Cost_Decision_v0_4_2_2026-10-26.xlsx) now has new date/cost/selection controls and an explicit human-review tie rule. The simulator described below has not been changed or retested in this checkpoint. [Alignment scope](EVOF_Simulator_Alignment_2026-10-26.md) and [current Excel provenance](EVOF_Excel365_Validation_Status_2026-10-26.md) define the next bounded work. Its committed-material-credit extension is not equivalent to the workbook's inactive B23 field. All 38-case simulator statements below refer to the earlier implementation, not proof of parity with v0.4.2.

## What the simulator connects

Changing FG-B production quantities recalculates one ITM-001 component requirement, a single shared stock pool, qualifying supply recovery, uncovered need, independent supply paths, decision windows, replenishment obligations and project-cost forecasts. The result is a recommendation for human review. It does not create an approved purchase or an ERP transaction.

| Area | Editable drivers | Output |
|---|---|---|
| MPS / BOM | Original and revised FG quantity, consumption, original total demand | Signed component change and updated gross demand |
| Shared material | Inventory, prior dated consumption, existing PO receipt | Stock after prior demand and gross shortage |
| Recovery | Quantity, arrival, verification and evidence reference | Qualified coverage and residual shortage |
| Supply | Lead times, confirmation, alternate qualification, lot and capacity assumptions | Arrival, quantity coverage, residual, and latest effective action |
| Financial impact | Prices, fees, modeled delay, commitments, recovery cost, approved budget | Procurement spend, incremental consequence and project forecast |
| Reallocation | Donor position, transfer authorization, replacement evidence, origin need, proposed cost split | Origin protection, replenishment obligation and both affected budgets |

## Corrected baseline

The default cut-off is **16 October 2026**, reproducing the workbook scenario; it is not a current supplier quotation. The need date is 30 October. MPS changes from 25 to 45 finished units, with three components per FG.

| Calculation | Default result |
|---|---:|
| Additional BOM demand: (45 − 25) × 3 | 60 pieces |
| Updated requirement: 75 + 60 | 135 pieces |
| Stock after prior demand: 90 − 60 | 30 pieces |
| Gross / uncovered shortage with no qualifying recovery | 105 pieces |
| Expedited incremental cost: 105 × USD 52 + USD 850 | USD 6,310 |
| Project forecast: USD 20,000 committed + USD 6,310 | USD 26,310 |
| Approved cost budget | USD 25,000 |
| Budget overrun | USD 1,310 |

**The 60-piece supply scenario is conditional:** only after 45 pieces of distinct, verified, documented recovery arrive on time does the residual fall from 105 to 60. Proposed or late recovery does not count. Partial solutions retain their uncovered residual.

## Decision and cost rules

1. Recalculate requirements and consume the shared stock only once. Carry an earlier unmet demand deficit forward.
2. Count a timely verified PO receipt once. Count separate recovery only if verification, evidence and timing gates pass; cap it at the remaining shortage.
3. Compare each alternative independently against the same residual requirement. Round purchase quantities to the disclosed lot assumptions and retain any capacity shortfall.
4. Establish timing, quantity, technical validity and confirmation before ranking. A favorable estimate is not confirmed supply.
5. Keep budget authority separate from delivery feasibility. Confirmed on-time supply above an affected budget requires escalation.
6. For a temporary reallocation, protect the origin through timely confirmed replenishment or a documented approved mitigation path. Evaluate the earlier receiving/replenishment action boundary and check both budgets.
7. Count material once. Deduct only the eligible already-committed material credit. Show fees, uncommitted recovery and modeled delay separately. The delay estimate is an economic consequence, not a booked accounting charge.

The disclosed prototype tie-break chooses the lowest modeled enterprise procurement spend among confirmed, fully covering, timely candidates that fit the affected budgets. It is not a universal EVOF value score. Finance must approve a proposed cross-project cost allocation.

## Inherited rules versus prototype extensions

Core arithmetic and default costs come from v0.4.1. Feasibility-first, allocability, origin protection, decision windows and human governance follow the D04 design baseline reviewed during development. Additional simulator controls are explicitly labeled as extensions: dated verified PO receipts, evidence references, calendar-day lead times, a configurable urgent horizon (default two days), MOQ/order multiples, a common illustrative supply cap, committed-material credit, uncommitted recovery cost, and the bounded donor/replenishment cost split.

These controls are simulated assumptions, not evidence of real capacity, actual approved FX policy or a completed production implementation. All amounts are entered in USD; there is no currency-conversion engine here.

## How to review a scenario

Load the workbook baseline, change MPS, then test unconfirmed, partial, late and full recovery. Select a supply row to inspect its budget impact and latest-action date. Use the reallocation preset to inspect origin replenishment and cost attribution. Every preset evidence reference is demonstrative.

Edits stay in memory until an explicit browser-local save. Load restores that saved scenario. JSON export captures inputs and computed outputs for review. These are local snapshots, not an immutable decision log or a shared database.

## Validation and next development gate

The JavaScript engine passed **38/38 fixed scenario checks**. Browser interaction checks covered live MPS propagation, evidence entry, conditional recovery, reallocation, full coverage, invalid inputs and browser-local persistence. See the separate report for provenance.

Workbook evidence remains distinct: **13/13 prior local coverage checks**, plus **7/7 Excel 365 checks reported by the user on 21 October**. The reported desktop results are not independently witnessed values. Simulator tests do not certify the historical integrated governance v1.1 workbook or every v2.0 requirement.

The next gate is a scenario-by-scenario comparison of workbook, simulator and the project owner's operational judgment, documenting discrepancies and deciding which extensions become accepted EVOF rules. Real supplier validation, capacity, split deliveries, production calendars, ERP/finance reconciliation, broader BOM planning and BUD integration remain open. Multi-entity purchase consolidation, a standalone small-business variant and agent orchestration remain deferred; this simulator does not activate those workstreams.


