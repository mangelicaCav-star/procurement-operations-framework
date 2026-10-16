# EVOF — MRP Buyer Decision Support | Pilot v0.2

**Date:** 2026-10-16  
**Status:** Excel formula prototype created; functional tests NOT EXECUTED  
**Positioning:** Procurement planning and decision support, not an ERP/MRP replacement.

## Purpose
Demonstrate the distinction between purchasing execution and production-linked material planning. EVOF interprets production requirements, a simplified BOM, usable inventory and scheduled receipts to identify supply exceptions and compare buyer actions. ERP transactions remain authoritative.

## Simulated scenario
- MPS: 30 FG-A due 2026-10-23; 25 FG-B due 2026-10-30; 20 FG-A due 2026-11-06.
- BOM: FG-A consumes 2 units of ITM-001; FG-B consumes 3 units.
- Inventory: 100 physical units, 10 reserved externally, **90 usable**.
- Scheduled receipt: 40 units due 2026-11-05.
- Component gross demand: 60 on Oct 23, 75 on Oct 30, 40 on Nov 6.
- First period ending Oct 23: projected 30 available.
- Oct 30: net requirement **45**; original receipt is not due until Nov 5.
- Illustrative mitigation: expedite 45 units by Oct 29 or use a qualified alternative supplying 45 by Oct 28.

## Analytical calculations
- Gross requirements = sum(MPS finished-goods quantities × BOM quantity per FG), by requirement date.
- Net requirements = MAX(0, gross requirements + safety stock − opening available − scheduled receipts). The prototype assumes the net requirement is supplied in that same period when calculating the projected ending balance.
- Planned release date = required date minus lead-time calendar days. **No working-day calendar, order multiples, MOQ, lot sizing, multi-level BOM, scrap, yield, pegging, demand changes, partial schedules or supplier capacity checks** are modeled.
- Buyer option evaluation: arrival date vs shortage date; covered quantity; residual shortfall; incremental cost plus assumed shortage-impact cost.
- The modeled USD 120 per short unit is **a hypothetical comparison input**, not a validated financial loss estimate.

## Scope and limitations
The Excel workbook contains MPS, BOM, Inventory, Receipts, MRP_Semanal, Alternativas, Supuestos, Decision and Pruebas. Source data is simulated. A working ERP connector is not included. Formulas were authored, but results and recalc have not been independently tested in an Excel calculation engine. All test statuses are NOT RUN. A calculated planned order is **not an actual PO**. Supplier qualification and delivery commitments require external verification.

The option comparison currently targets the Oct 30 shortage, not every future period. It is an initial focused decision demonstration; it is not a complete constrained supply plan.

## Acceptance tests to execute
1. Confirm BOM explosion: FG-A × 2; FG-B × 3.
2. Confirm gross requirements of 60 (Oct 23), 75 (Oct 30), and 40 (Nov 6).
3. Confirm 90 usable units and 45 net requirement on Oct 30.
4. Confirm Nov 5 PO receipt is not treated as available on Oct 30.
5. Confirm a delivery after Oct 30 does not resolve the Oct 30 shortfall.
6. Confirm expedite or alternate supply of 45 before Oct 30 reduces the shortfall to zero.
7. Change MPS demand and verify dependent requirements update.
8. Test a later/partial receipt and verify the date-based projection.
9. Confirm assumptions and financial impact are labeled as hypothetical.
10. Verify the model does not write back ERP transactions.

## Future extensions
- Import actual ERP MRP exception messages and explain root causes.
- Add inventory allocation and time-phased pegging to project demand.
- Evaluate expedite/de-expedite, excess and obsolescence, lead-time uncertainty.
- Implement PL-01 separately: cross-project reuse, replenishment frequency and dynamic min/max policy.

**Artifact:** `EVOF_MRP_Buyer_Pilot_v0_2.xlsx` (generated as a downloadable working file; not yet committed to this repository).
