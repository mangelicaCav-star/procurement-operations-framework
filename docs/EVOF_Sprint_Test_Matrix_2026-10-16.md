# EVOF — Sprint 2026-10-16 | Functional Test Matrix v1.1

**Target:** `EVOF_Integrated_Procurement_Validated_v1_1.xlsx`  
**Baseline:** [Technical Validation Report v1.1](../EVOF_Technical_Validation_Report_v1_1.md)  
**Status:** TEST DESIGN CREATED; EXECUTION PENDING.  
**Test data:** fictional; work on a copy and preserve the published baseline.

## Objective
Verify that ERP-exported operational information, procurement data-quality checks and management indicators respond correctly to representative PO, supplier, approval and risk changes. Do not treat formula presence alone as a passed functional test.

## Scenarios and expected outcomes

| ID | Priority | Test | Expected outcome | Execution |
|---|---|---|---|---|
| T01 | P0 | Open PO due date earlier than `SETTINGS!B4` | `PO MASTER` Days Late = max(0, as-of date − original due date) | Not run |
| T02 | P0 | Open PO with future due date | Days Late = 0 | Not run |
| T03 | P0 | Received quantity equals ordered quantity | Open quantity = 0; open exposure = 0 | Not run |
| T04 | P0 | Received quantity exceeds ordered quantity | Invalid quantity/price exception and quality count increase | Not run |
| T05 | P0 | Duplicate existing PO ID | `DUPLICATE PO` flag and quality count increase | Not run |
| T06 | P0 | Unknown Supplier ID | `INVALID SUPPLIER` flag | Not run |
| T07 | P0 | Exported ERP PO approval status or date missing | EVOF flags missing or inconsistent source evidence for review; no PO status change | Not run |
| T08 | P0 | ERP export indicates requester and approver are identical | EVOF flags possible segregation-of-duties inconsistency for source verification; ERP owns authorization | Not run |
| T09 | P0 | ERP export lacks required second approval evidence | EVOF flags incomplete information against configured policy; no transactional blocking | Not run |
| T10 | P0 | Exported PO status is inconsistent with ERP approval evidence or authorized role metadata | EVOF reports a source-data inconsistency for investigation when sufficient fields exist; ERP exclusively authenticates users, enforces roles and changes PO status | Design dependency: ERP export fields |
| T11 | P1 | Add risk tied to an existing PO | Supplier scorecard risk count increases | Not run |
| T12 | P1 | ERP export omits approval evidence reference | EVOF quality exception increases; source PO status remains unchanged | Not run |

## System boundary (confirmed 2026-10-16)
EVOF is a procurement information-governance, integration and decision-support framework using controlled ERP exports. It is **not** a replacement ERP, an approval engine, or a transactional application. The ERP is authoritative for user permissions, PO creation, approvals and status transitions. EVOF may check export completeness, traceability, consistency and risks; it does not grant or deny permissions, approve POs, or change their status. Current workbook approval gates are illustrative advisory calculations and must not be represented as operative release controls.

## Execution protocol
For each scenario record: workbook copy/version, input cell(s) and original/new values, expected formula/output, observed result after Excel recalculation, PASS/FAIL/BLOCKED, screenshot or workbook evidence reference, and defect ID if applicable. Restore baseline values between scenarios. Distinguish formula inspection from execution in a calculation engine.

## Acceptance criteria
- P0 cases T01–T09 must pass with documented observed values for functional signoff; T10 is an ERP-export consistency requirement dependent on available approval/role metadata, not an EVOF permission-enforcement test.
- T11–T12 require documented observed results for extended coverage.
- No claim of reliable operational reporting without source ERP authorization assurance, export-field lineage, approval-evidence validation, receipt-event history, and ERP reconciliation.

## Planned sequence
1. **First activity:** test-case specification and baseline freeze (this document).
2. Run P0 PO integrity and lateness scenarios T01–T06.
3. Run P0 exported-approval-data consistency scenarios T07–T09; document T10 ERP metadata dependency.
4. Run supplier risk/evidence scenarios T11–T12.
5. Update the technical report with observed results and next-sprint defects.

## Dependencies
The GitHub baseline is available, but scenario execution requires a local test copy and a spreadsheet calculation engine. This document records test design only, not executed outcomes.
