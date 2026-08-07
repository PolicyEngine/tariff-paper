# Executable tariff law: a conformance-tested statutory panel and synthetic customs entries for the 2025–26 trade shock

**Authors:** [slots — Max's call]
**Affiliations:** The Axiom Foundation; PolicyEngine
**Working paper draft — local only.**

# Abstract (exemplar — calibrates every later section)

When a tariff can be legally dead before it stops being collected,
"what is the statutory rate?" needs a date, an instrument, and a proof.
We encode the 2025–26 United States tariff stack as dated, executable
rules: column rates by tariff-schedule revision plus the §232, §301,
§201, §338, §122, and IEEPA overlays, including the IEEPA termination
order's own two endpoints ("no longer in effect" and "no longer
collected"). Every rule version cites its Federal Register instrument
or tariff-schedule heading with a verbatim excerpt, and terminations
are themselves encoded law rather than deletions. We validate the
encoding against the leading independent reference, Yale Budget Lab's
tariff-rate-tracker, on the tracker's own line-by-country-by-date
spine: at the pinned snapshot (dc1da3af), every in-scope cell is
exactly matched or carries an evidence-backed disposition, with zero
unexplained disagreements. The comparison surfaced two tracker defects,
a §201 rate carried past its proclamation's staged schedule and missing
column-2 handling for four countries; we reported both upstream with
the legal derivations. We also release synthetic transaction-level
customs entries that reproduce official Census import margins to the
integer dollar: eighteen months reconciled against the publisher's own
control totals with zero failures, 108,977 cells cross-checked exactly
over a second official channel, and every distributional assumption
registered beside the data. AI agents built the encodings and datasets
behind compile, test, and oracle gates, with independent cross-model
adversarial review run to zero findings. All code, corpora, and
evidence are public and pinned.


# 1. Why 2026 broke tariff lookup

On February 20, 2026, the additional ad valorem duties imposed under
the International Emergency Economic Powers Act stopped being law. They
did not stop being collected. That morning the Supreme Court held that
"IEEPA does not authorize the President to impose tariffs" (*Learning
Resources, Inc. v. Trump*, 607 U.S. 229 (2026)); the same day,
Executive Order 14389 ordered that the duties "shall no longer be in
effect and, as soon as practicable, shall no longer be collected" —
and named no date for the second clause. The date arrived two days
later in a Customs and Border Protection cargo-systems message (CSMS
#67834313), instructing that collection would end for goods entered on
or after 12:00 a.m. on February 24. So the legal end of the largest
tariff action of the era is a court decision and an executive order,
and its operational end is an agency bulletin — three documents, two
dates, four days apart. Any dataset that records "the tariff on
Chinese imports in February 2026" as a single number has taken a
position on which date counts, and most datasets do not say which
position they took.

That week is the 2025–26 tariff environment in miniature. Over
eighteen months, the United States imposed, modified, litigated, and
unwound overlapping duties under at least seven distinct authorities.
Alongside the IEEPA orders and their termination: Section 232
national-security actions across metals and manufactured goods;
Section 301 actions including a forced-labor program that determined
sixty investigations actionable at once, inserting a new chapter-99
note into the tariff schedule (U.S. note 52) with two rate tiers and
country-specific quotas; a Section 122 balance-of-payments surcharge
(Proclamation 11012) that ran at 10 percent for exactly its statutory
maximum of 150 days; Section 201 safeguards on solar equipment
stepping down annually on a proclamation schedule to a 2026 expiry;
and Section 338 duties. The seams between authorities are themselves
dated facts: the §122 surcharge expired at 12:01 a.m. on July 24,
2026 — the same day the forced-labor duties took effect. The tariff
schedule these overlays modify was a moving target in its own right:
the International Trade Commission's 2026 edition stood at Revision 15
by the first week of August, and a revision can carry a single
surgical change — Revision 15's only entry amends one chapter-99
heading, zeroing the Section 232 rate on United Kingdom patented
pharmaceuticals from +10 percent, four days after Revision 14.

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

Reference datasets handled this churn the way reference datasets
always have: with expert judgment applied by hand, encoded in
scripts, and published as numbers whose reasoning lives in commit
messages if it lives anywhere. The best of these — Yale Budget Lab's
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
# source: rulespec-us us/policies/usitc/us-tariff-duty/overlays/ieepa/termination.yaml@main (excerpt)
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
citing the order that zeroed it — which means the panel this encoding
generates carries the termination as a dated fact, exactly as it
carries the imposition. The two-endpoint character of the IEEPA wind-
down survives into the data because both endpoints are just versions.
A companion test evaluates the composed rates on the one-day period of
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

# 3. Conformance against an independent tracker

An encoding of tariff law can be internally consistent and wrong. The
validation that matters is external: derive the panel our rules imply
and reconcile it, cell by cell, against a reference built by people
who never saw our code. Yale Budget Lab's tariff-rate-tracker is the
strongest available reference — an actively maintained pipeline that
resolves the 2025–26 churn into statutory rate columns on a tariff-
line × country × date spine, with documented policy parameters and
sourced instrument files. We pinned its repository at one commit
(c4307e51), built its panel locally (1 hour 46 minutes wall time;
123.4 GiB peak memory footprint — an envelope we measured and reported
upstream, since the project's documentation suggested a much smaller
machine would do), and made its spine the conformance universe.

That last clause carries the methodology. The comparison universe is
generated from the reference's own spine — every tariff line, partner,
and date interval the tracker covers, not a curated sample of cells we
expected to match. The conformance predicate is unforgiving in the
same way: the encoding is conformant only when covered cells equal
in-scope cells, unexplained disagreements equal zero, and open
disagreements attributed to our encoding equal zero. There is no
partial credit and no averaging; a single unexplained cell fails the
predicate. Scope is declared, not discovered: the comparison covers
the tracker's statutory rate columns — the column rates and each
authority overlay, at the tracker's default legal-date convention —
and excludes its estimation-layer constructs (trade-share weightings,
utilization adjustments), which are modeling rather than law and are
validated at a different layer of our stack.

At the pinned snapshot (axiom-oracles report dc1da3af, 2026-08-03),
the predicate holds: ten of ten in-scope policies covered, zero
unexplained disagreements, zero open encoding-attributed
disagreements. The residue is disclosed rather than hidden. Four
exclusions are tripwired — carved out of scope with machine-checked
guards that fail the build if the excluded condition's footprint
moves, so an exclusion cannot quietly grow. 8,283 cells where the
disagreement is attributed to the reference are classified and carried
with evidence (Section 4 examines the two most consequential). And
49,200 interval-cells of temporal debt — panel intervals predating our
encoded domain or straddling its boundary — are surfaced as named debt
in the scoreboard rather than dropped, because an honest conformance
number states what it does not cover.

Reaching zero was iterative in a way worth reporting, since the
iteration is the method. The comparison harness itself went through
six adversarial review rounds before we trusted it: early versions
could report vacuous agreement (a slim CI artifact corrupted totals; a
column of zeros compared equal to a column of zeros it should never
have matched), and the reviews killed those with mutation tests —
deliberately corrupted inputs that a sound harness must catch. The
final harness binds each panel row to a content digest, rebuilds
byte-identically, and carries 2,396 tests. The number we report is
only as good as the machinery that computed it, and the machinery's
failure modes were hunted by a reviewer whose job was to break it.

Two boundaries on the claim. First, conformance is agreement with a
reference, and the reference is not ground truth — Section 4 shows it
disagreeing with the instruments it tracks, which is precisely why the
comparison stores derivations rather than trust. Second, the
adversarial review that gated every merge in this work is independent
in the cross-model sense (a different model family, prompted to
refute, with its findings closed by machinery), but it is not external
certification: reviewer and author sit inside the same project. A
separately governed verification protocol is future work, and until it
exists we state our verification as what it is.

# 4. When the oracle disagrees: dispositions with legal derivations

A conformance run that ends in disagreement forces a choice with three
honest outcomes: the encoding is wrong (fix it), the reference is
wrong (demonstrate it), or the two are answering different questions
(declare it). The disposition machinery exists to make the second and
third outcomes as auditable as the first. A disagreement attributed to
the reference cannot be waved through; it requires either the
reference maintainer's acceptance or an independent derivation from
the governing instruments, recorded beside the cells it explains. The
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
its end, citing the proclamation's table; the disagreement covers
every affected cell after the schedule moves. The derivation —
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
this writing, unacknowledged. The reports sit in the tracker's issue
queue with four others we filed en route — a locale-sensitivity bug
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
We release the bridge: a synthetic transaction-level dataset that
reproduces the public margins exactly and declares every assumption it
adds on the way down to entry grain.

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
it does, with zero tolerance and zero failures. The archives replace
an API path we built first and demoted: the equivalent extraction
through the Census International Trade API took thousands of calls and
failed server-side on the largest chapters, and the bulk files carry
strictly more detail. The API survives as something better than a
primary source — an independent second channel. A gated cross-check
fetches a stratified sample through the API and compares cell for
cell: 108,977 cells, exact on all four dollar measures, zero
mismatches. Two official channels agreeing is stronger provenance
than either alone.

**Down to entries, assumptions on the table.** The generator
disaggregates each (line × country × month) customs-value cell into
weighted synthetic entries. The identity constraint is absolute:
weighted customs value reproduces every cell to the integer dollar, on
an enforced domain (cell values at or below 2^53, where integer
arithmetic is exact; the build asserts the reproduction at run time
rather than trusting the construction). In the pilot window of
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
effect). Three fields have no public anchor at all — postal-shipment
status, sub-monthly timing, the shipment-value/customs-value
distinction — and each is set to a declared constant with a
sensitivity note, not imputed and forgotten. Every row carries
`is_synthetic = true`.

The honesty machinery extends to the anchors themselves. CBP's
statistics page mixes completed fiscal years with in-progress ones;
our parser emits in-progress years only as fiscal-year-to-date records
with explicit as-of endpoints, and it fails closed — wording it cannot
read, impossible calendar dates, notes displaced from their table,
endpoints later than the retrieval instant, all raise rather than
default. A fiscal year becomes an annual total only after its final
day has elapsed.

The result is not a substitute for the restricted transaction data,
and the paper does not offer it as one. It is the dataset that
downstream tariff microsimulation actually needs: entry-grain records
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

**The adversary.** Every substantive change merged in this work
passed independent adversarial review by a different model family,
prompted to refute rather than confirm, with each finding closed by a
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

The synthesis bears stating once, directly. The reason 2025–26 tariff
law could be encoded, validated to unexplained-zero, and released with
transaction-grain data inside the same year the law was moving is that
the marginal cost of rigor collapsed: agents wrote the 149-test
battery nobody budgets human-weeks for, re-derived the panel on every
change, and re-litigated every disagreement against primary
instruments. The gates are what let that speed compound instead of
compounding error.

# 7. Uses and limits

What the pair enables now. The statutory panel and the synthetic
entries share a contract — the entries' fields conform to the
composed spine's inputs — so duty computation runs at entry grain:
for any entry, the rate stack in force on its date, by authority,
with the derivation attached. That supports revenue accounting by
statutory component under any counterfactual expressible as dated
rules (repeal an authority, move a termination date, extend a staged
schedule), audit-grade rate lookup for any line × country × date in
the covered window, and calibration: the ingest's 302,318 consumer
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
concentration) should not run on them. The covered window is January
2025 through June 2026 for margins and the composed spine's domain
(February 2026 onward) for entry-level duty computation; the panel's
temporal debt outside the encoded domain is surfaced, not covered.

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
[fajgelbaum2020return]; Amiti, Redding, and Weinstein assembled the
same sequence for pass-through event studies [amiti2019impact;
amiti2020whos]; Flaaen and Pierce mapped tariff-line changes into
industry exposure measures [flaaen2019disentangling]. In each case the
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
rather than executable derivations [teti2024missing].

