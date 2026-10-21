# EVOF v0.4.1 — Coverage logic correction and regression

**Environment:** local artifact_tool calculation engine. **Excel 365:** deferred. **Dataset:** synthetic. **Publication:** corrective workbook uploaded to GitHub on 2026-10-21; regression originally executed locally.

## EVOF-040-01 correction
Previously the candidate purchase quantity and coverage check referenced incremental BOM demand (`MRP_Cambio!B3`) instead of net uncovered demand. The corrected local workbook introduces `Parametros!B24` (confirmed recovery quantity), `B25` (confirmed receipt date), `B26` (verified confirmation indicator). `MRP_Cambio!B7` counts only confirmed, timely recovery (capped by uncovered demand); `B8` calculates remaining gap. Candidate quantities in `Alternativas!B2:B4` reference `B8`, and `K2:K4` compare candidate quantity to that gap. When gap is zero, coverage flag is NO to avoid unnecessary procurement. Date, approval and budget gates remain separate.

## Regression results
**13/13 local checks PASS:** baseline shortage 105; baseline candidate 105; no automatic confirmation; MPS FG-B 45→50 produces gap 120 and candidate 120; unconfirmed 45 ignored; confirmed timely 45 reduces gap to 60; late 45 ignored; partial confirmed 20 reduces gap to 85; confirmed 105 reduces gap to zero and blocks unnecessary procurement; simulated expedite confirmation with over-budget cost escalates; late expedite rejected; baseline restoration yields gap 105 and expedite USD 6,310.

## Baseline financial implications
- No verified prior recovery: expedite 105 × USD 52 + USD 850 = **USD 6,310**; project forecast USD 20,000 + USD 6,310 = **USD 26,310**, budget USD 25,000, over by USD 1,310.
- With confirmed timely 45-unit recovery: 60 × USD 52 + USD 850 = **USD 3,970**; project forecast **USD 23,970**. Original lower cost depended on unconfirmed recovery.
- Costs of prior recovery must be reconciled against the entered project baseline to prevent double counting.

## Remaining limitations
These 13 tests validate modeled formula propagation and gating in the local engine, **not** real supplier confirmation, Excel 365, ERP/MRP integration, MOQ, split deliveries, capacity or actual financials. The candidate quantity is set equal to the modeled uncovered need, not independently limited by supplier capacity.

**Disposition:** EVOF-040-01 resolved for modeled synthetic cases; **provisional local prototype sprint closure** only, not production release. Excel 365 deferred. The corrected workbook was subsequently [uploaded to GitHub on 2026-10-21](EVOF_MRP_Project_Cost_Decision_v0_4_1_Coverage_Corrected_LOCAL.xlsx).
