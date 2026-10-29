# EVOF — evidence and publication review, 29 October 2026

## Finding and correction

GitHub's README still described simulator 1.0 and alignment as future work, although the private simulator 1.1 was deployed later on 26 October. The portfolio already cited its 56 cases. This review corrects public documentation to match the actual deployed implementation and retains the older evidence as history.

## Verified implementation

- Deployed simulator 1.1 source: `1d81473187489025282a0bf78a4bc4ae20b06f76`, hosting version 2. URL: https://evof-decision-simulator.humblerobin2048.chatgpt.site.
- Version ID: `appgprj_6ada7c9900208191b1e396338e8f0a11~appgver_cd0b091f76d08191af8ad45030989e97`.
- **56/56 JavaScript cases PASS**, rerun on that exact clean checkout: 38 historical and 18 corrective. [Results](../validation/EVOF_Simulator_1_1_Results_2026-10-29.json).
- Existing browser QA dated 26 October records tie, missing price, missing dates, eligible lower-cost alternate, unknown baseline and save/load checks. It is historical evidence, not a fresh browser run or user approval.
- Published workbook v0.4.2 remains unchanged, SHA-256 `ec22fb39cbf5208a7fb43fedb9759c160e043301c1c5a8bd1edaefc1610acded`. Its 51 local checks are separate from the 56 simulator cases. No new native workbook execution occurred in this review.

## Open exception requiring focused work

The approved business premise defines available inventory as usable physical stock not allocated elsewhere. An open supplier PO is a commitment from issue, not physical inventory; its value is already included in project commitments, with workbook B23 informative. The deployed simulator still exposes its earlier committed-material credit extension. In the current test, credit 1000 reduces the default expedited forecast to 25310; baseline without that extension is 26310. This passing legacy extension case is not evidence that the later premise is implemented.

Therefore do not assert general workbook/simulator parity or complete protection against double counting for this scenario. The next bounded correction must first map baseline commitments, existing PO receipts and genuinely additional purchase costs, then demonstrate that each is counted once. No new cost rule, source import or functional redesign was implemented in this documentation review.

The native lower-cost workbook comparison remains setup-qualified in the published evidence and requires explicit reconfirmation with both alternatives eligible; JavaScript results do not close it. MOQ/capacity, reallocation and other preserved prototype extensions are simulator-only unless separately evidenced in the workbook. Full v2.0 and production remain unimplemented.

The guide now starts with current 1.1 information and labels original 1.0 material as historical, preserving lineage.

## Cross-project publication and scope

The existing public portfolio was refreshed: https://angelica-martinez.humblerobin2048.chatgpt.site, source commit `c1243bc0a6aaa3a373bf0a33fa60b59819b5ef28`, hosting version 5. Both full simulators retain owner-only access. No simulator source/assets were added to public GitHub.

The BUD public example now distinguishes current authorized sale, total supplier PO/budget and original-currency dated invoices. Its 16 Node model/markup checks (including unchanged public EVOF decision checks) passed. Static IDs/local links and syntax passed. Counts are separate from private-simulator suites. Browser QA attempted on 29 October failed at CUA kernel startup (read-only session-directory error), so no fresh visual or interaction execution is claimed. Historical browser evidence remains dated and separate. Public example is deliberately smaller than either private simulator.

No ERP/provider/Finance real-data validation, full native regression, authenticated approval, production certification, EVOF–BUD integration, multi-entity purchasing, agents or parked functions were added. The next development action is a bounded correction/verification of an identified discrepancy, not expansion of functionality. Naming/version convention and a modification/correction memory remain methodology parking-lot items; reuse the existing decision record and avoid parallel logs. No renaming policy was implemented.

Review was advanced with explicit user authorization on 29 October; no recurring automation was created or rescheduled.

