---
title: "Executable tariff law: a conformance-tested statutory panel and synthetic customs entries for the 2025–26 trade shock"
author: "[Author slots — working draft, local only]"
date: 2026-08-13
bibliography: research/references.bib
link-citations: true
---

# Abstract

Tariff rates can cease legally before collection ends, so a statutory
rate needs a date, an instrument, and a derivation. We encode the
2025–26 United States tariff stack as versioned, instrument-cited
executable rules and reconcile their outputs cell by cell against Yale
Budget Lab's open tariff-rate tracker [@yaletracker_repo]. The primary
contribution is the rules-as-code and cross-implementation conformance
method. Its five tariff lines are a witness slice jointly selected so
that every in-scope authority binds somewhere; every disagreement in
the five-line reconciliation receives an evidence-backed disposition.
The schedule's rate columns then extend to all 13,790 rated lines as
deterministically generated, per-cell provision-grounded tables, gated
on reproducing the hand-built witness line modules' encoded rates
exactly. The same discipline applied across implementations shows that
the 1.6-point April–June 2026 gap between Yale Budget Lab's and the
Tax Policy Center's daily average-rate series is mostly the
import-weight vintage — 1.34 of the 1.62 points; rerunning Yale's own
pipeline on 2025 weights lands within 0.08 points of TPC — a
reconciliation we find published by neither organization. The exercise
also produces two proposed reference corrections, each supported by a
legal derivation and still awaiting maintainer response. An enabling data artifact converts
official monthly import margins into synthetic, weighted customs-entry
lines that reaggregate exactly, with assumptions recorded beside the
data. The implementation has material boundaries. The hand-built
witness composition contains five line predicates but no fail-closed domain guard, so
callers must restrict it to the witness slice: unsupported lines can
return plausible values rather than errors. The generated tables
publish posted rates and dispositions at full coverage, and one
hundred generated per-chapter compositions evaluate the statutory
stack economy-wide under identity, differential, and replay gates. The
encoded action-incidence layer closes the Section 301 comparison to two
hundredths of a percentage point; the remaining separation from the
tracker is named entry-level facts and a scope difference in the
Section 232 family. Its output is a posted ad
valorem component-rate stack under declared synthetic timing, not a
complete duty amount or revenue account; the inputs omit specific-duty
quantities, aluminum-content value, quota state, and sub-monthly timing.
We report the committed pins, hash-pin the local P2 outputs, and identify
the remaining synchronization and archival prerequisites.

# 1. Why 2026 broke tariff lookup

