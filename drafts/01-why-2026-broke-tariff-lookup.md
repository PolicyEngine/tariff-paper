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
overlay authorities — IEEPA, Section 232, Section 301, Section 201,
Section 122, and Section 338 — the authority set the reference panel
of Section 3 tracks as statutory rate columns.
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
