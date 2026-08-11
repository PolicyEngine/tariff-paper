# Tariff paper revision round 6 — final report

Date: 2026-08-11  
Baseline: `2845fd46044997d11d06d02af25db1ce3a9db7d7`  
Final manuscript and audit checkpoint: `45d1840d339cceef87bb13b2f77830061e702aaa`  
Scope: paper-side resolution of F1, F2, M1, M2, M3, every listed minor,
and the stylistic findings in the fresh-eyes referee report.

## Outcome

The requested paper-side revision is complete. The manuscript now identifies
the two import-data grains correctly, binds the disposition claims to the
authoritative pinned YAML while quarantining the stale same-pin public mirror,
describes the composition's real off-slice behavior, limits the executable
output to a posted ad valorem component-rate stack, and supplies both the
operational-semantics and Data Records treatments requested under M3.

No reported paper result depends on an invented five-line runtime guard. The
3,806,050-row pilot remains a valid all-line data-construction result because it
is now labeled spatially unrestricted and is not presented as a tariff-
composition output. No replacement intersection count was invented.

The complete claim ledger, exact source references, and full before/after
quotation set are in `research/verification-report.md`, Section C. The final PDF
is `build/paper.pdf`.

## Artifact-exact receipts

All source-project reads used `git show <pin>:<path>`, rather than mutable
working-tree files.

| Claim family | Pinned or hash-pinned evidence | Replayed receipt |
|---|---|---|
| F1 data grains | `microcosm@d4b0855157af996bd367146bc200a2f72ee7d15d:docs/evidence/us-import-entry-margins/build_report.json` and pinned ingest code | 38,841,305 full-grain detail rows; 3,070,851 HTS-10 × country × month margins; 302,318 consumer facts; 18 months; 0 reconciliation failures. |
| F2 authoritative dispositions | `axiom-oracles@dc1da3af067c50fa7138458faf3703b4b9efd7cb:dispositions/us-tariff-panel.yaml` | 30 entries and 15,200 distinct units: 10 entries / 8,283 `upstream_engine_gap` + 20 / 6,917 `explained_residual`; MFN 594 = 528 column-2 + 66 preference. |
| F2 stale public mirror | Same pin, `dashboard/public/data/dispositions/us-tariff-panel.json` | Dated 2026-08-02; 46 entries; MFN 462 = 396 + 66. It is not evidence for the paper's disposition claims. |
| Comparison universe | Same pin, `reports/axiom-yale-us-tariff-panel-all-2026-08-03.json` | 5 lines, 240 countries, 39,600 comparisons, 24,400 matches, 15,200 mismatches, MFN 594, 0 errors. |
| M1/M2 mechanism | `rulespec-us@dbf09f44eddd00b7ad5520f89371ebe8fdf0b7df:us/policies/cbp/us-tariff-duty/composition.yaml` | Five predicates but no top-level guard; MFN `else: 0`; in-window §122 blanket fallback; explicit additive total; beer column-2 13.2¢/liter outside the ad valorem component; beer §232 applicability exposed while the component returns zero without the content basis. |
| Pilot scope and totals | Generator `microcosm@6707ed5912d33ff0a340474a1a24f31546c6dec5`; local validation, assumptions, and parquet hashes in the verification report | Month and positive-value filters only, no HTS filter; 889,169/889,169 cells exact; 3,806,050 rows; 44,881,145 weighted entries; $1,467,109,590,515; `exact: true`; all three declared hashes match. |
| M3 engine semantics | `axiom-rules-engine@ffd8213271947b0189a9dd61a055c1e0e78908a0` docs and source | Inclusive bounds at query-period start; greatest applicable `effective_from`; gaps error; equal-start ties fall through to document order; authored branches and explicit addition govern precedence/stacking; unknown, missing, type, scalar/judgment, and division-by-zero errors are explicit. |

## Before/after digest

F1 changed the Table 2 claim from:

> `Margin cells (HTS-10 × country × district × month) | 3,070,851`

to two separately verified rows:

> `Full-grain detail rows (HTS-10 × country × subcode × entry district × unlading district × rate provision × month) | 38,841,305`
>
> `District-aggregated margin cells (HTS-10 × country × month) | 3,070,851`

F2 replaced a generic snapshot reference with the full authoritative
`axiom-oracles@dc1da3af…:dispositions/us-tariff-panel.yaml` reference and added:

> “The public mirror has 46 entries and an MFN footprint of 462 … it is
> stale … and must be regenerated from the authoritative source under a
> synchronization tripwire before archival release.”

M1 replaced:

> “the pinned composition gates on the five witness lines”

with:

> “The filter is a caller obligation: the pinned composition has five
> predicates but no domain guard, and an off-slice call may return a plausible
> value rather than an error.”

The pilot wording now says its dates are inside the modeled temporal window,
but the generator is spatially unrestricted, applies no HTS-line filter, and
has no reported composed-rate result.

M2 replaced affirmative “duty computation” and “supports revenue accounting”
language with:

> “Applying the statutory composition requires first filtering to the five
> witness lines and returns only a posted ad valorem component-rate stack.”
>
> “What the pair does not enable is complete duty or revenue accounting.”

The manuscript now names the missing specific-duty quantities,
aluminum-content value, quota state, and sub-monthly timing.

