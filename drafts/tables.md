# Tables (wire into sections at final assembly)

## Table 1 — Conformance scoreboard at the pinned snapshot (§3)

Sources: comparison report
`axiom-oracles@dc1da3af067c50fa7138458faf3703b4b9efd7cb:reports/axiom-yale-us-tariff-panel-all-2026-08-03.json`;
authoritative dispositions
`axiom-oracles@dc1da3af067c50fa7138458faf3703b4b9efd7cb:dispositions/us-tariff-panel.yaml`;
reference Budget-Lab-Yale/tariff-rate-tracker @ `c4307e51`.

| Quantity | Value |
|---|---|
| Witness slice | 5 HTS-10 lines × 240 partners × 57 intervals |
| In-scope interval-cells | 68,400 = 20,400 covered + 48,000 temporal debt |
| Probe-date comparisons | 39,600 (33 probes per line-partner) |
| Exact matches / mismatches (raw) | 24,400 / 15,200 (61.6% raw) |
| Authoritative disposition partition | 30 entries: 10 / 8,283 upstream-engine-gap + 20 / 6,917 explained-residual = 15,200 units |
| In-scope policy records with `covered: true` | 10 / 10 |
| Unexplained disagreements | 0 |
| Open disagreements attributed to the encoding | 0 |
| Tripwired scope exclusions | 4 |
| Reference-attributed units, classified with evidence | 8,283 |
| Boundary-straddle clip events recorded | 1,200 |
| Comparison-harness tests at close | 2,396 |
| Corpus versions grounding the encoding | 138 (47 FR + 44 HTS + 47 notes) |
| Reference build, measured | 6,368 s wall; 123.4 GiB peak footprint |

## Table 2 — Entries pipeline validation (§5)

Sources: build report + reconciliation records + cross-check report,
committed in-branch (microcosm #620); generator validation report
(microcosm #621).

| Check | Result |
|---|---|
| Source archives (2025-01…2026-06) | 18, ~3.3 GB, all sha-256 manifested |
| Detail rows parsed | 38,841,305 |
| Margin cells (HTS-10 × country × district × month) | 3,070,851 |
| Consumer facts published (5 grains) | 302,318 |
| Exact-integer reconciliation vs publisher control totals | 3 axes × 18 months: **0 failures** |
| Cross-check vs second official channel (API) | 108,977 cells, 16 pairs: **0 mismatches** |
| Generator identity, pilot window 2026-02…06 | $1,467,109,590,515 weighted = margins total exactly |
| Pilot entry rows / weighted entries | 3,806,050 / 44,881,145 |
| Informal-share proxy calibration (σ = 2.6916) | share Δ 2.6×10⁻⁵; mean $32,689 vs $32,916 anchor |
| Adversarial review at merge | P1: 12 rounds ending APPROVE, no findings; P2: 4 rounds ending APPROVE |
| Trade test battery at merge | 149 |
