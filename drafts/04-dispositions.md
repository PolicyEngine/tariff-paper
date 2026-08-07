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
safeguard's extension proclamation (10339) sets a staged duty schedule
with a final period ending February 6, 2026. The reference carries a
flat 14.5 percent on the affected lines past that date. Our encoding
carries the staged schedule and its end, citing the proclamation's
table; the disagreement covers every affected cell after the schedule
expires. The derivation — proclamation, table, terminal date — is
recorded in the disposition file, and the finding was filed upstream
with the same citations.

**Four countries on the wrong rate column.** The tariff schedule's
General Note 3(b) assigns column-2 rates — the punitive column — to a
small set of countries (Cuba, North Korea, Belarus, Russia
`[NEEDS CITATION: A6 — quote the note's current text]`). The
reference's parser has no column-2 branch, so those four countries
inherit column-1 base rates throughout its panel. The disagreement is
systematic rather than episodic — it touches every line for four
partners — and the derivation is a single sentence of the schedule's
own general notes. Filed upstream likewise.

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