M3 replaced the underspecified formal-domain paragraph with an operational-
semantics table covering time, version selection, ties, precedence, stacking,
types, errors, and rate-versus-money behavior. Section 5 now has a Data Records
table plus the exact entry fields, observational keys, artifact relationships,
weight meaning, zero/null handling, and supported-operation boundary.

The minor and style changes additionally distinguish proof atoms from the
operative §201 zero, separate the Malaysia and Canada traces, describe five
lines as a joint witness design, separate policy-record coverage from interval-
cell coverage, state `15,200 = 8,283 + 6,917`, limit review verdicts to
retrospective provenance, and make rules-as-code conformance the primary
contribution. A final independent audit also changed “We publish the pins and
validation receipts” to “We report the committed pins, hash-pin the local P2
outputs.”

## Verification and gates

Final post-commit checks at `45d1840` returned:

```text
clean_tree=PASS
postcommit_negative_grep=PASS
postcommit_positive_grep=PASS
postcommit_pdf_grep=PASS
postcommit_draft_sync=PASS
pdf_hash=PASS
diff_check=PASS
independent_final_claim_audit=PASS
independent_final_receipt_audit=PASS
```

The PDF is 24 US-letter pages with embedded Palatino and Latin Modern Mono
fonts. Its sha-256 is
`c3f03de66de171ddbefbcb7fa754c65e48cc097c37066f79155828910fe0d54e`.
The final XeLaTeX pass has no overfull boxes or unresolved citations. Visual
review found no clipping, collisions, malformed lists, or unreadable tables.

The title, local-only author slot, and venue plan are unchanged. No push,
network access, preprint, submission, external contact, archival release, or
source-repository edit was performed. `Message-House.md` was read in full before
the manuscript copy pass.

## Archival-release prerequisites, not blockers to this paper-side revision

- In `rulespec-us` / the Axiom side, add a fail-closed five-line guard and
  negative off-slice tests. Until then, any application must prefilter to the
  true five-line intersection and commit its row, weight, and value receipt.
- In `axiom-oracles`, regenerate the public disposition mirror from the
  authoritative YAML and add the source/mirror synchronization tripwire.
- Archive the hash-pinned P2 parquet, assumptions register, and validation
  receipt in the release package.
- Archive exact review prompts, model versions/settings, adjudications, and
  prospective stop/restart rules; retain the planned containerized rebuild and
  persistent identifier.

## Revision table

| Finding | Commit(s) | Verification receipt |
|---|---|---|
| F1 — row count attached to wrong grain | `ac0d8e8`; receipt `3ef90ab` | Pinned build report replay: detail 38,841,305; margins 3,070,851; Table 2 and prose grep clean. |
| F2 — authoritative source versus stale public mirror | `b6592f1`, `a9124ab`, `29c0dd0`, `45d1840`; receipt `3ef90ab` | Authoritative 30 / 15,200 / MFN 594 versus mirror 46 / MFN 462; exact full ref, quarantine note, regeneration prerequisite, and tripwire present. |
| M1 — no fail-closed five-line gate | `dce1883`, `ac0d8e8`, `a9124ab`, `29c0dd0` | Pinned composition and generator replay; all composition claims state caller filtering/no guard; pilot is spatially unrestricted; no composed pilot result survives. |
| M2 — duty/revenue overclaim | `dce1883`, `a9124ab` | Living-source and PDF greps find bounded posted-ad-valorem language and all four missing input/state classes; affirmative stale phrases absent. |
| M3 — operational semantics and Data Records | `dce1883`, `ac0d8e8` | Engine/source replay; semantics table, record/file table, 14 fields, keys, weights, zero/null behavior, and supported operations present. |
| Minor 1 — five-line disclosure at every use | `dce1883`, `ac0d8e8`, `a9124ab` | §2, §5, and §7 state the true temporal/spatial/caller scopes. |
| Minor 2 — §201 implementation wording | `dce1883`, `b6592f1` | One operative explicit-zero version; historical stages attributed only to proof atoms. |
| Minor 3 — trace discontinuity | `dce1883` | Canada/February 24 is labeled a separate boundary probe from Malaysia/February 22. |
| Minor 4 — witness design | `dce1883` | Abstract and contribution section say five lines jointly witness all in-scope authorities. |
| Minor 5 — overloaded coverage term | `b6592f1` | Ten policy records with `covered: true` are explicitly distinguished from 20,400 covered interval-cells. |
| Minor 6 — missing disposition complement | `b6592f1` | Exact partition `15,200 = 8,283 + 6,917`, including entry counts, appears in prose and Table 1. |
| Minor 7 — review reproducibility | `a9124ab`, `29c0dd0` | Review counts/verdicts are retrospective provenance; missing protocol is a named release prerequisite. |
| Style and contribution hierarchy | `dce1883`, `a9124ab`, `45d1840` | Conformance is primary, data is enabling, inventory is moved out of the abstract, review trajectory is not evidence, and local outputs are not called published. |
| Claim ledger, PDF, and final audits | `3ef90ab`, `d2ab108`, `45d1840` | Full quote ledger; immutable artifact replay; 24-page PDF hash; clean source/PDF greps; 11/11 draft mirrors; two independent final audits pass. |

VERDICT: REVISION COMPLETE