On February 20, 2026, the additional ad valorem duties imposed under
the International Emergency Economic Powers Act stopped being law. They
did not stop being collected. That morning the Supreme Court held that
"IEEPA does not authorize the President to impose tariffs" [*Learning
Resources, Inc. v. Trump*, 607 U.S. 229 (2026); @learningresources2026]; the same day,
Executive Order 14389 [@eo14389_2026] ordered that the duties "shall no longer be in
effect and, as soon as practicable, shall no longer be collected" —
and named no date for the second clause. The date arrived two days
later in a Customs and Border Protection cargo-systems message
[CSMS #67834313; @csms67834313_2026], instructing that collection would end for goods entered on
or after 12:00 a.m. on February 24. So the legal end of the era's broadest tariff
action — the IEEPA orders reached imports economy-wide — is a court
decision and an executive order,
and its operational end is an agency bulletin — three documents, two
dates, four days apart. Any dataset that records "the tariff on
Chinese imports in February 2026" as a single number has taken a
position on which date counts — and a dataset that does not publish
its convention has taken it silently.

That week is the 2025–26 tariff environment in miniature. Over
eighteen months, the United States imposed, modified, litigated, and
unwound overlapping duties under the base tariff schedule and six
overlay authorities — IEEPA, Section 232, Section 301, Section 201,
Section 122, and Section 338 — the authority set the reference panel
of Section 3 tracks as statutory rate columns.
Alongside the IEEPA orders and their termination: Section 232
national-security actions across metals and manufactured goods;
Section 301 actions [@ustr2026forcedlabor] including a forced-labor program that determined
sixty investigations actionable at once, inserting a new chapter-99
note into the tariff schedule (U.S. note 52) with two rate tiers and
country-specific quotas; a Section 122 balance-of-payments surcharge
[@proc11012_2026] that ran at 10 percent for exactly its statutory
maximum of 150 days [@usc2132]; Section 201 safeguards on solar equipment
stepping down annually on a proclamation schedule to a 2026 expiry;
and Section 338 duties. The seams between authorities are themselves
dated facts: the §122 surcharge expired at 12:01 a.m. on July 24,
2026 — the same day the forced-labor duties took effect. The tariff
schedule these overlays modify was a moving target in its own right:
the International Trade Commission's 2026 edition stood at Revision
15 by the first week of August [@hts2026rev15], and a revision can carry a single
surgical change — Revision 15's only entry amends one chapter-99
heading, zeroing the Section 232 rate on United Kingdom patented
pharmaceuticals from +10 percent [@bis2026ukpharma], three days after
Revision 14.

The result is that the object researchers call "the statutory tariff
rate" became a function of four arguments — tariff line, partner
country, date, and legal interpretation — and the fourth argument is
the one nobody's spreadsheet has a column for. A rate query for a
solar module from Malaysia on February 22, 2026 has defensible answers
that differ by authority and by reading: the IEEPA overlay is legally
dead but still being collected for two more days, and the safeguard
duty's staged schedule has been expired for sixteen days. The
difference between the answers is not a data error. It is a fact
about how each authority ended, and an analysis of legal exposure
needs different dates than an analysis of customs revenue.

Reference datasets have handled this churn the way the trade-war
literature's datasets handled 2018–19: expert judgment applied by
hand, encoded in scripts, and published as numbers whose reasoning lives in commit
messages if it lives anywhere. The most complete of these for 2025–26 — Yale Budget Lab's
tariff-rate-tracker, an open-source pipeline that resolves the churn
into an interval-encoded panel of statutory rates by tariff line,
country, and date, and the validation reference we use throughout
this paper — is very good. It is also the product of judgment calls
that a reader cannot mechanically audit: which proclamation governs a
line on a date, when a staged schedule ends, which countries a
general note diverts to a different rate column. Sections 3 and 4
show what happens when those calls are made checkable — including two
places where the best available reference and the underlying
instruments disagree.

Our claim in this paper is narrow and, we think, timely: when the law
moves this fast, the honest representation of a tariff rate is not a
number but a dated derivation — a rule that cites the instrument that
set it, bounded by the instrument that ended it, executable so that
"the rate on date X" is computed rather than transcribed. The 2025–26
shock is the demonstration that this is not a formalist's luxury.
When rates change by proclamation monthly, die in two stages, and
expire into seams that begin the next program the same morning, the
derivation *is* the data.

The paper's primary contribution is a representation and validation
regime: the 2025–26 stack encoded as instrument-cited, version-dated
rules, then reconciled against a separately developed reference on a
five-line witness slice with mandatory boundary tests, a strict
predicate, an evidence standard for every disposition, and a disclosed
waterfall (Sections 2–4). The slice is jointly selected so that every
in-scope authority binds somewhere; it is not one independently
representative line per authority family. A second, enabling
contribution is a margin-exact synthetic customs-entry dataset with a
declared assumptions register (Section 6). The paper computes an
import-weighted average of the encoded statutory scope across the full
schedule (Section 7), but does not estimate the complete schedule-wide
tariff burden, complete duties, or customs revenue. The action-incidence
layer is encoded. Entry-level utilization, entry status, partial value,
the non-metal Section 232 family, and non-ad-valorem equivalents remain
outside the reported scope. Applications that add the missing bases and state — and
distributional incidence analyses built on them — remain future work
(Section 8).

# 2. What a tariff change is, formally

Every rule in our encoding is a list of dated versions. A version has
an `effective_from` date, a formula or value, and a proof: one or more
atoms, each citing a path into a signed corpus of legal instruments and
quoting the operative text verbatim. A policy change appends a version;
it never edits one. The history is not metadata attached to the
representation — the history is the representation, and the engine
answers "the rate on date X" by selecting the version in force at X.

Three properties follow, and each one earns its keep in the 2025–26
record.

**Changes cannot outrun their instruments.** A version's proof atoms
cite corpus paths — a Federal Register document, a tariff-schedule
heading at a specific revision — and the corpus is ingested under
signed manifests before any encoding can reference it. There is no way
to encode "the §232 aluminum rate doubled" ahead of possessing the
proclamation that doubled it, and the citation carries an excerpt, so
a reviewer checks the claim against quoted text rather than against a
maintainer's memory.

**Endings are law, not deletions.** The IEEPA termination that opened
Section 1 is encoded as a rule, not as the removal of one:

```yaml
# source: rulespec-us us/policies/usitc/us-tariff-duty/overlays/ieepa/termination.yaml@dbf09f44 (excerpt)
- name: terminated_ieepa_additional_ad_valorem_duty_rate
  kind: parameter
  dtype: Rate
  source: Executive Order 14389 section 1
  metadata:
    proof:
      atoms:
        - path: versions[0].formula
          kind: parameter
          source:
            corpus_citation_path: us/rulemaking/federal-register/2026-02-25/2026-03832
            excerpt: "shall no longer be in effect"
  versions:
    - effective_from: '2026-02-20'
      formula: |-
        0
```

The terminated rate is a zero that took effect on February 20, 2026,
citing the order that zeroed it — the panel this encoding generates
carries the termination as a dated fact, exactly as it carries the
imposition. One scope note, stated precisely: this encodes the LEGAL
endpoint, which is the semantics the reference panel publishes by
default and the semantics we reconcile against in Section 3. The
operational wind-down of Section 1 — CBP's February 24 collection
cutoff — is an agency bulletin, not a rule version in this encoding;
a parallel collection-status series sourced from such bulletins is
future work, and nothing in this paper's data should be read as
carrying it. A companion test evaluates the composed rates on the one-day period of
February 20 itself and asserts that the additional duty no longer
adds; the test is mandatory, so the change could not have merged
without pinning its own boundary.

**Schedule churn is encoded, not smoothed.** When the trade commission
issues a revision that restructures lines — consolidating headings,
retiring statistical suffixes — that restructuring is itself a dated
module (the aluminum family, for instance, carries a
revision-12 consolidation module alongside its rate overlays). A
downstream user never faces the silent question of which revision's
line structure a number refers to; the revision boundary is in the
derivation.

The engine's operational semantics are part of the claim, not an
implementation footnote. At the pinned engine revision `ffd82132`, they
are:

| Operation | Runtime rule | Consequence for this paper |
|---|---|---|
| Query time | Compare inclusive version bounds at the query period's start. | A day-grain query uses that day's start; intra-day legal cutoffs are not represented. |
| Version selection | Among applicable versions, select the greatest `effective_from`; a gap raises a missing-version error. Equal-start ties fall through to document order. | The encoding avoids relying on an equal-start tie as legal precedence. |
| Branch precedence | Evaluate the formula's authored, nested conditionals. The engine has no general tariff-authority hierarchy solver. | Exceptions and priority must be explicit inside each component formula. |
| Stacking | Add the component outputs explicitly in the composition formula. | No duty stacks merely because two instruments coexist. |
| Types and errors | Enforce declared scalar-versus-judgment shapes and reject unknown outputs, parameters, relations, or units; missing inputs, versions, or values; type mismatches; and division by zero. | `Rate` labels the composition's scalar output; it does not supply a duty base or turn a rate into money. |

The caller precondition is equally important. The composition defines
exact-line predicates for five witness lines and uses them within
components, but it does not require their disjunction as a top-level
domain guard. Outside the slice, the MFN component can fall through to
zero and, during the Section 122 window, a non-exempt line can receive
the blanket surcharge; their sum can therefore look plausible rather
than error. All tariff-composition comparisons in Sections 3–4
restrict the input to the true five-line intersection. A fail-closed
guard and negative off-slice tests are prerequisites for archival
release.

Within that caller-enforced slice, the composed function maps a
(tariff line, partner country, query period) triple to the ex-post,
posted ad valorem component-rate stack under legal-date semantics. It
does not compute specific duties requiring physical quantities,
Section 232 duties requiring declared aluminum-content value, quota
position, or sub-monthly timing. Nor does it resolve entry-specific
facts such as in-transit exceptions or claimed exclusions, or
knowledge-time: `effective_from` records legal-valid time, so a
retroactive instrument enters the ex-post record when encoded. Those
uses need inputs and state absent from this function, and Section 8
repeats the boundary.

The full stack composes from these pieces. A composition module wires
the column rates of the tariff schedule to the authority overlays —
the Section 232 aluminum program (the witness composition's 232
family), the Section 301 families including the forced-labor program, the per-country IEEPA reciprocal modules and
their fentanyl-order siblings, Section 122, Section 201, Section 338 —
and the engine evaluates the composed rate for a caller-restricted
(line, country, period) triple by resolving every overlay's version in
force. Nothing in the
pipeline is hand-transcribed from a secondary source: the corpus
snapshot for this work comprises 138 signed versions — 47 Federal
Register instruments, 44 tariff-schedule revision snapshots, and 47
chapter-99 and general-note extractions — and every operative number
on the evaluated witness paths traces to one of them.

We do not claim this representation is novel as an idea; executable
encodings of statutes have a literature (Section 9), and dated
parameters are standard in tax microsimulation. The claim is about
fit: 2025–26 tariff law is the environment where the alternatives
visibly fail, because the thing being represented changed character.
A rate that steps down on a proclamation schedule, dies in two stages,
or applies to a line that stopped existing mid-year is not a cell in a
table. It is a small legal argument, and the representation that
survives contact with it is the one that stores the argument.

**A worked trace.** Take the solar query of Section 1 — the
crystalline-silicon cell line, one of the five witness lines of
Section 3, from Malaysia on February 22, 2026 — and read the actual
rules at the pin rather than a stylized version of them. The
column-rate module contributes the line's general rate per the
tariff-schedule revision in force. The Section 201 component is an
explicit zero: its only operative version in the modeled temporal
window begins February 15, 2026, nine days after the safeguard's
staged schedule expired. The historical stages are not executable
versions in this component; its proof atoms document the derivation of
the operative zero by quoting the extension proclamation's staged
table (14.75, 14.5, 14.25, 14 percent, each period dated) and the
schedule's compiler's note that the safeguard has expired
[@proc10339_2022].
The operative formula is a constant; the legal argument for the
constant travels with it, which is the representation's point. The
IEEPA component resolves through the termination rule shown above:
from February 20 the termination's zero governs [@eo14389_2026], so
the legal-date answer carries no IEEPA contribution — while the
collection cutoff two days later [@csms67834313_2026] is, per the
scope note, outside this function's semantics. Every step is a
version lookup carrying instrument citations. A separate boundary
probe changes both the partner and date: at the February 24, 2026 probe
for solar cells from Canada, the pinned report shows both implementations return column rate
zero, IEEPA zero, Section 201 zero, Section 122 at 0.10 — a total of
exactly 10 percent, the balance-of-payments surcharge standing alone
atop an otherwise-terminated stack. The "two defensible answers" of
Section 1 become two different, explicit functions — and this paper's
panel computes the legal-date one.

# 3. Cross-implementation reconciliation against an independent tracker

An encoding of tariff law can be internally consistent and wrong. The
check this section reports is a cross-implementation reconciliation:
derive the panel our rules imply and reconcile it, cell by cell,
against a reference built by people who never saw our code. We are
deliberate about the term. The reference — Yale Budget Lab's
tariff-rate-tracker [@yaletracker_repo; @budgetlab2026tracker] — was
separately developed, and the Budget Lab's published rate series are
already a benchmark other measurement work checks against
[@cavallo2026tracking], but both implementations
read the same public instruments, its spine defines the comparison
universe (an omission from that spine is invisible to this exercise),
and our encoding iterated against the visible disagreements until the
predicate held. That is reconciliation between independent
implementations — the standard validation practice of tax
microsimulation transplanted to tariffs — not a held-out evaluation;
the upgrades that would strengthen it (a frozen future snapshot, an
independently double-coded legal sample, a third implementation) are
stated future work.

One design choice governs the universe and is the first thing a
reader should know: the reconciliation runs on a **five-line witness
slice** of the reference's spine. The five tariff lines — beer
(2203.00.0030), ferromanganese (7202.11.1000), unwrought aluminum
(7601.10.3000), crystalline-silicon solar cells (8541.42.0010), and
inflatable balls (9506.62.4040) — were chosen so that every overlay
authority in scope has at least one line where it binds, and each is
crossed with all 240 partners and all 57 of the tracker's date
intervals. The slice is a pilot of the method at full derivational
depth, not a sample estimate of schedule-wide agreement: five lines
are roughly 0.025 percent of the lines behind the reference's
277-million-row panel, every number below is exact within the slice
and says nothing outside it, and extending the same machinery across
the schedule is the recorded next stage of this program. We chose
depth-first deliberately — the two reference-attributed findings of Section 5
were found by exhausting five lines, not by sampling many — and the
paper's claims are written at the slice's scale throughout.

Definitions, so the numbers that follow are exact. A *cell* is a
(tariff line, partner, date-interval) row on the reference's spine;
each row carries one value per *concept slot* — the column rate, each
overlay authority, and the total — so mismatch counts by concept can
overlap on one row. An interval is *covered* when our encoded domain
spans it and *temporal debt* when it wholly predates that domain
(48,000 interval-cells here); an interval straddling the domain
boundary is clipped to its covered portion, with the clip recorded
(1,200 clip events in the artifact). A *comparison* evaluates one covered row in both implementations at
one probe date — 33 probe dates per line-partner span the covered
intervals, placed at interval boundaries and their neighbors — at the
reference's default legal-date convention; a *match* is exact
equality across every concept slot. A *disposition* closes a mismatched comparison
unit with a recorded claim — an encoding defect (which must then be fixed),
a reference-attributed discrepancy (Section 5's standard), or a
declared semantic difference — and a *tripwired exclusion* removes a
reference construct from scope entirely behind a machine-checked guard
that fails the build if the excluded construct's footprint moves.

The comparison totals below come from the pinned report
`axiom-oracles@dc1da3af067c50fa7138458faf3703b4b9efd7cb:reports/axiom-yale-us-tariff-panel-all-2026-08-03.json`;
the disposition entry, class, and footprint claims come from the
authoritative source
`axiom-oracles@dc1da3af067c50fa7138458faf3703b4b9efd7cb:dispositions/us-tariff-panel.yaml`,
updated 2026-08-03. The reference is pinned at `c4307e51`, the encoding
at `dbf09f44`, and the engine at `ffd82132`:

- The reference panel materializes 277,303,920 rows; the reconciled
  slice is the five witness lines crossed with 240 partners over the
  tracker's 2025–26 coverage.
- The slice's 68,400 in-scope interval-cells (5 lines ×
  240 partners × 57 intervals) split into 20,400 covered and 48,000
  temporal-debt cells — our encoded rule history begins 2026-02-15,
  later than the tracker's panel start, and the debt is the surfaced
  difference, carried into Section 8's usage limits.
- The covered intervals yield 39,600 probe-date comparisons (5 lines
  × 240 partners × 33 probes): 24,400 exact matches (61.6 percent
  raw) and 15,200 mismatches, with zero evaluation errors.
- Every one of the 15,200 enters a disposition; none remain
  unexplained, and none are open against our encoding. The authoritative
  file partitions them into 30 entries — every mismatched unit appears
  in exactly one — and the class arithmetic closes explicitly:
  **15,200 = 8,283 `upstream_engine_gap` units in 10 entries + 6,917
  `explained_residual` units in 20 entries.** Its families include the
  IEEPA metals-exclusion layer, the column-2 reference gap of Section 5,
  a Section 232 aluminum-content basis on beer, a free-trade-agreement
  preference layer, a Section 122 metal exclusion, and the Section 201
  safeguard expiry of Section 5; each entry records its concept, case
  selector, and instrument citations. At the
  concept level the mismatches sit in the Section 201 slot (7,887),
  the Section 122 slot (4,560), and the column-rate, IEEPA, and
  Section 232 slots (594, 476, 1,920) — concept counts overlap where
  one cell mismatches several concepts, so they exceed the 15,200
  distinct units. In the authoritative dispositions, the MFN footprint
  is 594 units: 528 in the column-2 family plus 66 in the preference
  family. Section 5 walks the two reference-attributed classes
  we escalated upstream; the remaining classes are recorded cell-by-
  cell in the same artifacts.
- Four reference constructs are excluded by tripwire, by name: the
  tracker's residual `other` column, its China-semiconductor 301 rate
  column, its stacking-output columns, and its Swiss-framework
  construct — each excluded for a recorded technical reason (zero
  exposure in the covered window or a construct our composition
  deliberately does not mirror), each with a guard that reds the build
  if its footprint becomes nonzero.

Table 1 consolidates the waterfall. All ten in-scope policy-construct
records have `covered: true`; four other records are excluded with
tripwires. This record field is distinct from the covered interval-cell
term defined above. The conformance predicate — all in-scope policy
records covered, unexplained equals zero, open encoding-attributed
equals zero — holds on the witness slice. We report the 61.6 percent raw match rate as prominently as the
zero because the two numbers mean different things: the raw rate is
what falls out before any human judgment; the zero is what survives
after every judgment is recorded, attributed, and exposed to audit.
A reader who distrusts our dispositions can recompute the raw rate
from the committed artifacts and re-litigate any cell.

The comparison machinery earned its own scrutiny before we trusted
its numbers. Adversarial review showed that early harness versions
could report vacuous agreement (a slim CI artifact
corrupted totals; an all-zero column compared equal to an all-zero
column it should never have matched), and the reviews killed those
with mutation tests — deliberately corrupted inputs a sound harness
must catch. The final harness binds each panel row to a content
digest and rebuilds byte-identically. Mutation tests validate the comparator,
not the law — the legal-correctness burden rests on the instrument
citations of Section 2 and the derivation standard of Section 5.

We also measured the reference's reproduction cost in a supervised
local rebuild and reported the unexpectedly large resource envelope
upstream, alongside a proposal that the project publish its panel as a
release artifact. Because that measurement receipt is not committed at
the named pins, this paper does not use its numerical value as evidence.

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

# 5. When the oracle disagrees: dispositions with legal derivations

A conformance run that ends in disagreement forces a choice with three
honest outcomes: the encoding is wrong (fix it), the reference is
wrong (demonstrate it), or the two are answering different questions
(declare it). The disposition machinery exists to make the second and
third outcomes as auditable as the first. A disagreement attributed to
the reference cannot be waved through; it requires either the
reference maintainer's acceptance or a derivation from the governing
instruments independent of both implementations' code — the
proclamation's own table, the schedule's own note — recorded beside
the cells it explains, with the cells enumerated by an applicability
predicate rather than by hand. Until the maintainer responds, the
honest name for such a finding is what we use throughout: author-
attributed, derivation-backed, maintainer-unacknowledged. The
rule's purpose is to block the tempting failure mode — "our number
differs, theirs is probably wrong" — by pricing that claim at a legal
argument.

Two derivations from this comparison illustrate the standard, and both
became upstream reports.

**A safeguard rate outliving its schedule.** The Section 201 solar
safeguard's extension proclamation (10339) sets a staged duty
schedule in its annex, verbatim: 14.75 percent through February 6,
2023, then 14.5, then 14.25, then 14 percent through February 6,
2026 — and nothing after. The current tariff schedule corroborates
the end: the compiler's note on the affected headings reads "this
subheading and its related note … have expired." The reference
carries a flat 14.5 percent on the affected lines past the terminal
date, which is wrong on two axes at once — 14.5 was the *second*
year's rate, stale since February 2024, and every rate is expired
after February 2026. For the modeled temporal window, our Section 201
component's operative version is an explicit zero. Its proof atoms
document the historical stages and the expiry; the stages themselves
are not executable versions in that component. The disagreement's recorded footprint is the
affected lines after the schedule moves, enumerated in the disposition
artifact (the Section 201 concept slot's 7,887 mismatched units of
Section 3 are dominated by this class). The derivation —
proclamation [@proc10339_2022], annex table, terminal date, the
schedule's own expiry
note — is recorded in the disposition file, and the finding was
filed upstream with the same citations.

**Four countries on the wrong rate column.** The tariff schedule's
General Note 3(b) [@hts2026rev15] directs that "the rates of duty shown in column 2
shall apply to products, whether imported directly or indirectly, of
the following countries and areas": the Republic of Belarus, Cuba,
North Korea, and the Russian Federation. The reference's parser has
no column-2 branch, so those four countries inherit column-1 base
rates throughout its panel. The disagreement is systematic rather
than episodic — within the witness slice it touches four of the
five lines for the four partners (beer escapes: its column-2 rate is
specific rather than ad valorem, so the ad valorem panel shows no
gap there), and nothing in the parser limits it to the slice — and the
derivation is a single sentence of the schedule's own general notes,
with the note's cross-reference to the Russia and Belarus additional-
duty headings compounding the gap. Filed upstream likewise.

We report both findings as what they are: derivation-backed and, as of
this writing, unacknowledged. The reports sit in the tracker's issue queue with our other
filings — a locale-sensitivity bug
that corrupted country matching (with a patch), the measured build
envelope of Section 3, and a proposal that the project publish its
panel as a release artifact, which would let downstream users skip the
resource-intensive build. None of this is offered as fault-
finding. A reference strong enough to validate against is a reference
worth strengthening, and the economics of the exchange favor everyone:
the tracker gave us the spine that made our zero meaningful, and the
conformance run gave the tracker two defects located to the instrument
and the line, for free.

The dispositions are the paper's answer to a question every validation
exercise should face: what happens to your zero when the reference is
imperfect? An unexplained-zero predicate against an imperfect
reference is achievable only with an escape valve, and the escape
valve is where validation exercises usually rot. Ours is load-bearing
and inspectable — every escaped cell names its instrument — and the
tripwires of Section 3 patrol its edges. When the reference updates,
the dispositions are re-litigated against the new panel, not
grandfathered: acceptance upstream would convert them to fixed cells;
a counter-derivation would convert them to encoding bugs. Either
outcome improves the public record, which is the point of validating
in the open.

# 6. Synthetic customs entries from official margins

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
review of Section 7 caught and killed a fixed-width accumulation that
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
(achieved share within 2.6 × 10⁻⁵ of target; achieved mean $32,689
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

# 7. Provenance engineering

Every reported result is tied either to a committed pin or to an
explicitly hash-pinned local receipt, and the machinery was built by AI
agents under human-directed gates. The distinction matters: the local
receipts and several review records still require archival inclusion,
so this draft does not claim that every result is yet publicly
recomputable.

**The gates.** Corpus documents enter under signed manifests; an
encoding cannot cite what the corpus does not hold. Every rule change
must compile, must carry proof atoms whose excerpts appear in the
cited document, and must pass companion tests that pin behavior at its
effective boundaries — the merge machinery refuses the change
otherwise. Panel derivations bind each row to a content digest and
rebuild byte-identically. Conformance reports pin the reference
commit, the engine build, and the encoding revision they were computed
from, and the scoreboard numbers quoted in this paper carry their
snapshot hashes because the live reports refresh as the encoding
grows.

**The adversary.** The comparison harness, entries ingest, and entries
generator received same-project cross-model adversarial review. The
reviews found concrete failures, including vacuous
comparison, fixed-width overflow, unsafe publication paths, and an
incorrect durability boundary; the associated regression and mutation
tests are part of the technical evidence. The round counts and final
no-finding verdicts are only retrospective development provenance. The
exact component prompts, model versions and settings, adjudication
record, and prospective stopping or restart rules were not preserved,
so the sequence cannot establish convergence or a defect probability.
Archiving those materials is a prerequisite for treating review as a
reproducible protocol.

**The division of labor.** Model-written code, model-run reviews,
machine-checked gates — and human judgment exactly where it is load-
bearing: scope decisions (what counts as law versus estimation), the
disposition standard of Section 5, anything that leaves the project
(upstream reports, this paper), and the decision to ship. We do not
claim the review regime is external certification — reviewer and
authors sit inside one project, and a separately governed
verification protocol is future work. The committed encodings, corpus
manifests, comparison report, P1 build report, reconciliation records,
and cross-check report are pinned and inspectable. The disposition
mirror, P2 output receipts, and component-review protocol have the
specific release limitations stated below; review verdicts do not
substitute for those artifacts.

Within this project, the useful products of adversarial review were
the defects it exposed and the tests and receipts added in response.
Those artifacts, rather than a trajectory toward a no-finding verdict,
carry the evidentiary weight.

## Deterministic generation at schedule scale

The witness slice's hand-built line modules extend to the full
schedule by generation rather than authorship. A deterministic
generator reads the corpus-pinned Revision 15 snapshot — the exact
bytes, hash-pinned, that the corpus retains for that release — and
emits per-chapter rule modules covering every rated line: 13,790 lines
across 98 chapters, as general and column-2 rate tables over ad valorem
and Free lines and total-partition disposition tables over all of them
(ad valorem 6,247, Free 5,795, specific 777, conditional 548, compound
326, component-valued 93, column-2-only 4). A line whose column text is
a specific, compound, or component-valued duty gets an explicit
classification and no rate cell; the machinery refuses to force-parse
what it cannot represent. The same refusal caught the schedule's own
data repair: the one column-2 change between the 2025 basic edition
and Revision 15 across 11,504 common base lines is a trailing-slash
typo the publisher fixed, which the partition classified as
conditional rather than misreading as a rate.

Every table cell carries a proof atom citing its line's provision with
a verbatim body-line excerpt — 48,479 atoms across the full schedule —
validated
against a corpus version that normalizes all 29,845 HTS-numbered rows
of the pinned snapshot to per-line provisions. The generation is gated
three ways: the generated cells must reproduce the encoded rates of the three
hand-built witness line modules that carry rate cells exactly, with
expectations parsed from those modules rather than from any secondary
record; emitting twice must
produce identical bytes; and the base general-rate column must show
zero changes between the 2025 basic edition and Revision 15, which it
does across 11,504 common base lines. A single dated version per line
therefore rests on a verified endpoint comparison for those lines'
general column; chapter 99's action headings and the 66 base lines
born mid-window carry the snapshot's value at a nominal date, with
per-revision versioning recorded as composition-layer work. One structural fact stays out of statutory parameter
space deliberately: the map from ten-digit statistical lines to their
rate-bearing ancestors is emitted as a generated data artifact, held
for the archival release, because its synthetic integer keys appear
nowhere in provision text and therefore cannot meet the grounding
standard the rate cells meet.

Two findings from building the feedstock bear on anyone consuming the
schedule programmatically. The USITC's live export endpoint accepts a
release parameter and silently ignores it — a January 2025 request
returns headings that did not exist until April 2025 — so frozen
vintages exist only where someone retained them; the corpus retains
the full revision series for 2025 and 2026 as pinned snapshots. And at the table stage, applying a
line's rate to an entry was composition-layer work each module declared
as a deferred output: the tables publish what the schedule says, at
full coverage, and leave the five-line witness composition of Sections
2–3 untouched. The next subsection lands that deferred layer.

## Composition at schedule scale and its measured boundary

The composition layer then extends the same way: a second
deterministic generator emits one composition per chapter — one
hundred modules — each importing its chapter's generated tables and
replicating the witness composition's authority components, proof
atoms, declared-entry surface, and effective windows verbatim, with
chapter routing left in entry preparation. Keeping one hundred
same-inventory siblings distinct under the repository's static gates
takes a documented lossless serialization (per-chapter redundant
parentheses and temporal-key spelling for substantive formulas,
chapter-prefixed names for four scalar-literal parameters whose bare
values admit no parenthesization, one directory per chapter), and the
generator asserts reverse-substitution equality against witness bytes
for every transformed rule. Four gates held: the full battery
validates one hundred of one hundred modules; independently compiled
generated compositions reproduce the hand-built witness on
ninety-cell country-by-date grids for both non-pilot witness chapters
with zero component or total deltas; an independent second parser,
sharing nothing with the first path but the pinned snapshot bytes,
re-derives all 48,479 table cells and all 13,790 rated lines exactly,
and fails on a single mutated cell; and double emission is
byte-identical.

The first economy-wide evaluation made the witness boundary measurable.
Its five literal line equalities left most listed actions outside the
schedule calculation even though the rate tables were complete. Replay
of the certified witness slice reproduced all 1,300 extract comparisons
exactly. The missing incidence was therefore a composition boundary,
not an evaluation error. The next layer removes that boundary while
keeping the witness as an oracle.

## Encoding the action-incidence layer

The source is the tariff schedule itself. Chapter 99 notes state which
ordinary tariff provisions receive each action heading. They are page-
level provisions in the corpus and can be grounded at the same atom
standard as a rate cell. The Section 232 note, for example, says that
its headings apply to articles classifiable in the provisions in its
lists, then introduces “(iii) Articles of steel.” The aluminum note says
that a reference to a heading or subheading covers “all its subordinate
provisions (both legal and statistical).” Those words require four- and
six-digit scope as well as the eight- and ten-digit numbers used by the
other lists.

A declarative note grammar identifies the governing subdivision, its
page-spanning bounds, the action, and the printed code widths. The
generator emits 25 membership tables with 12,227 grounded rows.
The tables preserve heading and subheading widths for the primary
Section 232 scope. A structurally independent second parser uses the
same pinned notes bytes but neither the generator's prose boundaries
nor its number recognizer. It reproduced every emitted set exactly.
We also reconciled the sets against the tracker's membership resources.
Every difference was assigned to a vintage, partial-value, or
statistical-level disposition.

The composition generator then replaced five exemplar equalities with
membership-semantic inputs. It also added a Section 232 steel component
grounded on heading 9903.82.02. The hand-built five-line witness remains
unchanged as the oracle. This separation caught a coupling defect: when
general membership flags were fed into the exemplar slots, the witness
zeroed Section 122 on Section 301-member lines. That was an artifact of
the exemplar equalities, not the statute. The fix was made in the
generated source and gated against the witness slice. The gate
enumerates every coupling cell and requires equivalence on the witness
mapping.

Table 4 reports the fully gated round-three evaluation. The fixed-2024
statutory mean is 14.43 percent, with 83.4 percent of basket value
covered; the 2025-weight mean is 12.25 percent, with 86.4 percent
covered. Ex-post collections are 6.81 percent. Section 301 is 1.347
percent against the tracker's 1.329 percent, a residual of 0.017
percentage point. Our steel-and-aluminum Section 232 scope is 4.313
percent against the tracker's 5.168 percent. That −0.856-point
residual compares our metal scope with its all-Section 232 family,
which also includes autos, light trucks, parts, copper, semiconductors,
medium- and heavy-duty vehicles and buses, and the wood family.
Section 201 is zero against 0.080 percent because our slot fires only
on crystalline-silicon photovoltaic membership.

Section 122 is 6.435 percent against 2.969 percent, a difference of
3.47 points. This wedge is not closed. It is decomposed into declared
entry facts absent from the first version: General Note 6 civil-
aircraft utilization, which is sensitivity-only and covers 11.1
percent of value; USMCA and CAFTA entry status; partial-value facts;
and transit status. The remaining unencoded line-list layer is 0.92
percentage point, down from 6.58. These are accounting labels, not an
independent validation of closure.

# 8. Uses and limits

What the pair enables now is deliberately narrower than duty
assessment. The five-line witness still supports source-traceable,
posted ad valorem component-rate calculations on its guarded caller
surface. The generated schedule compositions now accept action-
membership inputs for arbitrary rated lines, with their posted general
or column-2 rate where that rate is ad valorem or Free. The action-
incidence layer is encoded, but the entry-level facts that determine
some exemptions and value bases are not inferred. The synthetic pilot
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

Nor do we claim effective rates, incidence, or behavioral response.
Trade-share weighting, exemption use, and de minimis composition are
estimation outside Section 3; nothing here says who bears a duty or how
trade reallocates. The synthetic entries reproduce observed margins
under declared assumptions but are not restricted transaction data,
and within-cell analyses such as importer concentration or the true
entry-size distribution are unsupported. The relevant ranges remain
separate: reconciliation covers five lines from the encoded temporal
start, margins cover January 2025 through June 2026, and the
spatially unrestricted pilot covers February through June 2026. A
joint application would require their true line-and-time intersection,
but no such composed result or committed intersection receipt is
reported here. The Section 7 schedule-scale averages inherit the same
discipline from the other side: they are exact evaluations of the
encoded scope. What remains outside is entry-level utilization, USMCA
and CAFTA entry status, partial value, transit status, and the non-metal
Section 232 family. The paper therefore does not estimate the complete
burden.

The natural next analyses — complete duty calculation, distributional
incidence, and tariff-revenue counterfactuals — sit one layer up, after
the fail-closed line guard, missing bases, quota state, finer timing,
and application receipt are supplied. Conflating that layer with this
paper would launder modeling assumptions through a dataset whose
claim to exactness is limited to reaggregation of declared margins.

# 9. Related work

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
tracker's internals; Section 5's
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
projects. The rulespec-us repository contains the tariff composition,
authority overlays, and companion tests. Axiom-oracles contains the
corpus manifests, comparison harness, conformance report, and the
authoritative disposition source. Microcosm contains the entries code
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
No archival release accompanies this local draft. Before release, the
project must also add the fail-closed five-line composition guard and
negative tests, regenerate and tripwire the disposition mirror, archive
the P2 outputs and review protocol, and retain the planned containerized
one-command rebuild and persistent identifier.

The Section 4 decomposition's leg outputs are committed in the public
scorecard repository [@scorecard_repo] at `f9e7acf` under
`data/pe/diagnostics/`, with the derivation annotation under
`sources/`; the weight bases with hash receipts, the 2025 recipe-build
log, the Census archive manifest chain, and the statistical-membership
map live in the project lane pending the archival release. The Section 7 generated schedule ships in the rules repository under
`us/policies/usitc/us-tariff-duty/lines/generated/` at merge
`f062088f`, with its reproducer
(`tools/generate_hts_rate_tables.py`), whose check mode re-derives and
byte-compares all 200 committed files. The full-schedule provisions
feedstock is corpus version
`2026-08-09-usitc-hts-2026-rev15-full-schedule`. The Section 7
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
described in Section 7 were produced by AI agents under the stated
gates, with human direction of scope, dispositions, upstream
communication, and publication. This manuscript was drafted by the
authoring agents from a primary-source-verified fact base and revised
through hostile, round-diff, red-team, and fresh-eyes referee passes.
The component-review reproducibility limit above applies; manuscript
review cannot substitute for the pinned artifacts and checks reported
with each claim. The human author is responsible for all claims.

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

## Table 4 — Three average-rate constructs from the composed schedule, April–June 2026 (§7)

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
| Section 201 | 0.000% | 0.080% | −0.080 point; our slot fires only on crystalline-silicon photovoltaic membership |
| Section 122 | 6.435% | 2.969% | +3.47 points; not closed: GN6 civil-aircraft utilization, USMCA/CAFTA entry status, partial-value facts, and transit status are declared inputs absent in version 1 |

The General Note 6 input is sensitivity-only and covers 11.1 percent
of value. The remaining unencoded line-list layer is 0.92 percentage
point, down from 6.58 in revision 9. The Section 122 labels decompose
an accounting wedge; they do not close it. The encoded stack carries
no antidumping or countervailing duties, and excluded cells receive no
effective-layer ad valorem equivalents.
