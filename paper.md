---
title: "Tariff rate constructs for the 2025–26 trade shock: weights, scope, and synthetic customs entries"
author: "Max Ghenis"
date: 2026-08-16
bibliography: research/references.bib
link-citations: true
---

# Abstract

Public tariff-rate series can disagree because they measure different
constructs with different import-weight vintages. Over April–June 2026,
Yale Budget Lab's and the Tax Policy Center's daily averages differ by
1.62 percentage points. Holding Yale's pipeline and built panel fixed
while changing only the weight file attributes 1.34 points to the
weight vintage; the 2025-weight rerun lands 0.08 points from TPC, a net
residual we do not further decompose. We separately compare three rate
constructs—encoded posted statutory rates, published effective
statutory rates, and ex-post collections—with each denominator, vintage,
and coverage stated. The authority comparison is an accounting
identity, not an independent validation or proof of closure. Four
encoded action families—Brazil and forced-labor Section 301, the 2024
China action, and solar—were fed as false in the reported evaluation;
entry-level utilization, partial-value, transit, and preference facts
remain absent. An enabling artifact converts official monthly import
margins into synthetic weighted customs-entry lines that reaggregate
exactly under a declared assumptions register. The analysis does not
estimate the complete tariff burden, complete duties, customs revenue,
incidence, or behavioral response. The deterministic legal rules and
their conformance evidence are documented in the companion methods
paper [@tariff_rules_companion].

# 1. Rules layer

The estimation rests on a deterministic rules layer that maps tariff
line, partner, and legal date to a posted ad valorem component stack.
It represents policy changes as dated, instrument-cited versions and
uses generated schedule tables, per-chapter compositions, and grounded
action-membership sets. The five-line witness slice is conformant at
the pinned snapshot after evidence-backed dispositions, but the
schedule-scale artifacts hold no certificate and the witness
composition lacks a fail-closed off-slice guard. The legal derivations,
conformance predicate, disposition standard, and generation gates are
reported in the companion methods paper [@tariff_rules_companion].

This paper consumes that layer as an input and does not duplicate its
proofs or gate narrative. Rules pin: rulespec-us
`dbf09f44eddd00b7ad5520f89371ebe8fdf0b7df` (witness encoding),
`f062088f` (schedule spine), `747d54f5` (generated compositions),
`956a5474` (incidence tables), and `96d5e7c1` (decoupled compositions
and steel component); engine `ffd8213271947b0189a9dd61a055c1e0e78908a0`;
reconciliation snapshot `dc1da3af067c50fa7138458faf3703b4b9efd7cb`;
Yale reference `c4307e514196618afcbf88cf7fd33746417eeabf`.

# 2. Why the two public trackers disagree with each other

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
and the scope of trade-remedy duties. The companion rules paper's
dispositions apply the same discipline line by line; this section applies it
series by series. We also filed two further author-attributed
implementation findings upstream: chapter-98 partial-value sequencing
in the Section 122 path and a phantom civil-aircraft code. Both await a
maintainer response.

# 3. Synthetic customs entries from official margins

The statutory panel answers what the rate was. Applying it to trade
requires the other half: what crossed the border, at what value, in
which tariff line, from where. The public record answers this at the
margin — monthly totals by line, country, and district — while the
transaction-level record (the entry summaries importers actually file)
is either restricted to secure-enclave access or not assembled at all.
We construct the bridge: weighted synthetic entry-line allocations
whose customs value reproduces the public margins exactly at a stated
grain, with every assumption below that grain declared. Three scopes
govern everything in this section and must not blur. The bulk ingest
preserves eighteen months of detail at line × country × country
subcode × entry district × unlading district × rate provision × month.
It separately publishes district-aggregated margins at line × country
× month. The entry generator uses that second record for a five-month,
all-line pilot at the same margin grain.

**Data records and relationships.** The artifact is a small relational
system, not a single flat file:

| Record | Observation or key | Relationship |
|---|---|---|
| `detail/period=YYYY-MM.parquet` | Published monthly detail keyed by HTS-10, Census country and subcode, entry and unlading districts, and rate provision | Preserves the source publication grain and all 22 monthly measures. |
| `margins_hts10_country_month.parquet` | One active cell per `(period, hts10, cty_code)` | Aggregates the detail over subcode, both districts, and rate provision; it is the generator input. |
| `district_entry_month.parquet` | Publisher control total by entry district and month | A separate reconciled district record, not a dimension of the margins-table key. |
| `synthetic_import_entries.parquet` | One weighted synthetic allocation row | Disaggregates each positive margins-table customs-value cell. |
| `assumptions.json`; `validation_report.json` | Dataset-level register and receipt | Authenticate the input publication, state assumptions, and record exact reaggregation. |

