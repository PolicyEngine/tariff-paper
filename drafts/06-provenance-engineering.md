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
the full revision series for 2025 and 2026 as pinned snapshots. And applying a line's rate to an
entry remains composition-layer work each module declares as a
deferred output: the tables publish what the schedule says, at full
coverage, and do not alter the five-line witness composition of
Sections 2–3.
