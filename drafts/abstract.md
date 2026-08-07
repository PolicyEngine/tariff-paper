# Abstract

When a tariff can be legally dead before it stops being collected,
"what is the statutory rate?" needs a date, an instrument, and a
proof. We encode the 2025–26 United States tariff stack as dated,
executable rules — the schedule's column rates by revision plus the
overlays imposed under Sections 232, 301, 201, 338, and 122 and under
IEEPA, including the IEEPA termination — at the legal-date semantics
under which a rule's version history answers for each day. Every rule
version cites its Federal Register instrument or tariff-schedule
provision with a verbatim excerpt, and terminations are themselves
encoded law rather than deletions. We reconcile the encoding
cell-by-cell against the leading open reference, Yale Budget Lab's
tariff-rate-tracker [@yaletracker_repo], on the tracker's own
line-by-country-by-date spine over its 2025–26 coverage: at the pinned
snapshot, 39,600 compared cells resolve to 24,400 exact matches and
15,200 discrepancies, every one of which is closed by an evidence-
backed disposition — zero remain unexplained and zero are open against
our encoding, with the full waterfall (coverage, temporal debt, and
four excluded reference constructs) reported in Section 3. The
reconciliation surfaced two author-attributed, derivation-backed, and
as-yet maintainer-unacknowledged reference defects — a safeguard rate
carried past its proclamation's staged schedule and missing column-2
handling for four countries — reported upstream with the legal
derivations. Separately, we release margin-exact synthetic customs
entries: eighteen months of Census import margins reconciled to the
integer dollar against the publisher's own control totals with zero
failures, and, over a five-month pilot window, weighted entry-line
allocations whose customs value reproduces every line-by-country-by-
month cell exactly, with every distributional assumption registered
beside the data. AI agents built the encodings and datasets behind
compile, test, and oracle gates, with same-project cross-model
adversarial review run until a pass with no findings; all code,
corpora, and evidence are public at pinned revisions.
