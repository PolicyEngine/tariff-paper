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

Evaluating the composed schedule economy-wide is what turns the
witness's scope boundary from a caveat into a measurement. Weighted
by the rebuilt 2024 import basket, the encoded law's statutory stack
averages 12.34 percent over April–June 2026 (12.07 on 2025 weights;
realized collections, a different construct entirely, run 6.81
percent), on 83.4 percent of basket value — the remainder being specific, compound, and conditional cells
the machinery classifies rather than force-parses. The by-authority
decomposition then shows exactly where encoding ends: the balance-of-
payments surcharge and the pre-termination emergency layers, which
attach by origin or economy-wide, appear at full statutory incidence,
while the line-list actions — the China Section 301 lists, the
Section 232 derivative annexes, Sections 201 and 338 — contribute
essentially nothing beyond the witness lines, because the witness
encodes their incidence as five literal line equalities. A replay of
the certified oracle slice through this evaluation path reproduces
all 1,300 extract comparisons exactly, so the boundary is in the
encoded incidence, not the evaluation.

Set beside the tracker rerun of Section 4 — reported alongside, not
as a like-for-like comparison — the distance decomposes into two
independently measured wedges and one balancing residual. The
unencoded line-list layer carries 6.58 points of the window mean on
the tracker's own decomposition columns, and the surcharge's
exemption and stacking structure, which the five-line witness never
exercised, accounts for 7.03 points of overapplication in our
flat-incidence evaluation: both magnitudes come from the tracker's
per-authority columns, not from fitting. The remaining 1.16 points is
a balancing residual by construction — the shared-scope difference
minus the surcharge wedge — bundling basket composition, ad valorem
equivalents for the excluded cells, and anything else; the resulting
closure to the rerun mean (10.72) is therefore an accounting
identity, not an independent gate, and the evidence bundle records it
as report-only. What the decomposition establishes is bounded but
real: the two dominant, independently measured wedges are the
unencoded incidence layer itself, in both directions. Table 4 reports
the constructs with these disclosures. The incidence layer —
membership tables for the action lists and the surcharge's exemption
structure, generated from the corpus-retained chapter 99 notes under
the same gate ladder — is the declared next stage; until it lands,
the average-rate series stay concept-separated, with the two
dominant separations independently quantified and the remainder
carried as a named residual.
