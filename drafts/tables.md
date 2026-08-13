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
| Corpus versions grounding the encoding | 138 (47 FR + 44 HTS + 47 notes) |

## Table 2 — Entries pipeline validation (§6)

Sources: `microcosm@d4b0855157af996bd367146bc200a2f72ee7d15d:docs/evidence/us-import-entry-margins/`
(build report, reconciliation records, and cross-check report); generator
code at `microcosm@6707ed5912d33ff0a340474a1a24f31546c6dec5` and the
local, P1-authenticated validation receipt with sha-256
`45276e944ff8cb6680e50ba27238d68a5b37da09b0d860db2ccfbd577ec5a03e`,
pending archival inclusion.

| Check | Result |
|---|---|
| Source archives (2025-01…2026-06) | 18, ~3.3 GB, all sha-256 manifested |
| Full-grain detail rows (HTS-10 × country × subcode × entry district × unlading district × rate provision × month) | 38,841,305 |
| District-aggregated margin cells (HTS-10 × country × month) | 3,070,851 |
| Consumer facts published (5 grains) | 302,318 |
| Exact-integer reconciliation vs publisher control totals | 3 axes × 18 months: **0 failures** |
| Cross-check vs second official channel (API) | 108,977 cells, 16 pairs: **0 mismatches** |
| Generator identity, all-line pilot window 2026-02…06 | $1,467,109,590,515 weighted = margins total exactly |
| Spatially unrestricted pilot allocation rows / weighted entries | 3,806,050 / 44,881,145 |
| Informal-share proxy calibration (σ = 2.6916) | share Δ 2.6×10⁻⁵; mean $32,689 vs $32,916 anchor |

## Table 3 — Tracker decomposition, April–June 2026 daily means (§4)

Both legs
run Yale's daily-series stage on Yale's built panel (`c4307e51`),
identical except the import-weights file; weight bases built with
Yale's own recipe over sha-manifested Census import archives.

| Series | Weight base | Mean rate |
|---|---|---|
| Yale, published | 2024 (theirs) | 11.08% |
| Rerun leg | 2024 (rebuilt, \$3,119.3B) | 10.72% |
| Rerun leg | 2025 (rebuilt, \$3,242.5B) | 9.38% |
| TPC, published | 2025 (theirs, ex-AD/CVD) | 9.46% |

Weight-vintage effect −1.34 points; residual against TPC 0.08 points.
All four rows are unweighted means over the 91 calendar days
2026-04-01 through 2026-06-30. Sources: Yale published series at their
2026-06-09 release; TPC all-goods series from the published Datawrapper
feed (aO4iG, version 44); rerun legs committed as
`data/pe/diagnostics/daily_overall_weights{2024,2025}.csv`
[@scorecard_repo] at `f9e7acf`. The validation leg (2024 base) tracks the published
Yale series within 0.2–0.6 points in months containing no schedule
revision and sits 0.36 points below it on the window mean; the
departure is consistent with publication vintage and single-pass
versus per-revision weight keying, acting in opposite directions.
