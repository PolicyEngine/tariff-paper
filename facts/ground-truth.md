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
- Policy-record conformance predicate: the count of in-scope policy records
  with `covered: true` equals the count of in-scope policy records, and
  `unexplained == 0 && axiom_attributed_open == 0`; this `covered` field is not
  the 20,400 covered-interval-cell term used by the tariff report. The universe
  is generated from the oracle's own spine. [read:
  project_axiom_certification_stack.md]
- Scope (CORRECTED per the dc1da3af detail file): 10 covered policy
  constructs — MFN column rate, §232 (aluminum in the composition),
  §301 China + Brazil + forced-labor, IEEPA (fentanyl+reciprocal as
  one combined slot), §122, §201, §338, total — at the reference's
  default legal-date mode; 4 excluded:technical with tripwires (other,
  rate_301_cs, stacking_outputs, swiss_framework). Estimation layer
  (metal_share, USMCA utilization, exemption shares, effective
  constructs) out of scope entirely. [read: detail file @ dc1da3af]
- Reference vintage: Yale tariff-rate-tracker commit `c4307e51`; their
  full R build measured locally: 6368.27 s real (1 h 46 m), peak memory
  footprint 132,526,069,168 bytes (123.4 GiB), maximum RSS
  89,850,789,888 bytes (83.7 GiB). [read:
  ~/TheAxiomFoundation/_tariff-yale/build-timing.log; two failed
  attempts preserved as .locale-fail and .stale-gate variants]. Panel
  rate_timeseries.rds = 1,929,830,536 bytes (1.93 GB). [read: local file]
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
- **No five-line domain guard at `dbf09f44`.** The composition defines five
  exact-line predicates but never requires their disjunction. For an unsupported
  line, `mfn_ad_valorem_rate` falls through to `else: 0`; during
  2026-02-24 through 2026-07-23, `section_122_component_rate` falls through to
  the blanket 10 percent rate; the total adds these components. Off-slice calls
  can therefore return plausible rates rather than errors. All paper inference
  is caller-restricted to the five lines; a fail-closed guard and negative tests
  are an Axiom-side archival prerequisite. [read: composition.yaml lines
  691–799, 2214–2282, 2945–2996, 3804–3821 @ `dbf09f44`]
- Engine operational semantics at `ffd82132`: version bounds are inclusive and
  selected at the query period's start; the applicable version with greatest
  `effective_from` wins, gaps error, and same-start overlap precedence is not a
  legal semantic to rely on. Formula branch order carries precedence; stacking
  is explicit component addition; declared scalar/judgment types and missing
  inputs/versions produce runtime errors. The composed output is a `Rate`, not a
  duty amount. [read: engine docs/rulespec.md, src/model.rs, src/engine.rs]

## Legal timeline (the "why 2026" hook) — ALL [verified 2026-08-07, research/verification-report.md]

- IEEPA: Learning Resources, Inc. v. Trump, 607 U.S. 229 (2026),
  No. 24-1287 (with No. 25-250), decided 2026-02-20; holding (syllabus,
  verbatim): "IEEPA does not authorize the President to impose
  tariffs." EO 14389 ("Ending Certain Tariff Actions", 91 FR 9437,
  doc 2026-03832) signed the SAME DAY: duties "shall no longer be in
  effect and, as soon as practicable, shall no longer be collected" —
  NO date in the order's text for collection. The 2026-02-24 00:00 ET
  collection cutoff was set operationally by CBP CSMS # 67834313
  (issued 2026-02-22). EO 14388 = the de minimis CONTINUATION order
  (91 FR 9433), NOT the collection end — never cite it for that.
- §122: Proclamation 11012 (91 FR 9339), 10% surcharge on all imports
  (annex exceptions; not stacked on §232), effective 2026-02-24
  00:01 EST through 2026-07-24 00:01 EDT — exactly the 150-day
  statutory maximum of 19 U.S.C. § 2132(a) (which caps at 15%). Ran to
  scheduled expiry (no modifying FR instrument through 2026-08-07).
- Forced-labor §301: 91 FR 47318 (doc 2026-15181, USTR, pub.
  2026-07-28): 60 investigations determined actionable; rates 10%
  (prohibition/agreement economies) / 12.5% (others); TRQs for four;
  Annex I inserts chapter-99 U.S. note 52 (headings 9903.05.85–
  9903.06.21); effective 2026-07-24 — THE SAME DAY the §122 surcharge
  expired (verified seam).
