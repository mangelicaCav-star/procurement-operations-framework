# EVOF — MRP Project Cost Decision | Validation Report v0.4

**Date:** 2026-10-16. **Disposition:** PARTIALLY VALIDATED — arithmetic and static scenario consistency only.

## Evidence reviewed
Local workbook `EVOF_MRP_Project_Cost_Decision_v0_4.xlsx` contains worksheets Guia, Parametros, Proyectos, MRP_Cambio, Alternativas, Control_Decision, Pruebas. Its Pruebas worksheet records **13 PASS (V01–V13)** and **3 NOT RUN (V14–V16)**. The results were inspected against the workbook values and independently cross-checked for the core arithmetic; **do not interpret this as a full Excel recalculation test**.

| Check | Expected / observed | Result |
|---|---|---|
| FG-B 25→45 | +20 FG | Arithmetic PASS |
| BOM ×3 | +60 components | Arithmetic PASS |
| Oct 30 gross requirement | 135 components | Arithmetic PASS |
| Availability after Oct 23 | 30 components | Arithmetic PASS |
| Oct 30 cumulative uncovered need | 105 components | Arithmetic PASS |
| Earlier 45-unit proposed expedite | 60 conditional additional units; 45 not confirmed | Scenario consistency PASS |
| Existing PO ETA Nov 5 | Does not cover Oct 30 need | Date comparison PASS |
| Expedite ETA Oct 29 | Before due date; not supplier confirmed | Date comparison PASS |
| Standard incremental material | 60 × $52 = $3,120 | Arithmetic PASS |
| Expedite total | $3,120 + $850 = $3,970 | Arithmetic PASS |
| Alternate total | 60 × $64 + $300 = $4,140 | Arithmetic PASS |
| Wait total | $3,120 + assumed $2,000 = $5,120 | Arithmetic PASS |
| Project forecast expedite | $20,000 + $3,970 = $23,970 | Arithmetic PASS |

## Not run / not demonstrated
- V14: edit inputs and verify live recalc in Microsoft Excel.
- V15: MOQ, multiple deliveries, dynamic supplier capacity.
- V16: actual project financial data and real-world costing.
- No independent end-to-end regression showing a changed MPS automatically propagates through the v0.4 cost decision workbook; this is **not** claimed.
- No confirmed supplier lead times, approvals, plant schedules or ERP connection.
- Cross-project inventory and cost allocation remain untested.

## Decision
The model supports a **conditional** preference for expedite ($3,970) over alternate ($4,140) or waiting ($5,120) **under the stated synthetic assumptions**. The $1,150 difference versus waiting depends on a hypothetical delay cost. No purchase order should be executed based on this pilot. A real recommendation requires supplier and project-owner confirmation.

## Release gate
Before marking v0.4 functionally validated: execute Excel recalc tests after MPS, dates, quantity and cost changes; validate no double-counting and budget baseline; test unconfirmed supply; test infeasible dates; obtain documented reviewer sign-off.
