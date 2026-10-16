# EVOF — Parking Lot / Design Opportunities

## PL-01 — Cross-project reuse and dynamic inventory policy
**Captured:** 2026-10-16  
**Status:** PARKED — not committed to current sprint implementation  
**Origin:** Functional architecture discussion for EVOF v2.0

### Hypothesis
Item master and min/max inventory decisions should reflect an item's cross-project reuse, replenishment frequency, actual and committed availability, lead time, projected demand and operational criticality. The purpose is to inform stocking decisions from ERP-derived data rather than duplicate ERP inventory transaction logic.

### Decision question
How should minimum stock, reorder point and target/max stock change for a component with long replenishment lead time (example: 10 months) and a replenishment index of 2, especially when it is reusable across multiple projects?

**Terminology dependency:** Define the unit and meaning of 'replenishment index = 2' before calculating anything (e.g. two replenishments per year, a score of 2, or two replenishment cycles). Do not infer the unit in the actual model.

### Candidate data inputs
- Item ID, unit of measure, category, obsolescence risk, substitutes.
- Cross-project reuse: number of qualifying projects, recurrence and expected future demand; distinguish number of projects from actual volume.
- On-hand stock, reserved/allocated stock, confirmed incoming receipts, open POs, available-to-promise by date.
- Supplier lead-time distribution and reliability, not only nominal lead time.
- Demand forecast and dated project requirements, uncertainty, usage frequency.
- Replenishment cadence, order constraints, MOQ, holding cost, cash limitations.
- Criticality, shortage cost, desired service level and alternative sourcing options.

### Candidate analysis
- Time-phased net availability and projected inventory position.
- Lead-time demand plus explicitly calculated safety stock: ROP = expected demand during lead time + safety stock (subject to policy and data quality).
- Reorder point distinct from minimum physical stock and maximum/target stock.
- Replenishment policy alternatives: hold buffer, order ahead, consolidate projects, alternate source, or accept managed risk.
- Sensitivity of the recommendation to cross-project reuse, 10-month lead time, lead-time variability, and replenishment index assumptions.
- Avoid arbitrary weighting without validated business objectives, costs and service-level targets.

### Validation / acceptance questions
1. What exactly does the replenishment index of 2 mean, and what time unit applies?
2. Does reuse reflect count of projects, probability of use, expected units or committed requirements?
3. Can we show how the recommended policy changes with lead time and demand?
4. Are incoming orders and project reservations correctly netted to prevent double-counting?
5. Does the recommendation disclose shortage, excess/obsolete and working-capital trade-offs?

### Disposition
Backlog candidate for a future EVOF inventory decision-model sprint. Current sprint remains focused on the first supply-continuity use case and minimum ERP-export data architecture.
