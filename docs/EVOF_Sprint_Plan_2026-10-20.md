# EVOF — Sprint plan | 2026-10-20

**Workstream:** MRP Buyer / Project Cost Decision v0.4. **Status:** PLANNED; today's dynamic tests NOT YET EXECUTED. **Data:** fictional.

## Objective
Demonstrate end-to-end change propagation from MPS/project demand to BOM material requirements, time-phased inventory coverage, sourcing alternatives, incremental cost and project budget impact, without double counting.

## Verified starting point
- Workbook `EVOF_MRP_Project_Cost_Decision_v0_4.xlsx` is already present in the GitHub repository.
- Prior v0.4 validation records 13 arithmetic/static PASS (V01–V13), not a live spreadsheet recalculation.
- V14 (input mutation/recalculation), V15 (MOQ/multiple deliveries/supplier capacity), V16 (real project finance) remain NOT RUN.
- ERP-linked approval, lead times, available-to-promise and real financials are not authenticated.
- The integrated governance workbook v1.1 has its own separate T01–T12 functional test matrix; it is not the target of this sprint.

## Execution plan
| Priority | Task | Evidence required | Status |
|---|---|---|---|
| P0 | Freeze v0.4 baseline and inputs | Version/hash, baseline values, engine | NOT RUN |
| P0 | Mutate MPS demand; verify BOM explosion | Before/after demand and component requirement | NOT RUN |
| P0 | Verify time-phased inventory and open PO coverage | Available-by-date, uncovered quantity, no double count | NOT RUN |
| P0 | Compare wait, expedite, alternate | Cost assumptions, lead time and feasibility flags | NOT RUN |
| P0 | Propagate selected option to project budget forecast | Incremental cost and budget baseline preserved | NOT RUN |
| P1 | Negative tests: unconfirmed ETA, insufficient supply, infeasible delivery | Explicit HOLD / infeasible or documented model gap | NOT RUN |
| P1 | Record evidence and defects; reconcile README | PASS/FAIL/BLOCKED with exact observations | NOT RUN |

## Sprint acceptance criteria
1. At least one MPS input mutation propagates reproducibly to BOM, net material need, sourcing alternatives and project forecast; all intermediate outputs are recorded.
2. Inventory/PO supply is counted once at the correct time bucket; late supply cannot satisfy an earlier due date.
3. Wait/expedite/alternate costs and feasibility are separately explained; unsupported supplier confirmation is never represented as guaranteed.
4. Project forecast equals baseline plus *incremental* selected option cost, without mixing commitments, receipts and recognized costs.
5. Every executed test has workbook/version, changed input, expected result, observed result, test engine, status and restoration evidence.
6. No critical P0 defect remains unresolved; if a control is unsupported, mark BLOCKED and restrict the release claim.
7. README and validation report accurately describe the v0.4 file as published, static validation as completed, dynamic validation only if actually executed, and production limitations.

## Exclusions / future functionality
- Actual ERP/MRP integration, supplier confirmation, live project accounting, approval enforcement.
- MOQ, split deliveries and capacity optimization beyond demonstrated test support (V15).
- Real project cost validation (V16).
- Integrated governance workbook v1.1 T01–T12 tests: separate sprint.

## Decision gate
If all P0 checks pass with recorded evidence, mark **v0.4 functional pilot validated in the tested environment**, not production ready. If any P0 test fails or is blocked, mark **partial validation** with an issue and corrective plan. Excel 365 desktop execution may be deferred but must be explicitly stated, never implied.

## Approval needed
User decision on whether to accept automated/local calculation evidence as the sprint gate, with Excel 365 regression deferred, consistent with the BUD approach.