- HTS 2026: Revision 15 dated 2026-08-03 (Rev 14 was 2026-07-31).
  Rev 15's sole change: heading 9903.04.63 (UK PATENTED pharmaceutical
  articles) +10% → +0% per 91 FR 49406 implementing Proclamation 11020;
  context rates: 9903.04.60 general pharma 100%, 9903.04.62
  EU/JP/KR/CH/LI 15%.
- §201 solar: Proclamation 10339 (87 FR 7357) Annex I staged table
  verbatim: 14.75% / 14.5% / 14.25% / 14% for the four years ending
  2026-02-06; current HTS marks note 18 EXPIRED. Yale's flat 14.5% past
  the end is therefore wrong on two axes (stale stage since 2024-02-07;
  nonzero past expiry). Later Procs 10779/10790 changed TRQ/coverage,
  not the terminal date.
- GN 3(b) verbatim (HTS 2026 Rev 15): column-2 rates apply to products
  "of the following countries and areas": Republic of Belarus, Cuba,
  North Korea, Russian Federation (footnote cross-references note 30 /
  9903.90.08 additional duties).
- Yale tracker: MIT license, org Budget-Lab-Yale, commit c4307e51
  reachable upstream (2026-07-24, ancestor of master); companion Budget
  Lab post "Introducing the Tariff Rate Tracker" (2026-04-01).

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
  mentions). Statutory derivation verified: GN 3(b) verbatim above.

## The entries dataset (Microcosm leg) — microcosm #620 + #621, MERGED 2026-08-07

- P1 merged: squash `d4b0855157af996bd367146bc200a2f72ee7d15d`, sol
  rounds r1–r12 ending APPROVE-no-findings; P2 merged: squash
  `6707ed5912d33ff0a340474a1a24f31546c6dec5`, sol r4 APPROVE.
  [read: gh merges executed this session]
- Source: Census monthly bulk U.S. Imports of Merchandise (IMDB) ZIPs,
  `census.gov/trade/downloads/{YEAR}/Merch/im_m/IMDB{YY}{MM}.ZIP`,
  18 archives 2025-01→2026-06, ~3.3 GB, every byte sha-manifested;
  18 GETs replace thousands of 500-prone API calls. [posted: PR #620 body]
- Ingest: 38,841,305 detail rows at HTS-10 × country × subcode ×
  entry district × unlading district × rate provision × month → 3,070,851
  district-aggregated margin cells at HTS-10 × country × month, plus 302,318
  consumer facts; reconciled
  exact-integer against the publisher's own in-archive control totals on
  three axes (22 commodity / 18 country / 18 district measures):
  **0 failures in all 18 months**. [read: r3 review prompt / build report,
  committed in-branch docs/evidence/us-import-entry-margins/]
- Cross-check over the second official channel (Census International
  Trade API): 108,977 cells exact on all four dollar measures, 16 pairs,
  0 mismatches, 0 gating failures. [read: crosscheck report; posted:
  #615 comment]
- Generator: every positive (HTS-10 × country × month) customs-value cell
  reproduced to the integer dollar on an enforced domain (values ≤ 2⁵³);
  spatially unrestricted pilot window 2026-02→2026-06: 3,806,050 entry rows → 44,881,145
  weighted entries, weighted customs value $1,467,109,590,515 — equal to
  the all-line window's margins total exactly. The generator filters only by
  month and positive customs value, not by the five witness lines; no composed
  rate result over these rows is reported. [posted: #615 comment; read:
  build_us_import_entries.py lines 111–153 @ `6707ed59`]
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
- The exact component-review prompts, model settings, adjudication rules, and
  prospective stopping protocol are not preserved in this repo. Treat the
  round counts and verdicts as retrospective development provenance; the
  mutation tests, committed reproductions, and pinned outputs carry the
  evidentiary weight. Protocol publication is an archival prerequisite.
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
  RuleSpec); old names only as code identifiers.
- Policy advocacy in any direction.
- Unpinned scoreboard numbers (every scoreboard claim carries its
  snapshot SHA).

## Conformance waterfall + pins (extracted from the dc1da3af artifacts, 2026-08-07)

- Universe (per policy, from the -all report): 240 countries; 68,400
  in-scope intervals = 20,400 covered + 48,000 temporal debt;
  comparisons 39,600; raw matches 24,400 (61.6%); raw mismatches
  15,200; error_count 0. Reference panel rows total: 277,303,920.
- Per-policy conformance record (detail file): explained_rate 100,
  unexplained 0, axiom_attributed_open 0, oracle_attributed 8,283
  (cells); dispositions operate per concept-slot (per-concept mismatch
  counts overlap across slots: mfn 594, ieepa 476, s122 4,560, s232
  1,920, s201 7,887; row-level total 15,200).
- Authoritative dispositions at
  `axiom-oracles@dc1da3af067c50fa7138458faf3703b4b9efd7cb:dispositions/us-tariff-panel.yaml`
  are dated 2026-08-03 and partition 15,200 units into 30 entries:
  8,283 `upstream_engine_gap` units (10 entries) plus 6,917
  `explained_residual` units (20 entries). Their MFN footprint is 594 = 528
  column-2 + 66 preference units. The public mirror at the same pin,
  `dashboard/public/data/dispositions/us-tariff-panel.json`, is stale: dated
  2026-08-02, 46 entries, with a 462 MFN footprint (396 + 66). It must be
  regenerated under a synchronization tripwire before archival release.
- 14 policy records: 10 conformant, 4 excluded:technical, IDs:
  us-tariff-yale:{other, rate_301_cs, stacking_outputs,
  swiss_framework}.
- IEEPA note (verbatim from the detail record): fentanyl compared
  jointly with reciprocal via the suite's combined ieepa slot (the
  composition encodes one IEEPA component).
