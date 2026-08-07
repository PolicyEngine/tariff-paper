# 1. Why 2026 broke tariff lookup

On February 20, 2026, the additional ad valorem duties imposed under
the International Emergency Economic Powers Act stopped being law. They
did not stop being collected. Executive Order 14389, implementing the
Supreme Court's decision in *Learning Resources v. Trump*
`[NEEDS CITATION: A2 — date, citation]`, ordered that the duties "shall
no longer be in effect and, as soon as practicable, shall no longer be
collected" — one sentence containing two different end dates, one legal
and one operational `[NEEDS CITATION: A1 — EO 14388 collection
endpoint]`. Any dataset that records "the tariff on Chinese imports in
February 2026" as a single number has already taken a position on which
of those dates counts, and most datasets do not say which position they
took.

That sentence is the 2025–26 tariff environment in miniature. Over
eighteen months, the United States imposed, modified, litigated, and
unwound overlapping duties under at least seven distinct authorities:
the column rates of the tariff schedule itself, Section 232 national-
security actions across metals and manufactured goods, Section 301
actions including a forced-labor program that added sixty
determinations under a new chapter-99 note `[NEEDS CITATION: A4]`, a
Section 122 balance-of-payments surcharge that arrived and expired
within its statutory 150-day limit `[NEEDS CITATION: A3]`, Section 201
safeguards on solar equipment stepping down on a proclamation schedule,
Section 338 duties, and the IEEPA orders whose termination opened this
section. The tariff schedule that these overlays modify was itself a
moving target: the United States International Trade Commission issued
revision after revision within the year `[NEEDS CITATION: A5 — count
as of 2026-08]`, each one changing line structure, statistical
suffixes, and in some revisions the operative rates.

The result is that the object researchers call "the statutory tariff
rate" became a function of four arguments — tariff line, partner
country, date, and legal interpretation — and the fourth argument is
the one nobody's spreadsheet has a column for. A rate query for
HTS 8541.43 from Malaysia on February 22, 2026 has two defensible
answers, and the difference between them is not a data error. It is a
fact about how the law ended: the legal authority died on the 20th,
the collection machinery wound down later, and an analysis of legal
exposure needs the first date while an analysis of customs revenue
needs the second.

Reference datasets handled this churn the way reference datasets
always have: with expert judgment applied by hand, encoded in scripts,
and published as numbers whose reasoning lives in commit messages if
it lives anywhere. The best of these — Yale Budget Lab's
tariff-rate-tracker, which we use as our validation reference
throughout this paper — resolves the churn into a
line-by-country-by-date panel with documented policy parameters, and
it is very good. It is also the product of judgment calls that a
reader cannot mechanically audit: which proclamation governs a line on
a date, when a staged schedule ends, which countries a general note
diverts to a different rate column. Sections 3 and 4 show what happens
when those calls are made checkable — including two places where the
best available reference and the underlying instruments disagree.

Our claim in this paper is narrow and, we think, timely: when the law
moves this fast, the honest representation of a tariff rate is not a
number but a dated derivation — a rule that cites the instrument that
set it, bounded by the instrument that ended it, executable so that
"the rate on date X" is computed rather than transcribed. The 2025–26
shock is the demonstration that this is not a formalist's luxury. When
rates change by proclamation monthly and die in two stages, the
derivation *is* the data.
