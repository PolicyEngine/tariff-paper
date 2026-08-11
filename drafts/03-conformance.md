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
depth-first deliberately — the two reference-attributed findings of Section 4
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
a reference-attributed discrepancy (Section 4's standard), or a
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
  difference, carried into Section 7's usage limits.
- The covered intervals yield 39,600 probe-date comparisons (5 lines
  × 240 partners × 33 probes): 24,400 exact matches (61.6 percent
  raw) and 15,200 mismatches, with zero evaluation errors.
- Every one of the 15,200 enters a disposition; none remain
  unexplained, and none are open against our encoding. The authoritative
  file partitions them into 30 entries — every mismatched unit appears
  in exactly one — and the class arithmetic closes explicitly:
  **15,200 = 8,283 `upstream_engine_gap` units in 10 entries + 6,917
  `explained_residual` units in 20 entries.** Its families include the
  IEEPA metals-exclusion layer, the column-2 reference gap of Section 4,
  a Section 232 aluminum-content basis on beer, a free-trade-agreement
  preference layer, a Section 122 metal exclusion, and the Section 201
  safeguard expiry of Section 4; each entry records its concept, case
  selector, and instrument citations. At the
  concept level the mismatches sit in the Section 201 slot (7,887),
  the Section 122 slot (4,560), and the column-rate, IEEPA, and
  Section 232 slots (594, 476, 1,920) — concept counts overlap where
  one cell mismatches several concepts, so they exceed the 15,200
  distinct units. In the authoritative dispositions, the MFN footprint
  is 594 units: 528 in the column-2 family plus 66 in the preference
  family. Section 4 walks the two reference-attributed classes
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
citations of Section 2 and the derivation standard of Section 4.

We also measured the reference's reproduction cost in a supervised
local rebuild and reported the unexpectedly large resource envelope
upstream, alongside a proposal that the project publish its panel as a
release artifact. Because that measurement receipt is not committed at
the named pins, this paper does not use its numerical value as evidence.
