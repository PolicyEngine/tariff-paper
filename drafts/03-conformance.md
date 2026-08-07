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
