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
not an evaluation error. The next layer narrows that boundary while keeping the witness as an
oracle; what remains after it is enumerated below — entry-level facts,
four action families (Brazil and forced-labor Section 301, the 2024
China action, solar) whose membership was fed as false, the tracker's
wider Section 232 family, and a residual line-list layer bundling
unencoded and vintage list differences, aircraft-exemption utilization,
partial-value facts, and basket and ad valorem equivalent differences.

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
