---
title: "Executable tariff law: a conformance-tested statutory panel and synthetic customs entries for the 2025–26 trade shock"
author: "[Author slots — working draft, local only]"
date: 2026-08-07
bibliography: research/references.bib
link-citations: true
---

# Abstract

When a tariff can be legally dead before it stops being collected,
"what is the statutory rate?" needs a date, an instrument, and a
proof. We encode the 2025–26 United States tariff stack as dated,
executable rules — the schedule's column rates by revision plus the
overlays imposed under Sections 232, 301, 201, 338, and 122 and under
IEEPA, including the IEEPA termination — at the legal-date semantics
under which a rule's version history answers for each day. Every rule
version cites its Federal Register instrument or tariff-schedule
provision with a verbatim excerpt, and terminations are themselves
encoded law rather than deletions. We reconcile the encoding
cell-by-cell against the leading open reference, Yale Budget Lab's
tariff-rate-tracker [@yaletracker_repo], on the tracker's own
line-by-country-by-date spine over its 2025–26 coverage: at the pinned
snapshot, 39,600 compared cells resolve to 24,400 exact matches and
15,200 discrepancies, every one of which is closed by an evidence-
backed disposition — zero remain unexplained and zero are open against
our encoding, with the full waterfall (coverage, temporal debt, and
four excluded reference constructs) reported in Section 3. The
reconciliation surfaced two author-attributed, derivation-backed, and
as-yet maintainer-unacknowledged reference defects — a safeguard rate
carried past its proclamation's staged schedule and missing column-2
handling for four countries — reported upstream with the legal
derivations. Separately, we release margin-exact synthetic customs
entries: eighteen months of Census import margins reconciled to the
integer dollar against the publisher's own control totals with zero
failures, and, over a five-month pilot window, weighted entry-line
allocations whose customs value reproduces every line-by-country-by-
month cell exactly, with every distributional assumption registered
beside the data. AI agents built the encodings and datasets behind
compile, test, and oracle gates, with same-project cross-model
adversarial review run until a pass with no findings; all code,
corpora, and evidence are public at pinned revisions.

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
overlay authorities: IEEPA, Section 232, Section 301, Section 201,
Section 122, and Section 338.
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
the International Trade Commission's 2026 edition stood at Revision 15
by the first week of August, and a revision can carry a single
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

This paper's contributions are three, stated plainly. First, a
representation: the 2025–26 stack encoded as instrument-cited,
version-dated executable rules whose termination and revision events
are themselves rules, with mandatory boundary tests (Section 2).
Second, a validation regime: a cross-implementation reconciliation
against the leading open reference on its own spine, with an
unforgiving predicate, a disposition standard that prices reference-
attributed claims at a legal derivation, and a fully disclosed
waterfall — which in passing produced what we believe is the first
external research engagement with the reference's internals, and two
upstream defect reports (Sections 3–4). Third, a dataset: public,
margin-exact synthetic customs entry-line allocations with a
declared assumptions register, filling a gap the restricted
transaction data leave open (Section 5). The paper is a methods-and-
data contribution; the downstream analyses these enable — revenue
accounting under counterfactual rule histories, distributional
incidence — are deliberately out of scope (Section 7).

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

What the composed function computes, exactly: for a (tariff line,
partner country, calendar date) triple inside the encoded domain, the
ex-post statutory rate stack under legal-date semantics — each
authority's posted ad valorem contribution per the versions in force
that day, as the instruments read after the fact. Four things the
function deliberately does not resolve, because the inputs do not
determine them: intra-day boundaries (the instruments themselves
specify 12:00 versus 12:01 a.m. entry cutoffs; a date-grain panel
adopts the day), quota position (tariff-rate-quota lines depend on
cumulative entries to date), entry-specific facts (in-transit
exceptions, claimed exclusions), and knowledge-time (a version's
`effective_from` is legal-valid time; retroactive instruments are
encoded when published, so the panel is an ex-post record, not a
reconstruction of what was knowable on each day). Analyses needing
those distinctions need more state than this function's signature,
and Section 7 repeats the warning where it bites.

