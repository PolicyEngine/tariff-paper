# Ground truth — pinned facts for the tariff paper

Every number a draft uses comes from here. Source classes: **[read]** =
artifact read or produced in the 2026-08-07 session (file/commit named);
**[posted]** = published today by this campaign (URL named); **[recall]**
= campaign memory — carries `[NEEDS VERIFICATION]` until the research
lane confirms against the primary artifact.

## The conformance result (Axiom leg)

- us-tariff-yale **conformant TRUE on main**, closed 2026-08-03: 10/10
  policies covered (100%), unexplained 0, axiom_attributed_open 0,
  invalid_exclusions [], 4 tripwired exclusions, oracle_attributed 8,283
  classified, temporal debt 48,000 pre-domain + 1,200 straddle-clipped
  intervals surfaced non-blocking. Snapshot pin: axiom-oracles #452 @
  `dc1da3af`. [read: _tariff-parity/CAMPAIGN.md close block]
- Conformance predicate: `covered == in_scope && unexplained == 0 &&
  axiom_attributed_open == 0`, universe generated from the oracle's own
  spine. [read: project_axiom_certification_stack.md]
- Scope: Yale's `statutory_rate_*` columns — MFN base via HTS columns,
  §232 family, §301 family (incl. Brazil + forced-labor + CS), IEEPA
  reciprocal/fentanyl incl. termination, §122, §201, §338 — plus
  total_additional/total_rate reconciliation, at their default
  legal-date mode. Out of scope (estimation layer): metal_share, USMCA
  utilization, MFN exemption shares, effective constructs.
  [read: CAMPAIGN.md]
- Reference vintage: Yale tariff-rate-tracker commit `c4307e51`; their
  full R build measured locally: 6368.27 s real (1 h 46 m), peak memory
  footprint 132,526,069,168 bytes (123.4 GiB), maximum RSS
  89,850,789,888 bytes (83.7 GiB). [read:
  ~/TheAxiomFoundation/_tariff-yale/build-timing.log; two failed
  attempts preserved as .locale-fail and .stale-gate variants]. Panel
  ~1.9 GB rate_timeseries.rds `[NEEDS VERIFICATION: exact size]`.
- Corpus grounding: 138 signed corpus versions ingested for the
  campaign (47 FR instruments + 44 HTS revision snapshots + 47 chapter-99
  /US-note extractions). [read: CAMPAIGN.md cycle-3 block]
- Adversarial arc on the harness: sol rounds r2→r7 to APPROVE; battery
  2,396 passing at close; final sweep 0 predicate disagreements across
  220 committed dashboard reports. [read: CAMPAIGN.md]

## Encoding mechanics (verified against code 2026-08-07)