**The tracker we validate against.** The nearest neighbor to our
statutory panel is its own validation reference. Yale Budget Lab's
tariff-rate-tracker is an open-source pipeline producing an
interval-encoded panel of statutory rates at the tariff-line ×
country level for the 2025–26 regime, built from the trade
commission's schedule archives with documented policy parameters
[yaletracker_repo; budgetlab2026tracker]; the Budget Lab's rate
series are already the benchmark other measurement work checks
against [cavallo2026tracking]. We are not, therefore, the first
executable statutory tariff panel; the tracker is one, and a good
one. The contribution is the form and what the form enables: rules
at the instrument grain, each version citing and quoting its legal
source, with mandatory boundary tests — versus one pipeline whose
judgment calls live in code — and, on top of that form, a
cross-implementation conformance regime. To our knowledge the
conformance run of Section 3 is the first external research
engagement with the tracker's internals (we find no formal citation
of the tool itself as of August 2026), and Section 4's
derivation-backed defect reports are what that engagement produces
when a disagreement survives audit.

**Rules as code and calculator validation.** Executable encodings of
law have an established line: OpenFisca's deployed tax-benefit
engines [openfisca], Catala's formally grounded statute-to-code
language [merigoux2021catala], and the policy agenda articulated for
rules-as-code generally [mohun2020cracking]. Cross-validation is
likewise institutionalized practice in tax microsimulation — NBER's
TAXSIM as a reference implementation [feenberg1993introduction],
EUROMOD's country-report validation regime [sutherland2013euromod],
and maintained harnesses that reconcile independent calculators
line-by-line [taxcalculator_taxsim_validation]. That culture has not
previously reached trade law. Tariffs are, if anything, the easier
target for it — the instruments are public, the schedule is versioned
by the issuing agency, and the reference tracker already exists — and
the 2025–26 record supplies the volatility that makes the exercise
informative rather than ornamental.

