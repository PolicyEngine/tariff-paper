# Revision round 6 progress

## State

- Status: revision round 6 complete.
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
- Bound the 30-entry disposition partition and 594-unit MFN footprint to the authoritative YAML's full pinned reference, including the exact 15,200 = 8,283 + 6,917 class receipt.
- Separated the policy-record `covered: true` field from covered interval-cells and corrected the Section 201 component account in the disposition narrative.
- Corrected F1 in prose and Table 2: 38,841,305 rows belong to the full detail grain; 3,070,851 belongs to district-aggregated HTS-10 × country × month margins.
- Added the Data Records relationship table, exact synthetic-entry fields, uniqueness/positive-cell/null/weight semantics, and supported-operation boundary.
- Re-scoped the five-month pilot as temporally inside the modeled window but spatially unrestricted across all positive HTS-line cells, with no composed result claimed.
- Hash-pinned the local P2 validation receipt (`45276e94…`) and named its archival inclusion as a release prerequisite.
- Replaced all affirmative duty-computation and revenue-accounting claims with caller-filtered posted-ad-valorem rate-stack capabilities and named the missing quantity, aluminum-content, quota-state, and sub-monthly inputs.
- Recast component-review rounds and verdicts as retrospective provenance; the mutation tests and pinned receipts now carry the evidentiary weight, with the missing review protocol stated explicitly.
- Quarantined the stale 46-entry/462-MFN public disposition mirror in Data and code availability, and listed regeneration plus a synchronization tripwire as a release prerequisite.
- Removed unarchived harness-test, review-round, and build-envelope counts from the result tables and narrative rather than using local-only values as validation evidence.
- Added the round-6 section to `research/verification-report.md`: exact pin/hash receipts, a touched-claim ledger, and quoted baseline/current lines for F1, F2, M1, M2, M3, all minors, and the style corrections.
- Completed the first living-source grep and draft-synchronization pass: negative grep PASS, required-positive grep PASS, all section/table mirrors PASS, and `git diff --check` PASS.
- Rebuilt `build/paper.pdf` as a 24-page, font-embedded US-letter artifact; added a minimal PDF preamble so exact pins and hashes wrap rather than clip, eliminated all overfull boxes, visually inspected every page plus full-size risk pages, and recorded final sha-256 `c3f03de66de171ddbefbcb7fa754c65e48cc097c37066f79155828910fe0d54e`.
- Corrected the last independent-audit residual in the abstract: committed pins are reported, while local P2 outputs are only hash-pinned. Repeated artifact replay, living-source and PDF greps, draft synchronization, front-matter preservation, and whitespace checks; all passed.
- Wrote the final report to `research/revision-round-6-report.md`, including the finding-to-commit-to-receipt table and `VERDICT: REVISION COMPLETE`.

## Next

1. No further paper-side round-6 work remains.
2. Before any future archival release, complete the four named prerequisites in `PLAN.md`; they are outside this paper-side task and remain gated on Max.
