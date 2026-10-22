# EVOF Simulator 1.0 — Validation record | 2026-10-22

**Result:** 38/38 PASS. Fixed expectations were evaluated against the same JavaScript engine used by the private simulator. These are deterministic regression checks, not independently audited business outcomes.

**Private deployment:** [EVOF simulator](https://evof-decision-simulator.humblerobin2048.chatgpt.site). **Private source revision:** `7040f775ccd5f0482ee86688570d1232fe67e1c2`. Source code remains outside this public repository. The revision identifies the deployed implementation; it is not a public GitHub commit link. The test definitions were rerun during this documentation update on 22 October 2026 without changing the engines.

## Reference cases

| ID | Flow | Expected behavior | Engine result |
|---|---|---|---|
| EVOF-SIM-01 | MPS explosion | 25 → 45 produces 60 additional components | PASS |
| EVOF-SIM-02 | Gross requirement | 75 + 60 = 135 pieces | PASS |
| EVOF-SIM-03 | Shared inventory | 90 − 60 = 30 remaining | PASS |
| EVOF-SIM-04 | Corrected coverage | 135 − 30 = 105 uncovered | PASS |
| EVOF-SIM-05 | Default expedite cost | 105 × $52 + $850 = $6,310 | PASS |
| EVOF-SIM-06 | Default project forecast | $20,000 + $6,310 = $26,310 | PASS |
| EVOF-SIM-07 | Unconfirmed recovery | 45 proposed pieces do not reduce the shortage | PASS |
| EVOF-SIM-08 | Missing recovery evidence | Confirmation alone does not qualify the recovery | PASS |
| EVOF-SIM-09 | Late recovery | Confirmed Nov 5 recovery does not cover Oct 30 | PASS |
| EVOF-SIM-10 | Timely recovery | 45 confirmed pieces leave 60 uncovered | PASS |
| EVOF-SIM-11 | Partial recovery | 20 confirmed pieces leave 85 uncovered | PASS |
| EVOF-SIM-12 | Full recovery | 105 confirmed pieces suppress additional supply | PASS |
| EVOF-SIM-13 | Recovery is capped | Excess recovery cannot create a negative shortage | PASS |
| EVOF-SIM-14 | MPS reduction | 25 → 20 revised units releases 15 components | PASS |
| EVOF-SIM-15 | No MPS change | Zero incremental BOM does not erase the baseline shortage | PASS |
| EVOF-SIM-16 | Confirmation gate | On-time estimate never becomes confirmed feasibility | PASS |
| EVOF-SIM-17 | Budget escalation | Confirmed expedite still exceeds the $25,000 budget | PASS |
| EVOF-SIM-18 | Budget boundary | Exact budget fit remains a candidate | PASS |
| EVOF-SIM-19 | Late supply | Every late option routes to impact management | PASS |
| EVOF-SIM-20 | Alternate qualification | A confirmed alternate requires separate qualification | PASS |
| EVOF-SIM-21 | Timely existing receipt | 40 verified pieces reduce the requirement once | PASS |
| EVOF-SIM-22 | Partial existing PO | 40 late pieces leave 65 unresolved | PASS |
| EVOF-SIM-23 | Committed material credit | Already committed material is counted only once | PASS |
| EVOF-SIM-24 | MOQ / order multiple | 105 pieces round to 120 with 20-piece multiples | PASS |
| EVOF-SIM-25 | Capacity cap | A 50-piece offer retains a 55-piece residual | PASS |
| EVOF-SIM-26 | Origin protection | Late replenishment blocks a transfer | PASS |
| EVOF-SIM-27 | Replenishment confirmation | A timely replacement estimate alone does not confirm a transfer path | PASS |
| EVOF-SIM-28 | Confirmed replenishment | Transfer and replacement evidence make the full path a candidate | PASS |
| EVOF-SIM-29 | Documented mitigation | An approved recovery path can conditionally protect origin | PASS |
| EVOF-SIM-30 | Allocation reconciliation | 75/25 split keeps enterprise spend at $5,660 | PASS |
| EVOF-SIM-31 | Origin budget gate | Receiving-project savings cannot hide an origin overrun | PASS |
| EVOF-SIM-32 | Replenishment boundary | Transfer LEAD protects the earlier replacement decision | PASS |
| EVOF-SIM-33 | Urgent vs schedulable | Expedite has one day; a 5-day supplier has nine | PASS |
| EVOF-SIM-34 | At-boundary action | A 14-day expedite is actionable immediately | PASS |
| EVOF-SIM-35 | Invalid inputs | Negative MPS blocks decisions | PASS |
| EVOF-SIM-36 | Invalid dates | Impossible dates block calculations | PASS |
| EVOF-SIM-37 | Prior stock deficit | Uncovered prior consumption carries forward | PASS |
| EVOF-SIM-38 | Recovery cost retention | Recovery cost remains visible even when supply is covered | PASS |

## What this evidence establishes

The outcomes above exercise scenario arithmetic, explicit missing-data/confirmation gates, boundary conditions and the bounded decisions implemented in this simulator. Expected values are fixed test assertions; the report records PASS/FAIL rather than claiming independent source-document reconciliation. The owner can rerun these fixed checks in the simulator's Validation view. Scenario save/load and user-input behavior were checked separately through browser interaction before deployment.

## Evidence layers remain separate

- Simulator: 38 current JavaScript regression checks and scoped browser interaction QA.
- Corrected workbook: 13 prior synthetic local coverage checks; [7 Excel 365 checks reported by the user](EVOF_Excel365_Validation_Status_2026-10-21.md). The desktop submission did not include observed cell values, screenshots or an independently witnessed execution.
- Still open: operational acceptance of extensions; real supplier confirmation, capacity and dates; production-calendar and split-supply behavior; source-to-finance reconciliation; the separate integrated governance v1.1 workstream and broader architecture requirements.

No workbook binary is replaced or released by this report. No production readiness, realized savings, authoritative financial reporting or BUD–EVOF integration is claimed. The next functional gate is the owner's scenario review and cross-artifact reconciliation, with differences resolved or explicitly accepted.

## Engine file fingerprints

These SHA-256 values identify the privately retained engine and case definitions without publishing their code.

| Private source file | SHA-256 |
|---|---|
| `dist/model.js` | `6b44e5e4d615f2b079372d41bb90d0fa74893a66c1f2439cf4f3df7e648fbad7` |
| `dist/validation.js` | `5b789220d0ee49f660133232a71c697b920badc59aa0a29cf172257100eba0a7` |
