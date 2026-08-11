# Revision round 6 progress

## State

- Status: artifact audit complete; manuscript revisions in progress.
- Baseline: `2845fd46044997d11d06d02af25db1ce3a9db7d7` on `master`; worktree clean at intake.
- Scope: paper-side repairs for referee findings F1, F2, M1, M2, M3, and all remaining minors.
- Hard gates: local commits only; no push, network, preprint, submission, contact, external-repository edits, authorship changes, or venue-slot changes.
- Artifact rule: verify every touched number-plus-unit claim against its pinned artifact before commit and grep-verify it afterward.
- External dependency boundary: any `axiom-oracles` or `microcosm` implementation/regeneration work will be recorded as an archival-release prerequisite, not performed here.
- Copy gate: satisfied by reading all 155 lines of `/Users/maxghenis/TheAxiomFoundation/launch/Message-House.md`; it is not tracked in this repository.
- Final-report output: `research/revision-round-6-report.md` (no pre-existing output path was designated; this follows the repository's `research/*-report.md` convention).

## Done

- Read the complete 170-line fresh-eyes referee report at `/Users/maxghenis/PolicyEngine/_buildo-runtime/reviews/sol_tariff_referee_r2.log`.
- Confirmed the requested baseline HEAD and a clean initial worktree.
- Read `PLAN.md` and captured its unchanged hard gates and honesty constraints.
- Located and read the complete Axiom Foundation message house before any manuscript-copy edit. Its applicable guardrails include keeping interpretations visible, avoiding completeness claims, and pairing statistics with scope, denominator, and date.
- Identified the user-specified M1 scope override: paper-side correction and named axiom-side prerequisites only.
- Verified F1 at `microcosm@d4b0855`: 38,841,305 detail rows at the full publication grain and 3,070,851 district-aggregated HTS-10 × country × month margins.
- Verified F2 at `axiom-oracles@dc1da3af`: authoritative YAML dated 2026-08-03 has 30 entries covering 15,200 units, partitioned 8,283 + 6,917, with MFN 594 = 528 + 66; the public JSON mirror dated 2026-08-02 has 46 entries and an MFN footprint of 462 = 396 + 66.
- Verified M1 directly in `composition.yaml@dbf09f44`: five predicates but no domain guard, MFN off-slice fallback zero, in-window Section 122 fallback 10 percent, and additive total. Verified the generator at `6707ed59` has no HTS-line filter.
- Audited manuscript dependencies: no reported result applies the composition to the 3,806,050-row pilot, so the generator totals survive only when labeled all-line and spatially unrestricted; no locally recomputed intersection number will be introduced.
- Recorded the Axiom-side guard/tests, disposition-mirror synchronization, and review-protocol archive as named prerequisites in `PLAN.md`.
- Reframed the abstract and contribution hierarchy around rules-as-code conformance, with the synthetic entries as an enabling artifact rather than a complete duty or revenue result.
- Added pinned engine operational semantics and errors; replaced the false five-line gating claim with the actual caller precondition and off-slice fallthrough consequence.
- Corrected the Section 201 implementation description and made the Canada/February 24 endpoint an explicitly separate boundary probe from the Malaysia/February 22 trace.

## Next

1. Correct the conformance/disposition evidence chain, terminology, and exact partition.
2. Correct the data grains; add Data Records, field/weight/null/zero semantics, and re-scope the all-line pilot.
3. Narrow uses, limits, review claims, and availability/prerequisite language.
4. Update `research/verification-report.md`, perform before/after and forbidden-phrase greps, rebuild/check the PDF, and write the final report.
