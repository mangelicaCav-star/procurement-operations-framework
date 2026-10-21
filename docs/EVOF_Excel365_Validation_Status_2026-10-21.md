# EVOF v0.4.1 — Excel 365 validation results | 2026-10-21

**Workbook:** [EVOF v0.4.1 Coverage Corrected](EVOF_MRP_Project_Cost_Decision_v0_4_1_Coverage_Corrected_LOCAL.xlsx)

**Evidence provenance:** user-reported results from Microsoft Excel 365 desktop. No screenshots, actual cell values, workbook execution log, or independently witnessed desktop run supplied. The previous submission reported all tests NOT RUN; this later submission supersedes it for execution status.

| Test | Purpose | Reported result |
|---|---|---|
| EV-01 | Baseline uncovered need | PASS |
| EV-02 | FG-B MPS 45 to 50 and shortage propagation | PASS |
| EV-03 | Restore FG-B baseline | PASS |
| EV-04 | Ignore unconfirmed prior recovery | PASS |
| EV-05 | Count confirmed timely prior recovery | PASS |
| EV-06 | Exclude late recovery | PASS |
| EV-07 | Restore baseline cost and forecast | PASS |

**Summary:** 7 PASS / 0 FAIL / 0 NOT RUN (user-reported). No new defects reported. Prior EVOF-040-01 (coverage comparison against incremental demand rather than net uncovered need) is corroborated as corrected within the tested scenarios. Separate local automated regression: 13/13 PASS.

**Disposition:** functional sprint acceptance for the defined Excel 365 scenarios; no independent verification of user-reported observed values. The workbook is a synthetic portfolio prototype, not a production-certified planning or financial system. MOQ, supplier capacity, split deliveries, actual ERP integration, supplier confirmations and real project finance remain outside validated scope.
