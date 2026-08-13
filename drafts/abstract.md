# Abstract

Tariff rates can cease legally before collection ends, so a statutory
rate needs a date, an instrument, and a derivation. We encode the
2025–26 United States tariff stack as versioned, instrument-cited
executable rules and reconcile their outputs cell by cell against Yale
Budget Lab's open tariff-rate tracker [@yaletracker_repo]. The primary
contribution is the rules-as-code and cross-implementation conformance
method. Its five tariff lines are a witness slice jointly selected so
that every in-scope authority binds somewhere; every disagreement in
the five-line reconciliation receives an evidence-backed disposition.
The schedule's rate columns then extend to all 13,790 rated lines as
deterministically generated, per-cell provision-grounded tables, gated
on reproducing the hand-built witness line modules' encoded rates
exactly. The same discipline applied across implementations shows that
the 1.6-point April–June 2026 gap between Yale Budget Lab's and the
Tax Policy Center's daily average-rate series is mostly the
import-weight vintage — 1.34 of the 1.62 points; rerunning Yale's own
pipeline on 2025 weights lands within 0.08 points of TPC — a
reconciliation we find published by neither organization. The exercise
also produces two proposed reference corrections, each supported by a
legal derivation and still awaiting maintainer response. An enabling data artifact converts
official monthly import margins into synthetic, weighted customs-entry
lines that reaggregate exactly, with assumptions recorded beside the
data. The implementation has material boundaries. The composition
contains five line predicates but no fail-closed domain guard, so
callers must restrict it to the witness slice: unsupported lines can
return plausible values rather than errors. The generated tables
publish posted rates and dispositions at full coverage, but their
application to entries is declared, deferred work. Its output is a posted ad
valorem component-rate stack under declared synthetic timing, not a
complete duty amount or revenue account; the inputs omit specific-duty
quantities, aluminum-content value, quota state, and sub-monthly timing.
We report the committed pins, hash-pin the local P2 outputs, and identify
the remaining synchronization and archival prerequisites.
