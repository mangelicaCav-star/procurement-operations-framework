# EVOF Sprint Log — 2026-10-16

## Sprint objective and pivot
Original objective: v2.0 information architecture and supply-continuity pilot. Mid-sprint, narrowed the first domain-specific use case to **MRP Buyer / Buyer-Planner decision support**. Further pivot: prioritize **project-level economic and operational evaluation** of supply recovery options over creating a transactional MRP tool.

## Completed / supported
- Functional scope v2.0 and information architecture v2.0 documented earlier in repository.
- Synthetic MPS/BOM example and quantity-change simulation prepared.
- MPS FG-B 25→45: +20 FG, +60 components; 30-Oct requirement 135, available 30, shortage 105. Earlier proposed expedite 45 remains unconfirmed.
- v0.4 workbook with three alternatives and PRJ-200 budget scenario prepared.
- 13 static/arithmetic validation cases PASS as recorded in workbook; 3 NOT RUN.
- This sprint log, decision methodology and validation report prepared for repository.

## Architecture and governance decisions
1. EVOF consumes authorized ERP/MRP data and produces analytical scenarios, not POs, ERP approvals or inventory transactions.
2. Evaluate every recovery alternative by cost, project budget, dates and feasibility; compare waiting versus intervening.
3. Separate original need, MPS-change incremental need, proposed supply and confirmed supply.
4. Track assumption provenance and do not confuse a simulated cost or supplier date with a validated commitment.
5. Preserve prior versions as historical prototypes; do not label v0.4 production-ready.

## Open / backlog
- Run Excel-engine change propagation regression (MPS→BOM→shortage→alternatives→budget).
- Confirm supplier feasibility rules and plant calendar assumptions.
- Model shared inventory, cross-project allocation and budget impacts (v0.5).
- Validate MOQ, partial shipments, quote premiums, production replan costs and source lineage.
- Publish binary workbook separately when supported; these documentation commits do not imply workbook upload.

## Sprint disposition
**Documentation completed; prototype partially validated; functional release gate remains open.**
