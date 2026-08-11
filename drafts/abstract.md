# Abstract

Tariff rates can cease legally before collection ends, so a statutory
rate needs a date, an instrument, and a derivation. We encode the
2025–26 United States tariff stack as versioned, instrument-cited
executable rules and reconcile their outputs cell by cell against Yale
Budget Lab's open tariff-rate tracker [@yaletracker_repo]. The primary
contribution is the rules-as-code and cross-implementation conformance
method. Its five tariff lines are a witness slice jointly selected so
that every in-scope authority binds somewhere, not an estimate of the
full schedule; every disagreement at the pinned snapshot receives an
evidence-backed disposition. The exercise also produces two proposed
reference corrections, each supported by a legal derivation and still
awaiting maintainer response. An enabling data artifact converts
official monthly import margins into synthetic, weighted customs-entry
lines that reaggregate exactly, with assumptions recorded beside the
data. The implementation has material boundaries. The composition
contains five line predicates but no fail-closed domain guard, so
callers must restrict it to the witness slice: unsupported lines can
return plausible values rather than errors. Its output is a posted ad
valorem component-rate stack under declared synthetic timing, not a
complete duty amount or revenue account; the inputs omit specific-duty
quantities, aluminum-content value, quota state, and sub-monthly timing.
We publish the pins and validation receipts and identify the remaining
synchronization and archival prerequisites.
