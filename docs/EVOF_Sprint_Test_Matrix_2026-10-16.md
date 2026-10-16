# EVOF — Sprint 2026-10-16 | Functional Test Matrix v1.1

**Target:** `EVOF_Integrated_Procurement_Validated_v1_1.xlsx`  
**Baseline:** [Technical Validation Report v1.1](../EVOF_Technical_Validation_Report_v1_1.md)  
**Status:** TEST DESIGN CREATED; EXECUTION PENDING.  
**Test data:** fictional; work on a copy and preserve the published baseline.

## Objective
Verify that operational exceptions, procurement controls and management indicators respond correctly to representative PO, supplier, approval and risk changes. Do not treat formula presence alone as a passed functional test.

## Scenarios and expected outcomes

| ID | Priority | Test | Expected outcome | Execution |
|---|---|---|---|---|
| T01 | P0 | Open PO due date earlier than `SETTINGS!B4` | `PO MASTER` Days Late = max(0, as-of date − original due date) | Not run |
| T02 | P0 | Open PO with future due date | Days Late = 0 | Not run |
| T03 | P0 | Received quantity equals ordered quantity | Open quantity = 0; open exposure = 0 | Not run |
| T04 | P0 | Received quantity exceeds ordered quantity | Invalid quantity/price exception and quality count increase | Not run |
| T05 | P0 | Duplicate existing PO ID | `DUPLICATE PO` flag and quality count increase | Not run |
| T06 | P0 | Unknown Supplier ID | `INVALID SUPPLIER` flag | Not run |
| T07 | P0 | Approval decision or date missing | Release gate = HOLD | Not run |
| T08 | P0 | Primary approver equals requestor | Release gate = HOLD | Not run |
| T09 | P0 | Required secondary approval absent | Release gate = HOLD | Not run |
| T10 | P0 | Approver has unauthorized role | **Known control gap:** workbook does not authenticate roles; must not pass | Known gap; not remediated |
| T11 | P1 | Add risk tied to an existing PO | Supplier scorecard risk count increases | Not run |
| T12 | P1 | Eligible approval missing evidence reference | Data Quality missing-evidence count increases | Not run |

## Execution protocol
For each scenario record: workbook copy/version, input cell(s) and original/new values, expected formula/output, observed result after Excel recalculation, PASS/FAIL/BLOCKED, screenshot or workbook evidence reference, and defect ID if applicable. Restore baseline values between scenarios. Distinguish formula inspection from execution in a calculation engine.

## Acceptance criteria
- P0 cases T01–T09 must pass with documented observed values for functional signoff; T10 remains an explicitly accepted *known control gap*, not a passed test.
- T11–T12 require documented observed results for extended coverage.
- No claim of production readiness without approver identity/role enforcement, evidence validation, receipt-event history, and ERP reconciliation.

## Planned sequence
1. **First activity:** test-case specification and baseline freeze (this document).
2. Run P0 PO integrity and lateness scenarios T01–T06.
3. Run P0 approval scenarios T07–T09; document T10 control gap.
4. Run supplier risk/evidence scenarios T11–T12.
5. Update the technical report with observed results and next-sprint defects.

## Dependencies
The GitHub baseline is available, but scenario execution requires a local test copy and a spreadsheet calculation engine. This document records test design only, not executed outcomes.
