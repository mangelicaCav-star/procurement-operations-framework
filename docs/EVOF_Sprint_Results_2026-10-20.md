# EVOF v0.4 — Local regression results | 2026-10-20

**Environment:** local artifact_tool spreadsheet calculation engine; Excel 365 deferred by user authorization. **Data:** synthetic. **Workbook:** `EVOF_MRP_Project_Cost_Decision_v0_4.xlsx`. Original workbook unchanged.

## Executed tests
| ID | Scenario | Observed | Result |
|---|---|---|---|
| R01 | Baseline incremental BOM | 60 components | PASS |
| R02 | FG-B 45 → 50 | Additional components 75 | PASS |
| R03 | MPS change → net shortage | 120 | PASS |
| R04 | MPS change → expedite cost | USD 4,750 | PASS |
| R05 | MPS change → project forecast | USD 24,750 | PASS |
| R06 | Restore MPS | 60 components / USD 3,970 | PASS |
| R07 | Inventory 90 → 110 | Net shortage 85 | PASS |
| R08 | Expedite ETA after need date | NO FACTIBLE | PASS |
| R09 | Simulated expedite confirmation | FACTIBLE CONFIRMADA / EVALUAR EXPEDITE | PASS for formula behavior; see R11 |
| R10 | Budget 25,000 → 23,000 | USD 970 over / ESCALAR PRESUPUESTO | PASS |
| R11 | FG-B 50; expedite qty 75; net shortage 120; earlier 45 unconfirmed | Coverage flag `SI` | **FAIL — business rule** |
| R12 | Restore original inputs | shortage 105 / expedite USD 3,970 / pending confirmation | PASS |

**Summary: 11 PASS / 1 FAIL.** The formulas recalculate, but passing formula behavior does not establish correct supply coverage.

## Open P0 defect — EVOF-040-01
`Alternativas!K2:K4` compare proposed purchase quantity to incremental BOM demand (`MRP_Cambio!B3`) instead of uncovered demand (`MRP_Cambio!B6`) adjusted for *confirmed, timely* prior recovery. At FG-B=50, proposed quantity 75 is less than uncovered need 120, yet coverage shows `SI`. At baseline, proposed 60 is less than uncovered 105. The prior 45-unit recovery is expressly unconfirmed.

**Required correction:** compute net uncovered quantity after confirmed, timely receipts/recoveries; compare candidate quantity against that gap; distinguish partial coverage from full coverage; prevent a simulated confirmation toggle from recommending an insufficient option. Retest no recovery, partial confirmed recovery, full recovery and late receipt.

## Sprint disposition
**NOT CLOSED**: P0 defect open. Excel 365 validation is deferred, not passed. V15 (MOQ/multiple deliveries/capacity) and V16 (actual project finance) remain out of tested scope. No live ERP, real supplier confirmation or production claims.