The synthetic table's fields are `entry_id`, `entry_date`, `period`,
`hts_number`, `hts10`, `chapter`, `country_of_origin`,
`census_country_code`, `customs_value`, `shipment_value`,
`is_postal_shipment`, `is_synthetic`, `weight`, and `size_stratum`.
The generator requires a unique `(period, hts10, cty_code)` input key
and emits rows only for positive customs-value cells; a zero cell has
no synthetic row. `weight` is the integer multiplicity represented by
the row, so weighted value is `weight × customs_value`, not an
unweighted transaction observation. Validation rejects a null in any
emitted field, a non-positive value or weight, unequal shipment and
customs values, a true postal flag, or a synthetic marker other than
true. These rules support exact reaggregation and weighted summaries
under the registered assumptions; they do not identify true transaction
counts or distributions.

**The margins, from the loading dock rather than the front door.**
Census publishes the complete monthly U.S. Imports of Merchandise
database as public archives — one ZIP per month, no authentication, at
a stable URL pattern. Eighteen archives (January 2025 through June
2026, ~3.3 GB, every byte sha-manifested at retrieval) parse under the
record layouts shipped inside the archives themselves into 38,841,305
detail rows: tariff line × partner country × country subcode × entry
district × unlading district × rate provision × month, with twenty-two monthly measures spanning customs value, dutiable
value, calculated duty, charges, quantities, and air/vessel/
containerized transport splits. The same archives carry the
publisher's own control-total files, which makes reconciliation an
internal affair: our parse must reproduce Census's own totals, in
integer dollars, on three independent axes — by country, by commodity,
by district. Across all eighteen months and every published measure,
it does, with zero tolerance and zero failures (Table 2 consolidates
the pipeline's validation results). The archives replace an API path we built first and demoted: the
equivalent extraction through the Census International Trade API took
thousands of calls and failed server-side on the largest chapters,
and the bulk files carry strictly more detail. The API survives as a
second delivery channel of the same producer — a check that detects
parsing and channel errors on either path, not errors common to the
source itself. A gated cross-check fetches a stratified sample
through it and compares cell for cell: 108,977 cells across sixteen
(line-prefix, country) strata, exact on all four dollar measures,
zero mismatches. The reconciliation against control totals is
likewise internal validity — the archive against its own publisher's
sums, monetary and quantity measures alike across the 22 commodity,
18 country, and 18 district measures — and we label both checks as
what they are.

**Down to entries, assumptions on the table.** The generator
disaggregates each (line × country × month) customs-value cell into
weighted synthetic entries by integer largest-remainder allocation:
entry counts and the within-cell size distribution fix each stratum's
target dollars, integer division allocates the floor, and the
remainder distributes one dollar at a time by largest fractional
part — so each stratum resolves to at most two weighted rows and the
allocation is integer arithmetic end-to-end, with the weights
carrying how many identical entries each row represents. The identity constraint is absolute:
weighted customs value reproduces every line-by-country-by-month cell
to the integer dollar. The arithmetic earns the word exact: cross-
cell aggregations run in arbitrary-precision Python integers (the
adversarial review caught and killed a fixed-width accumulation that
could wrap), cell values are validated at or below 2^53 so their
parquet representation is exactly representable, and the build
asserts the reproduction at run time rather than trusting the
construction. In the pilot window of February through June 2026, every
synthetic date (the fifteenth) is inside the composition's modeled
temporal window. Spatially, however, the generator is unrestricted: it
applies no HTS-line filter and includes every positive customs-value
cell in those months. Its 3,806,050 allocation rows carry 44,881,145
weighted entries and a weighted customs value of $1,467,109,590,515,
equal to the all-line window's margins total exactly. These are data-
construction totals, not results from applying the tariff composition;
this paper reports no composed rate over the pilot.

What the margins do not determine, the dataset does not pretend to
know. An assumptions register ships beside the data, and its entries
are calibrated where an anchor exists and labeled where one does not:
entry counts derive from Customs and Border Protection's published
fiscal-year-to-date mean entry value, with the coverage window
(October 1, 2025 through July 27, 2026) carried explicitly rather than
laundered into an annual figure; within-cell entry sizes are
lognormal, with σ = 2.6916 solved so that the share of entries at or
under $2,500 matches CBP's published informal-entry share — labeled a
proxy moment, because the regulatory informal-entry categories map
imperfectly onto a value threshold, and the residual gap is registered
(achieved share within $2.6 \times 10^{-5}$ of target; achieved mean $32,689
against a $32,916 anchor, the difference a documented small-cell floor
effect). Three fields have no public anchor at all — postal-shipment status,
sub-monthly timing, the shipment-value/customs-value distinction —
and each is set to a declared constant with a sensitivity note, not
imputed and forgotten. The timing constant deserves its own warning
because this paper's own Section 1 is the counterexample: every
allocation is dated mid-month, so nothing in this dataset can resolve
an intra-month legal boundary — the February 20 termination, the
February 24 collection cutoff, the July 24 seam. Analyses at those
boundaries need the margins plus the rule history, not these
allocations. Every row carries `is_synthetic = true`.

The honesty machinery extends to the anchors themselves. CBP's
statistics page mixes completed fiscal years with in-progress ones;
our parser emits in-progress years only as fiscal-year-to-date records
with explicit as-of endpoints, and it fails closed — wording it cannot
read, impossible calendar dates, notes displaced from their table,
endpoints later than the retrieval instant, all raise rather than
default. A fiscal year becomes an annual total only after its final
day has elapsed.

The result is not a substitute for the restricted transaction data,
and the paper does not offer it as one. Its intended uses are the
ones its contract supports: weighted synthetic allocation records
whose margins are exactly the official ones and whose departures from
the observable record are enumerated. Applying the statutory
composition requires first filtering to the five witness lines and
returns only a posted ad valorem component-rate stack. Complete duty or
revenue accounting additionally requires bases and state this dataset
does not supply.

# 4. Weighted rate constructs and reconciliation

Table 4 reports the round-three evaluation over the companion rules
layer [@tariff_rules_companion]. The fixed-2024
statutory mean is 14.43 percent, with 83.4 percent of basket value
covered; the 2025-weight mean is 12.25 percent, with 86.4 percent
covered. Ex-post collections are 6.81 percent. Section 301 is 1.347
percent against the tracker's 1.329 percent, a residual of 0.017
percentage point. Our steel-and-aluminum Section 232 scope is 4.313
percent against the tracker's 5.168 percent. That −0.856-point
residual compares our metal scope with its all-Section 232 family,
which also includes autos, light trucks, parts, copper, semiconductors,
medium- and heavy-duty vehicles and buses, and the wood family.
Section 201 is zero against 0.080 percent because the solar action's
membership, though encoded, was fed as false in this evaluation
alongside the Brazil, forced-labor, and 2024 China actions; the
difference is an evaluation-feed limitation, not a scope comparison.

Section 122 is 6.435 percent against 2.969 percent, a difference of
3.47 points. This wedge is not closed. It is decomposed into declared
entry facts absent from the first version: General Note 6 civil-
aircraft utilization, which is sensitivity-only and covers 11.1
percent of value; USMCA and CAFTA entry status; partial-value facts;
and transit status. The remaining unencoded line-list layer is 0.92
percentage point, down from 6.58. These are accounting labels, not an
independent validation of closure.

# 5. Uses and limits

What the pair enables now is deliberately narrower than duty
assessment. The five-line witness still supports source-traceable,
posted ad valorem component-rate calculations on its guarded caller
surface. The generated schedule compositions now accept action-
membership inputs for arbitrary rated lines, with their posted general
or column-2 rate where that rate is ad valorem or Free. The action-
incidence layer is membership-encoded and evaluated for the principal
families, but four families (Brazil and forced-labor Section 301, the
2024 China action, solar) were fed as false in the reported run, and
the entry-level facts that determine some exemptions and value bases
are not inferred. The synthetic pilot
supplies the needed identifiers and a declared mid-month date, but this
paper reports no application of the composition to those rows.
Separately, the ingest's 302,318 consumer
facts publish at five aggregation grains with channel-invariant keys
that can serve as calibration targets downstream.

What the pair does not enable is complete duty or revenue accounting.
The entries lack the quantities needed for beer's column-2 duty of
13.2 cents per liter, declared aluminum-content value for the beer Section 232
duty, quota state, and sub-monthly timing. The Section 232 rule exposes
beer applicability but returns zero in its ad valorem component because
the content-value basis is unavailable. Every synthetic entry is dated
on the fifteenth, so it cannot resolve the February 20/24 boundary or
other intra-month changes. Exclusions, drawback, misclassification, and
collection wind-down create further wedges between a posted statutory
rate and collected revenue.

Nor do we claim incidence or behavioral response. Trade-share
weighting is an explicit estimation construct here, while exemption
use and de minimis composition remain outside the reported inputs;
nothing here says who bears a duty or how
trade reallocates. The synthetic entries reproduce observed margins
under declared assumptions but are not restricted transaction data,
and within-cell analyses such as importer concentration or the true
entry-size distribution are unsupported. The relevant ranges remain
separate: reconciliation covers five lines from the encoded temporal
start, margins cover January 2025 through June 2026, and the
spatially unrestricted pilot covers February through June 2026. A
joint application would require their true line-and-time intersection,
but no such composed result or committed intersection receipt is
reported here. The Section 4 schedule-scale averages inherit the same
discipline from the other side: they are exact evaluations of the
encoded scope. What remains outside is entry-level utilization, USMCA
and CAFTA entry status, partial value, transit status, the non-metal
Section 232 family, the four action families fed as false, and the
vintage and basket differences bundled in the residual line-list layer. The paper therefore does not estimate the complete
burden.

The natural next analyses — complete duty calculation, distributional
incidence, and tariff-revenue counterfactuals — sit one layer up, after
the fail-closed line guard, missing bases, quota state, finer timing,
and application receipt are supplied. Conflating that layer with this
paper would launder modeling assumptions through a dataset whose
claim to exactness is limited to reaggregation of declared margins.

# 6. Related work

**Tariff-rate data for the trade-war literature.** The empirical
literature on the 2018–19 tariffs built its rate data by hand, wave by
wave. Fajgelbaum, Goldberg, Kennedy, and Khandelwal digitized each
wave's product lists and statutory rates from the official
announcements to estimate the trade war's incidence
[@fajgelbaum2020return]; Amiti, Redding, and Weinstein assembled the
same sequence for pass-through event studies [@amiti2019impact;
@amiti2020whos]; Flaaen and Pierce mapped tariff-line changes into
industry exposure measures [@flaaen2019disentangling]. In each case the
tariff schedule is a bespoke research input, frozen at publication.
Bown's widely used trackers institutionalized the hand-compiled
approach as a maintained public timeline [@bown2021uschina;
@bown_piie_chart]. The 2025–26 environment strains this tradition on
two margins the earlier waves mostly spared it: authority count
(a base schedule plus six overlay authorities with distinct
lifecycles) and tempo
(terminations, expiries, and revision-level rate surgery inside single
months). Teti's Global Tariff Database extends statutory rate coverage
impressively in space and time — two hundred importers back to 1988 —
but at HS-6, without the 2025–26 emergency authorities, and as data
rather than executable derivations [@teti2024missing].

**The tracker we validate against.** The nearest neighbor to our
statutory panel is its own validation reference. Yale Budget Lab's
tariff-rate-tracker is an open-source pipeline producing an
interval-encoded panel of statutory rates at the tariff-line ×
country level for the 2025–26 regime, built from the trade
commission's schedule archives with documented policy parameters
[@yaletracker_repo; @budgetlab2026tracker]; the Budget Lab's published rate series are already a benchmark other
measurement work checks against [@cavallo2026tracking] (the citation
benchmarks the Lab's report series; the tracker tool itself is
newer). We are not, therefore, the first
executable statutory tariff panel; the tracker is one, and a good
one. The contribution is the form and what the form enables: rules
at the instrument grain, each version citing and quoting its legal
source, with mandatory boundary tests — versus one pipeline whose
judgment calls live in code — and, on top of that form, a
cross-implementation conformance regime. We find no formal citation of the tool itself as of August 2026
(a web-bounded search; the tool is four months old), which suggests —
though a negative search cannot establish — that Section 3's
reconciliation is the first external research engagement with the
tracker's internals; the companion rules paper's
derivation-backed defect reports are what that engagement produces
when a disagreement survives audit.

**Rules as code and calculator validation.** Executable encodings of
law have an established line: OpenFisca's deployed tax-benefit
engines [@openfisca], Catala's formally grounded statute-to-code
language [@merigoux2021catala], and the policy agenda articulated for
rules-as-code generally [@mohun2020cracking]. Cross-validation is
likewise institutionalized practice in tax microsimulation — NBER's
TAXSIM as a reference implementation [@feenberg1993introduction],
EUROMOD's country-report validation regime [@sutherland2013euromod],
and maintained harnesses that reconcile independent calculators
line-by-line [@taxcalculator_taxsim_validation]. To our knowledge that culture had not previously reached trade law. Tariffs are, if anything, the easier
target for it — the instruments are public, the schedule is versioned
by the issuing agency, and the reference tracker already exists — and
the 2025–26 record supplies the volatility that makes the exercise
informative rather than ornamental.

**Synthetic microdata.** The synthetic-data tradition in official
statistics runs through disclosure avoidance: synthetic establishment
panels standing in for confidential business registers
[@kinney2011towards], noise-infused releases with formal privacy
guarantees [@machanavajjhala2008privacy], and, in transport and
demography, synthetic populations fit to published margins
[@beckman1996creating]. Customs data specifically have seen synthesis
for machine-learning research — artificial Korean import declarations
generated for fraud-detection benchmarks [@jeong2022customs] — while
the true U.S. transaction record remains restricted-access
[@bernard2009importers; @census_lfttd] or proprietary. Our entries
invert the disclosure-avoidance objective: the inputs are already
public, no confidentiality constraint binds, and the generator's
contract is exact integer reproduction of the customs-value margin at
its stated grain, with a declared assumptions register below it. We find no prior public U.S. synthetic customs-entry dataset with
that contract; the claim is bounded by our search (August 2026) and
Section 1's contribution list is written to survive even if one
surfaces — the representation and the reconciliation regime do not
lean on the dataset's novelty.

# Data and code availability

The committed replication surface is distributed across the source
projects. Rules layer: see the companion methods paper
[@tariff_rules_companion]. Microcosm contains the entries code
and the P1 evidence pack: build report, source manifest, eighteen
monthly reconciliation records, and gated cross-check report. The Yale
reference is pinned at commit `c4307e51`. Census archive URLs, sizes,
and sha-256 digests are in the P1 source manifest, and the CBP page bytes
are archived beside the facts they ground.

Three limitations prevent an archival-replication claim for this draft:

1. The authoritative disposition evidence is
   `axiom-oracles@dc1da3af067c50fa7138458faf3703b4b9efd7cb:dispositions/us-tariff-panel.yaml`,
   dated 2026-08-03: 30 entries and an MFN footprint of 594. The public
   mirror has 46 entries and an MFN footprint of 462; its file is
   `dashboard/public/data/dispositions/us-tariff-panel.json` at that same
   pin, and it is stale, dated 2026-08-02. It is not evidence for this
   paper's disposition claims and must
   be regenerated from the authoritative source under a synchronization
   tripwire before archival release.
2. The P2 validation receipt and outputs are currently local rather
   than committed. Their sha-256 values are
   `45276e944ff8cb6680e50ba27238d68a5b37da09b0d860db2ccfbd577ec5a03e`
   (`validation_report.json`),
   `b3bcad3347d83c3ab9f9b937e1e6133ab002cb9432a2225e37a10e2c5f944a43`
   (`assumptions.json`), and
   `fbc64fd807eff3b2c43bfe88a39ccf5740be5a17786c1d110afd75c07c1d0972`
   (`synthetic_import_entries.parquet`). They must enter the archival
   package before its release.
3. Exact component-review prompts, model versions and settings,
   adjudication records, and prospective stop/restart rules are not
   preserved. Review-round counts remain development provenance until
   that protocol is archived.

The committed pins reproduce the comparison and P1 receipts. The local
P2 hashes make the present outputs checkable on this machine but do not
replace publication of those artifacts.

**Pinned revisions.** Encoding: rulespec-us
`dbf09f44eddd00b7ad5520f89371ebe8fdf0b7df`. Engine:
axiom-rules-engine `ffd8213271947b0189a9dd61a055c1e0e78908a0`
(v0.1.0; binary sha-256 `674ca6e7…bbe32d7`). Reconciliation snapshot:
axiom-oracles `dc1da3af067c50fa7138458faf3703b4b9efd7cb`. Reference:
Budget-Lab-Yale/tariff-rate-tracker
`c4307e514196618afcbf88cf7fd33746417eeabf` (MIT). Entries pipeline:
microcosm merge commits `d4b0855157af996bd367146bc200a2f72ee7d15d`
(ingest) and `6707ed5912d33ff0a340474a1a24f31546c6dec5` (generator).
No archival release accompanies this working paper. Before release, the
project must also add the fail-closed five-line composition guard and
negative tests, regenerate and tripwire the disposition mirror, archive
the P2 outputs and review protocol, and retain the planned containerized
one-command rebuild and persistent identifier.

The Section 2 decomposition's leg outputs are committed in the public
scorecard repository [@scorecard_repo] at `f9e7acf` under
`data/pe/diagnostics/`, with the derivation annotation under
`sources/`; the weight bases with hash receipts, the 2025 recipe-build
log, the Census archive manifest chain, and the statistical-membership
map live in the project lane pending the archival release. The rules-layer generated schedule ships in the rules repository under
`us/policies/usitc/us-tariff-duty/lines/generated/` at merge
`f062088f`, with its reproducer
(`tools/generate_hts_rate_tables.py`), whose check mode re-derives and
byte-compares all 200 committed files. The full-schedule provisions
feedstock is corpus version
`2026-08-09-usitc-hts-2026-rev15-full-schedule`. The rules-layer
composition layer (one hundred generated chapter compositions, their
companion tests and program specifications, the composition generator,
and the gate evidence bundle including the identity grids, the
independent differential report, and the hundred-module validation
record) ships in the rules repository under
`us/policies/cbp/us-tariff-schedule/generated/` at the
series-completing merge `747d54f5`, landed as three reviewed batch
merges with its generator
(`tools/generate_schedule_compositions.py`), whose check mode
re-derives and byte-compares all 300 committed files; the
schedule-scale evaluation caches, the three-construct series, and the
tracker reconciliation outputs live in the project lane with hash
receipts, held for the archival release alongside the weight bases.
The action-incidence tables, `tools/generate_incidence_tables.py`, and
`tools/b16_differential_check.py` ship in rulespec-us at merge
`956a5474`; the decoupled compositions and
the heading-9903.82.02 steel component ship at merge `96d5e7c1`.
Their gate reports and reconciliation evidence are archived in the
project lane pending archival release.

**AI-use disclosure.** The encodings, pipelines, tests, and reviews
described in the companion rules paper and Sections 2–4 here were produced by AI agents under the stated
gates, with human direction of scope, dispositions, upstream
communication, and publication. This manuscript was drafted by the
authoring agents from a primary-source-verified fact base and revised
through hostile, round-diff, red-team, and fresh-eyes referee passes.
The component-review reproducibility limit above applies; manuscript
review cannot substitute for the pinned artifacts and checks reported
with each claim. The human author is responsible for all claims.

# Tables (wire into sections at final assembly)

## Table 2 — Entries pipeline validation (§3)

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
| Informal-share proxy calibration (σ = 2.6916) | share Δ $2.6 \times 10^{-5}$; mean $32,689 vs $32,916 anchor |

## Table 3 — Tracker decomposition, April–June 2026 daily means (§2)

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

## Table 4 — Three average-rate constructs from the composed schedule, April–June 2026 (§4)

| Construct | Window mean | Coverage and scope |
|---|---:|---|
| Encoded statutory, fixed-2024 weights | 14.43% | 83.4% of basket value available; 16.6% excluded (specific/compound/conditional cells, classified not force-parsed) |
| Encoded statutory, 2025 weights | 12.25% | 86.4% available; 13.6% excluded |
| Ex-post collections | 6.81% | calculated duties over customs value, Census monthly |
| Yale published (effective statutory, fixed-2024) | 11.08% | non-comparable reference series: full basket with ad valorem equivalents and exemption-adjusted incidence |
| TPC published (statutory, 2025 ex-AD/CVD) | 9.46% | non-comparable reference series: published all-goods scope |

| Authority comparison | Ours | Yale | Residual and scope |
|---|---:|---:|---|
| Section 301 | 1.347% | 1.329% | +0.017 percentage point |
| Section 232 | 4.313% | 5.168% | −0.856 point; ours is steel and aluminum, while Yale is the all-Section 232 family, including autos, light trucks, parts, copper, semiconductors, medium- and heavy-duty vehicles and buses, and wood |
| Section 201 | 0.000% | 0.080% | −0.080 point; solar membership encoded but fed as false in this run (evaluation-feed limitation, with Brazil, forced-labor, and 2024 China) |
| Section 122 | 6.435% | 2.969% | +3.47 points; not closed: GN6 civil-aircraft utilization, USMCA/CAFTA entry status, partial-value facts, and transit status are declared inputs absent in version 1 |

The General Note 6 input is sensitivity-only and covers 11.1 percent
of value. The remaining unencoded line-list layer is 0.92 percentage
point, down from 6.58 in revision 9. The Section 122 labels decompose
an accounting wedge; they do not close it. The encoded stack carries
no antidumping or countervailing duties, and excluded cells receive no
effective-layer ad valorem equivalents.
