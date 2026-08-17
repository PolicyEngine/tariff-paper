# 4. Why the two public trackers disagree with each other

Two organizations publish daily average United States tariff rates
from independent pipelines: Yale Budget Lab's tracker
[@yaletracker_repo] and the Tax Policy Center's tariff series
[@tpctracker]. Over April–June 2026 their headline series sit 1.6
percentage points apart — Yale's weighted effective statutory rate
averages 11.08 percent, TPC's all-goods series 9.46 percent. Both numbers circulate in policy discussion, and we find no published
reconciliation from either organization.

Most of the gap — 1.34 of the 1.62 points — is the weight vintage.
We reran Yale's daily-series stage on
their own built rate panel (repository state `c4307e51`, built
locally), twice, identical in every respect except the import-weights
file. Both weight bases come from Yale's own recipe — their
`build_import_weights.R`, bypassing only its GTAP step —
applied to sha-manifested Census import-merchandise archives: a 2024
base totaling \$3,119.3 billion, within 0.15 percent of their published
denominator, and a 2025 base totaling \$3,242.5 billion. On the 2024
base, the rerun averages 10.72 percent over the window — unweighted
means over the 91 calendar days April 1 through June 30, identical for
every series compared here — and on the 2025 base, 9.38 percent
(Table 3). Rebasing
the weights moves the series by −1.34 points, stable across the
window's four revision segments (1.38, 1.35, 1.35, 1.32), and the
2025-weight leg lands within 0.08 points of TPC's published series.
The two bases join the panel at slightly different coverage — 94.7
percent of the 2024 base value matches against 96.4 percent of the
2025 base — so the −1.34 bundles basket composition with a small
join-coverage differential we did not separate. Everything that still
separates the 2025-weight leg from TPC's published series —
trade-remedy scope, effective-layer treatment, and any residual
difference between our rebuilt 2025 base and TPC's own volumes — nets
to 0.08 points in this window. We cannot decompose that net further,
and offsetting individual differences are not ruled out.

The rerun on Yale's own 2024 base doubles as a validation leg: it
reproduces their published series within 0.2 to 0.6 points in months
containing no schedule revision, and sits 0.36 points below it on the
window mean. That net is consistent with two identified causes acting
in opposite directions, which we did not separately quantify: their
June 9 publication vintage predates their own Brazil Section 301 and
Section 338 encodings, which our panel build includes and which push
the rerun upward where they bind; and our weight bases are built in a
single pass where their production pipeline re-keys weights per
schedule revision under the 484(f) statistical reclassifications,
which accounts for the downward remainder. Neither cause disturbs the
decomposition, which compares the two legs to each other on identical
code and panel.

Both organizations chose defensibly. Yale's fixed-2024 basket is
documented and motivated: it prices the statutory burden on a pre-shock
basket — Laspeyres-type fixed-base weighting — and their pipeline carries
dedicated machinery to keep that basket joinable across schedule
revisions. TPC's notes disclose 2025 volumes excluding antidumping and
countervailing duties without stating a rationale; 2025 was already a
tariff-distorted year, so that base carries first-round substitution in
its weights. A reader comparing the headlines sees a 1.6-point
disagreement that is mostly a weight-vintage choice, made independently
and reasonably on each side. Both leg outputs and the derivation are
committed [@scorecard_repo]; the finding is author-attributed, and the
derivation was sent to both maintainers, with no responses at this
writing.

The decomposition also fixes what an average-rate construct must
declare to be comparable: the rate concept (posted statutory, effective
statutory, or realized collections), the weight base and its vintage,
and the scope of trade-remedy duties. Section 5's dispositions apply
the same discipline line by line; this section applies it
series by series. We also filed two further author-attributed
implementation findings upstream: chapter-98 partial-value sequencing
in the Section 122 path and a phantom civil-aircraft code. Both await a
maintainer response.