The full stack composes from these pieces. A composition module wires
the column rates of the tariff schedule to the authority overlays —
the Section 232 metal programs, the Section 301 families including the
forced-labor program, the per-country IEEPA reciprocal modules and
their fentanyl-order siblings, Section 122, Section 201, Section 338 —
and the engine evaluates the composed rate for a (line, country, date)
triple by resolving every overlay's version in force. Nothing in the
pipeline is hand-transcribed from a secondary source: the corpus
snapshot for this work comprises 138 signed versions — 47 Federal
Register instruments, 44 tariff-schedule revision snapshots, and 47
chapter-99 and general-note extractions — and every operative number
in the panel traces to one of them.

We do not claim this representation is novel as an idea; executable
encodings of statutes have a literature (Section 8), and dated
parameters are standard in tax microsimulation. The claim is about
fit: 2025–26 tariff law is the environment where the alternatives
visibly fail, because the thing being represented changed character.
A rate that steps down on a proclamation schedule, dies in two stages,
or applies to a line that stopped existing mid-year is not a cell in a
table. It is a small legal argument, and the representation that
survives contact with it is the one that stores the argument.

**A worked trace.** Take the solar-module query of Section 1 — a
crystalline-silicon module from Malaysia, February 22, 2026 — and
follow the version selection rather than inventing numbers. The
column-rate module for the line contributes its general rate per the
tariff-schedule revision in force that day. The Section 201 overlay's
staged versions — 14.75, 14.5, 14.25, 14 percent across the extension
proclamation's four annual periods [@proc10339_2022] — contribute
nothing: the final period's version ends February 6, 2026, the
schedule's own compilation marks the safeguard note expired, and no
later version exists, so the overlay's contribution on February 22 is
zero by absence of a version in force, not by an edit. The IEEPA
overlay resolves through the termination rule shown above: the
reciprocal version in force until February 19 is superseded by the
termination's zero from February 20 [@eo14389_2026], so the legal-
date answer carries no IEEPA contribution — while the collection
cutoff two days later [@csms67834313_2026] is, per the scope note,
outside this function's semantics. Every step of that paragraph is a
version lookup citing an instrument, which is the representation's
whole argument: the "two defensible answers" of Section 1 become two
different, explicit functions — and this paper's panel computes the
legal-date one.

# 3. Cross-implementation reconciliation against an independent tracker

An encoding of tariff law can be internally consistent and wrong. The
check this section reports is a cross-implementation reconciliation:
derive the panel our rules imply and reconcile it, cell by cell,
against a reference built by people who never saw our code. We are
deliberate about the term. The reference — Yale Budget Lab's
tariff-rate-tracker [@yaletracker_repo; @budgetlab2026tracker] — was
separately developed and is the series other measurement work already
benchmarks against [@cavallo2026tracking], but both implementations
read the same public instruments, its spine defines the comparison
universe (an omission from that spine is invisible to this exercise),
and our encoding iterated against the visible disagreements until the
predicate held. That is reconciliation between independent
implementations, which is the standard validation practice of tax
microsimulation transplanted to tariffs; it is not a held-out
evaluation, and Section 6 states what would upgrade it (a frozen
future snapshot, an independently double-coded legal sample, a third
implementation).

