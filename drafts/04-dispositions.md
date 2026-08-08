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