- Rules carry `versions:` lists with `effective_from`; changes append
  dated versions, never edits. No `effective_until` in the overlays;
  supersession by later versions or explicit termination rules.
  [read: rulespec-us us/policies/usitc/us-tariff-duty/overlays/*]
- Terminations are encoded law: `overlays/ieepa/termination.yaml`
  encodes EO 14389 — `terminated_ieepa_additional_ad_valorem_duty_rate
  = 0` effective 2026-02-20, proof atom excerpt "shall no longer be in
  effect", corpus citation `us/rulemaking/federal-register/2026-02-25/
  2026-03832`. Companion test evaluates the one-day period ON
  2026-02-20. [read: termination.yaml + termination.test.yaml]
- Every version carries proof atoms citing corpus paths
  (`us/statute/hts/9903.01.25`-style) with verbatim excerpts.
  [read: reciprocal-baseline-9903-01-25.yaml]
- HTS revision consolidations are their own dated modules
  (e.g. section-232-aluminum/rev12-consolidation.yaml). [read: ls of
  overlays/section-232-aluminum/]
- Composed spine: `us:policies/cbp/us-tariff-duty/composition`, imports
  line modules + per-authority overlays (IEEPA fentanyl ×4, reciprocal
  per-country modules, §122, §232-aluminum incl. RU 200%, §301 families).
  [read: composition.yaml imports block]

## Legal timeline (the "why 2026" hook)

- IEEPA additional duties: legal end 2026-02-20 (EO 14389), collection
  end 2026-02-24 (EO 14388) `[NEEDS VERIFICATION: EO 14388 doc]`;
  SCOTUS Learning Resources v. Trump decided `[NEEDS VERIFICATION:
  decision date + citation]`. EO 14389 leg is [read] via the encoding's
  FR citation; the rest is [recall].
- §122 balance-of-payments surcharge expired 2026-07-24
  `[NEEDS VERIFICATION]`. [recall]
- Forced-labor §301 finalization: FR doc 2026-15181, 60 determinations,
  HTS note 52 `[NEEDS VERIFICATION]`. [recall]
- HTS 2026 revisions reached Rev 15 (UK pharma §232 zeroed)
  `[NEEDS VERIFICATION: USITC revision page]`. [recall]

## Yale tracker defects (reported upstream, unacknowledged)

All six filings verified open with 0 maintainer comments as of
2026-08-07 [read: gh api this session]:
- #23 + PR #24 — non-UTF-8 locale corruption + fix.
- #25 — measured build envelope vs documented 32 GB guidance.
- #26 — proposal: publish the line-level panel as a release artifact.
- #27 — §201 solar flat 14.5% carried past Proclamation 10339's staged
  table end (2026-02-06). Independent derivation recorded in
  axiom-oracles `conformance/detail/us-tariff-yale.json` (Proclamation
  10339 referenced; snapshot report
  `reports/axiom-yale-us-tariff-panel-all-2026-08-03.json`). [read:
  oracles main @ 7085600b greps]
- #28 — no GN3(b)/column-2 branch: CU/KP/BY/RU carry column-1 base
  rates. Column-2 disposition recorded in the same detail file (×2
  mentions). Statutory derivation: HTSUS General Note 3(b) current
  text `[NEEDS VERIFICATION: quote the note]`.

## The entries dataset (Microcosm leg) — microcosm #620 + #621, MERGED 2026-08-07

- P1 merged: squash `d4b0855157af996bd367146bc200a2f72ee7d15d`, sol
  rounds r1–r12 ending APPROVE-no-findings; P2 merged: squash
  `6707ed5912d33ff0a340474a1a24f31546c6dec5`, sol r4 APPROVE.
  [read: gh merges executed this session]
- Source: Census monthly bulk U.S. Imports of Merchandise (IMDB) ZIPs,
  `census.gov/trade/downloads/{YEAR}/Merch/im_m/IMDB{YY}{MM}.ZIP`,
  18 archives 2025-01→2026-06, ~3.3 GB, every byte sha-manifested;
  18 GETs replace thousands of 500-prone API calls. [posted: PR #620 body]
- Ingest: 38,841,305 detail rows → 3,070,851 margin cells (HTS-10 ×
  country × district × month), 302,318 consumer facts; reconciled
  exact-integer against the publisher's own in-archive control totals on
  three axes (22 commodity / 18 country / 18 district measures):
  **0 failures in all 18 months**. [read: r3 review prompt / build report,
  committed in-branch docs/evidence/us-import-entry-margins/]
- Cross-check over the second official channel (Census International
  Trade API): 108,977 cells exact on all four dollar measures, 16 pairs,
  0 mismatches, 0 gating failures. [read: crosscheck report; posted:
  #615 comment]
- Generator: every (HTS-10 × country × month) customs-value cell
  reproduced to the integer dollar on an enforced domain (values ≤ 2⁵³);
  pilot window 2026-02→2026-06: 3,806,050 entry rows → 44,881,145
  weighted entries, weighted customs value $1,467,109,590,515 — equal to
  the window's margins total exactly. [posted: #615 comment]
- Assumptions register (shipped beside the data): entry counts from
  CBP FYTD FY2026 mean entry value (coverage 2025-10-01→2026-07-27,
  labeled); lognormal within-cell sizes, σ = 2.6916 solved so the
  ≤$2,500 share matches CBP's informal-entry share as a **proxy moment**
  (19 CFR 143.21 mapping gap registered); share Δ 2.6×10⁻⁵; achieved
  mean $32,689 vs anchor $32,916; `is_postal_shipment = False`,
  entry_date = 15th, shipment_value = customs_value — all with
  sensitivity notes. [posted: #615 comment]
- Review arc: 12 adversarial rounds on P1 (publication machinery alone
  took 8), 4 on P2; trade battery 91 → 149 tests; final verdicts
  APPROVE with no findings. [read: this session's review files]
- Fiscal-year honesty machinery: FYTD-labeled record sets with as-of
  endpoints; fail-closed parsing (HTML entities, impossible dates,
  displaced notes, future endpoints all raise). [read: PR #620 body +
  code edited this session]

## Prohibitions (never appear in any draft)

- "Nonprofit" as Axiom's descriptor; the org is "The Axiom Foundation."
- Thesis (the org concept) — never in public artifacts.
- "Certified"/"certification" for the internal sol review — it is
  independent adversarial cross-model review; external certification
  (notary pattern) is future work.
- "Confirmed by Yale" or any maintainer-acceptance implication for
  #27/#28 — they are reported, derivation-backed, unacknowledged.
- Lowercase product names in prose (Microcosm, PolicyEngine, Chronicle,
  RuleSpec); "populace"/"ledger" only as code identifiers.
- Policy advocacy in any direction.
- Unpinned scoreboard numbers (every scoreboard claim carries its
  snapshot SHA).