Definitions, so the numbers that follow are exact. A *cell* is a
(tariff line, partner, date-interval, concept) tuple on the
reference's spine, where a concept is one statutory rate column (the
column rate, or one overlay authority) or the total. An interval is
*covered* when our encoded domain spans it, and *temporal debt* when
it predates that domain or straddles its boundary — debt is surfaced,
never compared. A *comparison* evaluates one covered cell in both
implementations at the reference's default legal-date convention; a
*match* is exact equality. A *disposition* closes a mismatched cell
with a recorded claim — an encoding defect (which must then be fixed),
a reference-attributed discrepancy (Section 4's standard), or a
declared semantic difference — and a *tripwired exclusion* removes a
reference construct from scope entirely behind a machine-checked guard
that fails the build if the excluded construct's footprint moves.

The full waterfall at the pinned snapshot
(`dc1da3af`, 2026-08-03; reference at `c4307e51`; encoding at
`dbf09f44`; engine at `ffd82132`):

- The reference panel materializes 277,303,920 rows; the reconciled
  slice covers 240 partners over the tracker's 2025–26 coverage.
- Per policy, 68,400 in-scope date-intervals split into 20,400 covered
  and 48,000 temporal-debt intervals (our encoded rule history begins
  later than the tracker's panel start; the debt is the surfaced
  difference, and Section 7 carries it into the usage limits).
- Covered cells yield 39,600 comparisons: 24,400 exact matches (61.6
  percent raw) and 15,200 mismatches, with zero evaluation errors.
- Every one of the 15,200 enters a disposition; none remain
  unexplained, and none are open against our encoding. 8,283 cells
  carry reference-attributed dispositions under Section 4's standard;
  the per-class census, with each cell's concept, interval, and
  instrument, is in the committed disposition artifacts. At the
  concept level the mismatches sit in the Section 201 slot (7,887),
  the Section 122 slot (4,560), and the column-rate, IEEPA, and
  Section 232 slots (594, 476, 1,920) — concept counts overlap where
  one cell mismatches several concepts, so they exceed the 15,200
  distinct rows. Section 4 walks the two reference-attributed classes
  we escalated upstream; the remaining classes are recorded cell-by-
  cell in the same artifacts.
- Four reference constructs are excluded by tripwire, by name: the
  tracker's residual `other` column, its China-semiconductor 301 rate
  column, its stacking-output columns, and its Swiss-framework
  construct — each excluded for a recorded technical reason (zero
  exposure in the covered window or a construct our composition
  deliberately does not mirror), each with a guard that reds the build
  if its footprint becomes nonzero.

Ten of the reference's fourteen policy constructs are therefore
covered and conformant; four are excluded with tripwires; and the
conformance predicate — covered equals in-scope, unexplained equals
zero, open encoding-attributed equals zero — holds on the covered
slice. We report the 61.6 percent raw match rate as prominently as the
zero because the two numbers mean different things: the raw rate is
what falls out before any human judgment; the zero is what survives
after every judgment is recorded, attributed, and exposed to audit.
A reader who distrusts our dispositions can recompute the raw rate
from the committed artifacts and re-litigate any cell.

The comparison machinery earned its own scrutiny before we trusted
its numbers. The harness went through six adversarial review rounds;
early versions could report vacuous agreement (a slim CI artifact
corrupted totals; an all-zero column compared equal to an all-zero
column it should never have matched), and the reviews killed those
with mutation tests — deliberately corrupted inputs a sound harness
must catch. The final harness binds each panel row to a content
digest, rebuilds byte-identically, and carries 2,396 tests; its
closing review swept 220 committed reports for predicate
disagreements and found none. Mutation tests validate the comparator,
not the law — the legal-correctness burden rests on the instrument
citations of Section 2 and the derivation standard of Section 4.

We also measured the reference's reproduction cost, since our
supervised rebuild of it is part of the reconciliation's provenance:
1 hour 46 minutes wall time and a 123.4 GiB peak memory footprint on
a 128 GiB workstation, against documentation suggesting a far smaller
machine — reported upstream, alongside a proposal that the project
publish its panel as a release artifact so downstream users can skip
the build entirely.

# 4. When the oracle disagrees: dispositions with legal derivations

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
after February 2026. Our encoding carries the staged schedule and
its end, citing the proclamation's table; the disagreement's recorded footprint is the
affected lines after the schedule moves, enumerated in the disposition
artifact (the Section 201 concept slot's 7,887 mismatched cells of
Section 3 are dominated by this class). The derivation —
proclamation, annex table, terminal date, the schedule's own expiry
note — is recorded in the disposition file, and the finding was
filed upstream with the same citations.

**Four countries on the wrong rate column.** The tariff schedule's
General Note 3(b) directs that "the rates of duty shown in column 2
shall apply to products, whether imported directly or indirectly, of
the following countries and areas": the Republic of Belarus, Cuba,
North Korea, and the Russian Federation. The reference's parser has
no column-2 branch, so those four countries inherit column-1 base
rates throughout its panel. The disagreement is systematic rather
than episodic — it touches every line for four partners — and the
derivation is a single sentence of the schedule's own general notes,
with the note's cross-reference to the Russia and Belarus additional-
duty headings compounding the gap. Filed upstream likewise.

We report both findings as what they are: derivation-backed and, as of
this writing, unacknowledged. The reports sit in the tracker's issue queue with our four other
filings (five issues and one patch pull request in all) — a locale-sensitivity bug
that corrupted country matching (with a patch), the measured build
envelope of Section 3, and a proposal that the project publish its
panel as a release artifact, which would let every downstream user
skip the 123 GiB build we measured. None of this is offered as fault-
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

# 5. Synthetic customs entries from official margins

The statutory panel answers what the rate was. Applying it to trade
requires the other half: what crossed the border, at what value, in
which tariff line, from where. The public record answers this at the
margin — monthly totals by line, country, and district — while the
transaction-level record (the entry summaries importers actually file)
is either restricted to secure-enclave access or not assembled at all.
We release the bridge: weighted synthetic entry-line allocations
whose customs value reproduces the public margins exactly at a stated
grain, with every assumption below that grain declared. Two scopes
govern everything in this section and must not blur: the margins
ingest covers eighteen months at line-by-country-by-district-by-month
grain; the entry-level generator covers a five-month pilot window and
reproduces the customs-value measure at line-by-country-by-month
grain, district-aggregated.

**The margins, from the loading dock rather than the front door.**
Census publishes the complete monthly U.S. Imports of Merchandise
database as public archives — one ZIP per month, no authentication, at
a stable URL pattern. Eighteen archives (January 2025 through June
2026, ~3.3 GB, every byte sha-manifested at retrieval) parse under the
record layouts shipped inside the archives themselves into 38,841,305
detail rows: tariff line × partner country × customs district × month,
with twenty-two monthly measures spanning customs value, dutiable
value, calculated duty, charges, quantities, and air/vessel/
containerized transport splits. The same archives carry the
publisher's own control-total files, which makes reconciliation an
internal affair: our parse must reproduce Census's own totals, in
integer dollars, on three independent axes — by country, by commodity,
by district. Across all eighteen months and every published measure,
it does, with zero tolerance and zero failures. The archives replace an API path we built first and demoted: the
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
weighted synthetic entries. The identity constraint is absolute:
weighted customs value reproduces every line-by-country-by-month cell
to the integer dollar. The arithmetic earns the word exact: cross-
cell aggregations run in arbitrary-precision Python integers (the
review of Section 6 caught and killed a fixed-width accumulation that
could wrap), cell values are validated at or below 2^53 so their
parquet representation is exactly representable, and the build
asserts the reproduction at run time rather than trusting the
construction. In the pilot window of
February through June 2026 — chosen to sit inside the composed
statutory spine's domain — 3,806,050 entry rows carry 44,881,145
weighted entries and a weighted customs value of $1,467,109,590,515,
equal to the window's margins total exactly.

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
ones its contract supports: entry-grain records
whose margins are exactly the official ones, whose every departure
from the observable record is enumerated, and whose fields conform to
the statutory spine's input contract — so that the panel of Section 3
and these entries compose into duty computation at the grain where
duties are assessed.

# 6. Provenance engineering

Every number in this paper is recomputable from public artifacts, and
the machinery that makes that true was built by AI agents. We state
both facts plainly because together they are the methods section: the
pipeline's outputs are only trustworthy because its architecture
assumes its authors — human or model — will err, and gates
accordingly.

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

**The adversary.** Every pull request merged in the repositories
this paper reports on passed same-project cross-model adversarial
QA — a reviewing agent from a different frontier model family (an
OpenAI GPT-5.6-class reviewer against Anthropic Claude-class
authoring agents) prompted to refute rather than confirm, with each finding closed by a
code change and a test that fails on the pre-fix implementation —
mutation-proven, not narrated. The entries pipeline of Section 5 is
the instructive case: its publication machinery (atomic directory
replacement with crash recovery) went through eight consecutive review
rounds, each finding a strictly narrower defect class than the last —
symlink-target validation before recursive deletion, a race in lock
takeover, asynchronous exceptions landing after a rename's commit
point, rename durability ordering under power loss — until the final
round found the structural invariant the piecewise fixes had been
approximating: no recovery marker may be removed until every mutation
it records is durable. The reviewer's last pass swept every marker-
removal site against that invariant, verified the closing test fails
on the previous implementation, and returned no findings. We report
the trajectory rather than just the endpoint because the trajectory is
the evidence: a review process that converges to zero by narrowing
finding classes is doing something different from one that runs out of
patience.

**The division of labor.** Model-written code, model-run reviews,
machine-checked gates — and human judgment exactly where it is load-
bearing: scope decisions (what counts as law versus estimation), the
disposition standard of Section 4, anything that leaves the project
(upstream reports, this paper), and the decision to ship. We do not
claim the review regime is external certification; Section 3 states
that boundary. We do claim the artifact trail is complete enough that
a skeptic need not trust any of it: the encodings, the corpus
manifests, the comparison harness, the entries pipeline, the review
verdicts, and the evidence packs (build reports, reconciliation
records, cross-check reports) are public, pinned, and re-runnable.

One synthesis sentence, scoped to what this project observed: the
gate-and-adversary architecture is what allowed agent speed — the
149-test battery, the per-change panel re-derivations, the twelve
review rounds — to accumulate as checked artifacts rather than as
unchecked claims.

# 7. Uses and limits

What the pair enables now. The statutory panel and the synthetic
entries share a contract — the entries' fields conform to the
composed spine's inputs — so duty computation runs at entry grain:
for any entry, the rate stack in force on its date, by authority,
with the derivation attached. That supports revenue accounting by
statutory component under any counterfactual expressible as dated
rules (repeal an authority, move a termination date, extend a staged
schedule), source-traceable rate lookup — every value carrying its instrument
citations — within the stated domain, and calibration: the ingest's 302,318 consumer
facts publish at five aggregation grains with channel-invariant keys,
built to serve as calibration targets for population synthesis
downstream.

What the pair does not claim. No effective rates: trade-share
weighting, exemption utilization, and de minimis composition are
estimation, deliberately out of the conformance scope of Section 3.
No incidence and no behavioral response: nothing here says who bears
a duty or how trade reallocates when one changes; the entries
reproduce observed margins under declared assumptions and do not
model responses to counterfactuals. Computed duty at statutory rates
is not collected revenue: exclusions in litigation, drawback,
misclassification, and the wind-down mechanics of terminated
authorities all wedge between the two, and our own comparison treats
calculated-duty fields as related-never-gating for exactly this
reason. The synthetic entries are not the restricted transaction
record: within-cell structure below the margins is assumption, the
register says which assumption, and analyses that depend on within-
cell joint distributions (entry-size inequality, importer
concentration) should not run on them. Four ranges govern use and are stated wherever a claim depends on
them: the rule history runs to the instruments' own dates; the
reconciliation of Section 3 covers the reference spine's 2025–26
coverage with 48,000 pre-domain interval-cells surfaced as temporal
debt rather than compared; the margins cover January 2025 through
June 2026; and entry-level duty computation is defined on the
composed spine's domain (February 2026 onward) intersected with the
pilot allocations (February through June 2026) — a window that ends
before the July 24 seam and the August revision, which the margins
record but the pilot does not reach.

The natural next analyses — distributional incidence of the 2025–26
stack, tariff-revenue swaps against other instruments — sit one layer
up, where these statutory computations meet household and firm
microdata. That layer exists in our stack but is not this paper, and
conflating the two would launder modeling assumptions through a
dataset whose claim to exactness is precisely that it added none it
did not declare.

# 8. Related work

**Tariff-rate data for the trade-war literature.** The empirical
literature on the 2018–19 tariffs built its rate data by hand, wave by
wave. Fajgelbaum, Goldberg, Kennedy, and Khandelwal digitized each
wave's product lists and statutory rates from the official
announcements to estimate the trade war's incidence
[@fajgelbaum2020return]; Amiti, Redding, and Weinstein assembled the
same sequence for pass-through event studies [amiti2019impact;
amiti2020whos]; Flaaen and Pierce mapped tariff-line changes into
industry exposure measures [@flaaen2019disentangling]. In each case the
tariff schedule is a bespoke research input, frozen at publication.
Bown's widely used trackers institutionalized the hand-compiled
approach as a maintained public timeline [bown2021uschina;
bown_piie_chart]. The 2025–26 environment strains this tradition on
two margins the earlier waves mostly spared it: authority count
(seven overlapping legal bases with distinct lifecycles) and tempo
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
[@yaletracker_repo; @budgetlab2026tracker]; the Budget Lab's rate
series are already the benchmark other measurement work checks
against [@cavallo2026tracking]. We are not, therefore, the first
executable statutory tariff panel; the tracker is one, and a good
one. The contribution is the form and what the form enables: rules
at the instrument grain, each version citing and quoting its legal
source, with mandatory boundary tests — versus one pipeline whose
judgment calls live in code — and, on top of that form, a
cross-implementation conformance regime. We find no formal citation of the tool itself as of August 2026
(a web-bounded search; the tool is four months old), which suggests —
though a negative search cannot establish — that Section 3's
reconciliation is the first external research engagement with the
tracker's internals; Section 4's
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
line-by-line [@taxcalculator_taxsim_validation]. That culture has not
previously reached trade law. Tariffs are, if anything, the easier
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
contract is exact integer reproduction of every published margin cell
with a declared assumptions register below that grain. We find no prior public U.S. synthetic customs-entry dataset with
that contract; the claim is bounded by our search (August 2026) and
Section 1's contribution list is written to survive even if one
surfaces — the representation and the reconciliation regime do not
lean on the dataset's novelty.

# Data and code availability

Everything this paper reports predates it in public. The encodings
live in the rulespec-us repository (the tariff composition and its
authority overlays, with mandatory companion tests); the corpus
manifests, comparison harness, conformance reports, and disposition
records in axiom-oracles, with the quoted scoreboard pinned at
snapshot dc1da3af; the entries pipeline, its 149-test battery, and the
committed evidence packs (build report, source manifest, eighteen
per-month reconciliation records, the gated cross-check report) in the
Microcosm repository, merged as pull requests #620 and #621 with the
full adversarial review inventories in their descriptions. The Yale
reference is pinned at commit c4307e51 of Budget-Lab-Yale/
tariff-rate-tracker; our six upstream reports are public issues on
that repository. The Census source archives are public no-auth
downloads whose URL pattern, sizes, and sha-256 digests appear in the
committed source manifest; the CBP page bytes our anchors parse from
are archived beside the facts they ground.

Replication is therefore not a package assembled for this paper but
the working state of the projects it reports on: re-running the
conformance derivation at the pinned revisions reproduces the
scoreboard; re-running the entries build against the manifested
archives reproduces the artifacts byte-for-byte, a property the review
regime enforced rather than aspired to.

**Pinned revisions.** Encoding: rulespec-us
`dbf09f44eddd00b7ad5520f89371ebe8fdf0b7df`. Engine:
axiom-rules-engine `ffd8213271947b0189a9dd61a055c1e0e78908a0`
(v0.1.0; binary sha-256 `674ca6e7…bbe32d7`). Reconciliation snapshot:
axiom-oracles `dc1da3af067c50fa7138458faf3703b4b9efd7cb`. Reference:
Budget-Lab-Yale/tariff-rate-tracker
`c4307e514196618afcbf88cf7fd33746417eeabf` (MIT). Entries pipeline:
microcosm merge commits `d4b0855157af996bd367146bc200a2f72ee7d15d`
(ingest) and `6707ed5912d33ff0a340474a1a24f31546c6dec5` (generator).
An archival release with containerized one-command replication and a
persistent identifier accompanies submission; until then the commits
above are the replication interface.

**AI-use disclosure.** The encodings, pipelines, tests, and reviews
described in Section 6 were produced by AI agents under the stated
gates, with human direction of scope, dispositions, upstream
communication, and publication; this manuscript was drafted by the
authoring agents from a verified fact base and revised under the same
adversarial-review regime, with the human author responsible for all
claims.

## Table 1 — Conformance scoreboard at the pinned snapshot (§3)

Source: axiom-oracles report `dc1da3af` (2026-08-03); reference =
Budget-Lab-Yale/tariff-rate-tracker @ `c4307e51`.

| Quantity | Value |
|---|---|
| In-scope policies covered | 10 / 10 |
| Unexplained disagreements | 0 |
| Open disagreements attributed to the encoding | 0 |
| Tripwired scope exclusions | 4 |
| Reference-attributed cells, classified with evidence | 8,283 |
| Temporal debt surfaced (pre-domain intervals) | 48,000 |
| Temporal debt surfaced (domain-straddling intervals) | 1,200 |
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

# References
