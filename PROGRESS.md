# Revision round 6 progress

## State

- Status: in progress.
- Baseline: `2845fd46044997d11d06d02af25db1ce3a9db7d7` on `master`; worktree clean at intake.
- Scope: paper-side repairs for referee findings F1, F2, M1, M2, M3, and all remaining minors.
- Hard gates: local commits only; no push, network, preprint, submission, contact, external-repository edits, authorship changes, or venue-slot changes.
- Artifact rule: verify every touched number-plus-unit claim against its pinned artifact before commit and grep-verify it afterward.
- External dependency boundary: any `axiom-oracles` or `microcosm` implementation/regeneration work will be recorded as an archival-release prerequisite, not performed here.
- Copy gate: satisfied by reading all 155 lines of `/Users/maxghenis/TheAxiomFoundation/launch/Message-House.md`; it is not tracked in this repository.

## Done

- Read the complete 170-line fresh-eyes referee report at `/Users/maxghenis/PolicyEngine/_buildo-runtime/reviews/sol_tariff_referee_r2.log`.
- Confirmed the requested baseline HEAD and a clean initial worktree.
- Read `PLAN.md` and captured its unchanged hard gates and honesty constraints.
- Located and read the complete Axiom Foundation message house before any manuscript-copy edit. Its applicable guardrails include keeping interpretations visible, avoiding completeness claims, and pairing statistics with scope, denominator, and date.
- Identified the user-specified M1 scope override: paper-side correction and named axiom-side prerequisites only.

## Next

1. Identify the repository-local final-report output path or create an explicit round-6 report path if none is designated.
2. Inventory every affected claim in `paper.md`, mirrored section drafts, tables, facts, and verification records.
3. Resolve pinned artifact references and independently verify the F1/F2 counts and all other touched quantitative claims.
4. Commit each coherent correction, refresh this ledger after each step, and finish with grep/test/render receipts.