- Full pins: rulespec-us dbf09f44eddd00b7ad5520f89371ebe8fdf0b7df;
  axiom-rules-engine ffd8213271947b0189a9dd61a055c1e0e78908a0 (v0.1.0,
  binary sha256 674ca6e70afdccb59c3d6847933bc24b4590105e49db54790f2dcd0bdbbe32d7);
  axiom-oracles dc1da3af067c50fa7138458faf3703b4b9efd7cb; Yale
  c4307e514196618afcbf88cf7fd33746417eeabf; microcosm merges
  d4b0855157af996bd367146bc200a2f72ee7d15d /
  6707ed5912d33ff0a340474a1a24f31546c6dec5.

## Witness-slice disclosure + section 201 mechanism (round-3 verifications, 2026-08-07)

- **The reconciliation universe is a five-line witness slice** (verified
  in the pinned report's scope.covered_lines): 2203.00.0030 (beer),
  7202.11.1000 (ferromanganese), 7601.10.3000 (unwrought aluminum),
  8541.42.0010 (crystalline-silicon solar cells), 9506.62.4040
  (inflatable balls) × 240 partners × 57 intervals = 68,400. Lines were
  chosen as authority witnesses; full-schedule expansion is the
  recorded backlog (campaign T1). ~0.025% of the reference's
  277,303,920-row spine. EVERY reconciliation claim must carry this.
- **Section 201 encoding mechanism at dbf09f44** (composition.yaml
  section_201_component_rate): ONE version, effective_from 2026-02-15,
  formula an explicit zero — with proof atoms quoting the ENTIRE staged
  table (14.75/14.5/14.25/14%, each period's dates) and the schedule's
  expiry compiler's note. Zero by explicit version with the derivation
  in the proof, NOT by absence of a version. The encoded domain begins
  2026-02-15 (post-expiry) temporally; this does not create a spatial guard.
- Temporal debt semantics per artifact: 48,000 pre-domain intervals =
  debt; boundary-straddling intervals are clipped to the covered
  portion (straddle/clip fields present in the report; 1,200 clip
  events recorded).
- Generator algorithm (entry_generator.py @ microcosm main): integer
  largest-remainder allocation; each (line, country, month) stratum
  yields at most two weighted rows; all dollar allocation in integer
  arithmetic; proven-exact domain bound documented in-module.
- **Rate-versus-amount boundary:** the composition supports posted ad valorem
  component-rate stacks under the input date supplied. It does not compute the
  beer column-2 specific duty of 13.2 cents per liter, the beer Section 232
  amount on declared aluminum-content value, quota position, or sub-monthly
  timing. The synthetic entries supply none of the specific-duty quantity,
  aluminum-content value, or quota state and date every allocation on the
  fifteenth. [read: composition.yaml lines 2214–2282 and 3073–3181 @
  `dbf09f44`; entry_generator.py lines 325–408 @ `6707ed59`]
- Review-coverage truth for §6: the three NAMED reviewed arcs are the
  comparison harness (6 rounds to APPROVE), entries P1 (12 rounds) and
  P2 (4 rounds); encoding waves carried lane-level review but NOT every
  rulespec-us PR (counterexamples exist) — never claim "every PR."
- Manuscript QA truth: one cross-model hostile round (GPT-5.6-class)
  addressed in revision 1; round-diff + red-team verification rounds =
  same-family (Claude-class); a second cross-model round pending codex
  quota (locks lift Aug 10–13).

## Post-draft repo state note (2026-08-08)

microcosm#638 (namespace rename) squash-merged 2026-08-08 20:23Z:
`populace.*` imports are now `microcosm.*` on main; `populace_us_trade.*`
fact keys byte-frozen as designed. The paper's pinned merge commits and
in-branch evidence paths are historical records and stay correct as
written; any NEW code (P3/P4, the archival replication release) imports
`microcosm.*` and cuts worktrees from renamed main.

## Tracker-vs-tracker decomposition (2026-08-09 runs; VERIFIED)

- Window: April–June 2026 daily means. Yale Budget Lab published
  weighted effective statutory rate 11.08%; TPC all-goods series 9.46%
  (Datawrapper aO4iG v44; raw values are PERCENT, divided by 100 in our
  adapter). Gap ≈ 1.6pp.
- Method: Yale's own daily-series stage and own built rate panel (their
  repo @ `c4307e51`, built locally), run twice, identical except the
  import-weights file supplied via their `config/local_paths.yaml`
  `import_weights:` hook. Weight bases built with THEIR
  `src/io/build_import_weights.R --no-gtap` over sha-manifested Census
  IMDB monthly archives: 2024 base $3,119.3B (their published
  denominator ≈ $3,123.8B), 2025 base $3,242.5B (347,709 hs10×country
  rows).
- Result: 2024 weights → 10.72%; 2025 weights → 9.38%. Weight-vintage
  effect −1.34pp; residual vs TPC's 9.46% = 0.08pp. The remaining
  construct differences (AD/CVD scope and effective-layer treatment)
  wash in this window.
- Validation leg: the 2024-weight rerun reproduces Yale's published
  series within 0.2–0.6pp in stable months. Departures traced: (a)
  their 2026-06-09 publication vintage predates their Brazil §301/§338
  encodings (our panel = full `c4307e51`); (b) our single-pass weight
  build vs their per-revision 484(f) re-keying in shock months.
- Artifacts: both leg outputs + the derivation annotation committed in
  PolicyEngine/policyengine-scorecard under `data/pe/diagnostics/`
  (daily_overall_weights2024.csv, daily_overall_weights2025.csv);
  weight bases + logs in the P5 lane (`_tariff-p5/stage1/`).
- Status: author-attributed. Both maintainers notified 2026-08-12
  (Ricco/Yale, Wong/TPC — verified sent); no responses at revision
  time. NEVER present as maintainer-confirmed until a reply lands.
- Referee-recomputed from the committed leg CSVs (2026-08-13): under
  unweighted means over the 91 calendar days 2026-04-01..06-30, legs
  reproduce exactly (10.7201 / 9.3757; difference 1.3444; residual
  0.0843); bridge closes 11.08 − 0.36 − 1.34 + 0.08 = 9.46. Leg-vs-leg
  gap by revision segment: 1.38 / 1.35 / 1.35 / 1.32. Join coverage:
  2024 base matches 94.74% of base value ($2,955.34B of $3,119.32B),
  2025 base 96.43% ($3,126.72B of $3,242.52B) — the −1.34 bundles
  basket composition with this small coverage differential,
  undecomposed. Validation leg sits 0.36 BELOW the published series on
  the window mean (the two identified causes act in OPPOSITE
  directions; not separately quantified). Panel-side columns
  byte-identical between the leg CSVs.
- Yale's fixed-2024 basket is documented and motivated in their weights
  doc (pre-shock Laspeyres; 484(f) re-keying machinery); TPC's notes
  disclose 2025 volumes ex-AD/CVD without stating a rationale. Neither
  org publishes a weight-vintage reconciliation; ours appears to be the
  first quantification (verified only as: none found in their repos,
  docs, or published series as of 2026-08-09).

## Full-schedule generated rate spine (landed 2026-08-10..13; VERIFIED)

- Corpus feedstock: version
  `2026-08-09-usitc-hts-2026-rev15-full-schedule` (axiom-corpus PR
  #595, merge-commit): all 29,845 HTS-numbered rows of the pinned
  Revision 15 snapshot (sha `59a76c12…`) as per-line provisions +
  document root; provision bodies byte-identical to the witness-chapter
  version for all 1,706 overlapping citation paths (reproducer-gated).
  Sol adversarial review, 3 rounds to APPROVE.
- The live USITC API cannot serve vintages: `reststop/exportList`
  accepts and silently ignores `release=` (proven: heading 9903.02.01,
  born April 2025, returned for "2025HTSRev1"). Frozen vintages exist
  ONLY as corpus snapshots.
- Spine: 13,790 rated lines across 98 chapters, emitted as 100
  generated rulespec modules (chapter 99 as three sub-shards: 9901 +
  9902 first half / 9902 second half / 9903–9999). Per-line general and
  column-2 rate tables (ad valorem + Free; Free = 0) and total-partition
  disposition tables: ad_valorem 6,247 / free 5,795 / specific 777 /
  conditional 548 / compound 326 / component 93 / empty 4 (column-2-only
  records). Non-ad-valorem lines carry explicit markers, never silent
  zeros.
- Grounding: per-cell proof atoms citing `us/statute/hts/<htsno>` with
  verbatim body-line excerpts (48,479 atoms; full-batch proof validation
  196/196 under the pinned toolchain; full validate battery (compile +
  companion tests + grounding) 98/98 locally before landing.
- Gates: witness identity (generated cells reproduce the 3 hand-built
  witness modules' encoded rates exactly; expectations parsed from
  those YAMLs, never memory); double-emit determinism; window
  stability (0 general-column diffs on 11,504 common base lines,
  2025-basic ↔ 2026-rev15; the single column-2 diff is USITC's own
  source-text repair on 2909.19.18.00, caught as `conditional` by the
  partition, not force-parsed).
- Membership: 19,948/19,949 ten-digit statistical lines map to their
  rate-bearing ancestor (1 unowned: 9802.00.91.00, ch-98 special
  regime). The hts10→rate-line map ships as a generated DATA artifact
  (spine.json), deliberately NOT as a statutory parameter table — its
  synthetic integer keys are not groundable in provision text.
- Applied per-entry duty is a declared deferred output on every module
  (composition-layer work); the five-line witness composition is
  UNCHANGED in this revision — the spine publishes statutory rate
  TABLES at full schedule, not full-schedule duty computation.
- Landed as rulespec-us PRs #1267 (ch 01–25), #1275 (26–50), #1276
  (51–75), #1280 (76–89), #1284 (90–98), #1286/#1287/#1288 (chapter 99
  sub-shards a/b/c; #1288 MERGED 2026-08-13, spine-completing merge
  `f062088fb` — all 13,790 lines on main, reproducer --check green
  over the complete 200-file set). Each PR: subset manifests via
  `sign-applied-files --manual-exception rulespec-us#1190`
  (deterministic-generator provenance class), append-only
  oracle-coverage ledger entries, regenerated reverse index.
- CI-scale facts for §7-class claims: the us-shard validate leg under
  the production (unindexed) resolver costs roughly 6–10 s per cited
  path; single PRs exceeding ~3,000 cited lines hit GitHub's 6-hour
  job cap (observed thrice). A resolver memoization (60+ min →
  27.5 s per module locally; sol-reviewed to APPROVE over 3 rounds) is
  structurally unpinnable until the repo's strict toolchain cutover
  (encode pins must live on encode main; encode main requires bound
  releases the repo cannot yet bind).
