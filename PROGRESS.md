# Revision round 6 progress

## State

- Status: in progress.
- Baseline: `2845fd46044997d11d06d02af25db1ce3a9db7d7` on `master`; worktree clean at intake.
- Scope: paper-side repairs for referee findings F1, F2, M1, M2, M3, and all remaining minors.
- Hard gates: local commits only; no push, network, preprint, submission, contact, external-repository edits, authorship changes, or venue-slot changes.
- Artifact rule: verify every touched number-plus-unit claim against its pinned artifact before commit and grep-verify it afterward.
- External dependency boundary: any `axiom-oracles` or `microcosm` implementation/regeneration work will be recorded as an archival-release prerequisite, not performed here.
- Copy gate: locate and read `Message-House.md` before changing outward-facing manuscript copy; it is not tracked in this repository.

## Done

- Read the complete 170-line fresh-eyes referee report at `/Users/maxghenis/PolicyEngine/_buildo-runtime/reviews/sol_tariff_referee_r2.log`.
- Confirmed the requested baseline HEAD and a clean initial worktree.
- Read `PLAN.md` and captured its unchanged hard gates and honesty constraints.
- Identified the user-specified M1 scope override: paper-side correction and named axiom-side prerequisites only.

## Next

1. Locate and read `Message-House.md`.
2. Identify the repository-local final-report output path or create an explicit round-6 report path if none is designated.
3. Inventory every affected claim in `paper.md`, mirrored section drafts, tables, facts, and verification records.
4. Resolve pinned artifact references and independently verify the F1/F2 counts and all other touched quantitative claims.
5. Commit each coherent correction, refresh this ledger after each step, and finish with grep/test/render receipts.