**Synthetic microdata.** The synthetic-data tradition in official
statistics runs through disclosure avoidance: synthetic establishment
panels standing in for confidential business registers
[kinney2011towards], noise-infused releases with formal privacy
guarantees [machanavajjhala2008privacy], and, in transport and
demography, synthetic populations fit to published margins
[beckman1996creating]. Customs data specifically have seen synthesis
for machine-learning research — artificial Korean import declarations
generated for fraud-detection benchmarks [jeong2022customs] — while
the true U.S. transaction record remains restricted-access
[bernard2009importers; census_lfttd] or proprietary. Our entries
invert the disclosure-avoidance objective: the inputs are already
public, no confidentiality constraint binds, and the generator's
contract is exact integer reproduction of every published margin cell
with a declared assumptions register below that grain. We find no
prior public U.S. synthetic customs-entry dataset with that
contract — the combination this paper ships (instrument-cited
executable rules, a conformance verdict against an independent
implementation, and margin-exact public entries) appears to be
unoccupied, and we state the boundary of that claim as a search
bounded at August 2026 rather than a certainty.

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

# Tables (wire into sections at final assembly)

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
| Adversarial review at merge | P1: 12 rounds → APPROVE, no findings; P2: 4 rounds → APPROVE |
| Trade test battery at merge | 149 |

