# EVOF — Technical Validation Report (v1.1)

**Date:** 2026-10-15  
**Scope:** `EVOF_Integrated_Procurement_Governance_Controls.xlsx`  
**Output:** `EVOF_Integrated_Procurement_Validated_v1_1.xlsx`  
**Status:** **PARTIALLY VALIDATED — prototype, not production-certified**

## Method

Inspected worksheet structures, stored Excel formulas, sample PO and risk records, data links, approval rules, and summary calculations. Applied targeted formula corrections and additional data-quality checks to a separate copy. Verified the exported XLSX archive opens as a structurally valid ZIP package and that corrected formulas are present across intended ranges. **Full Excel-engine recalculation and exhaustive interactive scenario testing were not performed.** Values should be recalculated and reviewed in Microsoft Excel.

## Findings and actions

| ID | Severity | Finding | Action in v1.1 | Residual limitation |
|---|---|---|---|---|
| V-01 | High | `PO MASTER!P4:P103` Days Late measured elapsed days since PO issue (`F`) instead of promised due date (`G`). | Formula now uses `MAX(0, As-of Date - Original Due)` for open POs. | Completed PO lateness is not measurable without actual receipt date. |
| V-02 | High | Approval Release Gate verifies approval decision/name/date but **does not verify the approver's assigned role or authenticated identity**. | Explicit warning retained; no false claim of role validation. | Requires role directory, permissions and enforced release workflow. |
| V-03 | Medium | Supplier Scorecard risk count formula only examined the first ten POs and five risks. | Expanded source ranges to 100 PO/risk rows. | Needs recalculation in Excel; design assumes one PO record per PO ID. |
| V-04 | Medium | PO data-quality checks did not cover duplicate IDs, invalid quantities, negative prices or missing/inconsistent dates. | Extended `PO MASTER!X4:X103` checks and `DATA QUALITY` summary. | Advisory only; does not prevent entry or external PO release. |
| V-05 | Medium | Duplicate supplier, risk and approval IDs and RFQ supplier references were not checked in Data Quality. | Added checks in `DATA QUALITY!D8:D11`. | Some other identifiers and cross-record invariants remain manual. |
| V-06 | Medium | Approval evidence may be missing even when release gate is eligible. | Added evidence-missing count in `DATA QUALITY!D12`. | Release Gate itself still does not enforce evidence. |
| V-07 | Medium | `DATA QUALITY!D5` subtracts release-eligible approval rows from PO count; duplicate approval records can distort the measure. | Duplicate approval-ID count added. | PO-to-approval cardinality and duplicate PO reference checks still needed. |
| V-08 | Medium | Supplier and RFQ names/IDs are linked only by limited Excel checks; no transactional database constraints. | Existing ID checks retained. | Referential integrity not technically enforced. |

## Recommended scenario tests in Microsoft Excel

1. **Overdue PO:** Choose an open PO, set original due before `SETTINGS!B4`, verify `Days Late` equals the difference in days.
2. **Future PO:** Set original due after `SETTINGS!B4`, verify `Days Late = 0`.
3. **Closed PO:** Set received quantity equal to ordered quantity, verify open quantity and open exposure are zero; do not interpret Days Late as historic OTD.
4. **Overreceipt:** Set received quantity above ordered quantity; verify `INVALID QTY/PRICE` appears in `PO MASTER!X` and the Data Quality exception count increases.
5. **Duplicate PO:** Duplicate an existing PO ID in a new row; verify `DUPLICATE PO` and duplicate counter.
6. **Unknown supplier:** Replace a Supplier ID with an unrecognized value; verify `INVALID SUPPLIER`.
7. **Approval missing:** Leave decision or date blank; verify `HOLD`.
8. **Self-approval:** Set primary approver equal to requestor; verify `HOLD`.
9. **Secondary approval:** For a two-signature PO, leave secondary approval blank; verify `HOLD`.
10. **Unauthorized role:** Enter an approver with the wrong role. **Current workbook cannot detect this; must remain a known failed control.**
11. **Supplier scorecard expansion:** Add a new risk for an existing PO and verify the supplier risk count changes.
12. **Evidence omission:** Mark an approval eligible without an evidence reference and confirm the new Data Quality count increases.

## Interpretation and release criteria

- **Suitable for:** a clearly labeled independent portfolio prototype demonstrating process design, decision support, formula-driven controls and governance requirements.
- **Not suitable for:** real procurement authorizations, financial commitments, regulatory audit evidence, or automated operational reporting without additional development and testing.
- **Before labeling fully validated:** recalculate in Microsoft Excel; execute the scenario tests; add actual receipt records; enforce role authorization and approval evidence; verify all ID uniqueness and referential checks; document test outcomes and version history.

All sample suppliers, orders and individuals are fictional. The original workbook was not overwritten.
