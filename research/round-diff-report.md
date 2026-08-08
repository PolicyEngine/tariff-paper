# Round-diff review — verifying the hostile-pass round-1 fixes

Date: 2026-08-07. Reviewer: round-diff lane (revision-integrity audit).
Inputs: `paper.md` @ e4215c3 ("Hostile-pass revision round 1: all 20
findings addressed"), `research/hostile-pass-report.md` (20 findings,
NEEDS-MAJOR-WORK), `facts/ground-truth.md` (incl. new "Conformance
waterfall + pins" section), `research/references.bib`.

Beyond the briefed inputs, this audit opened the pinned conformance
artifacts directly — `git show dc1da3af:reports/axiom-yale-us-tariff-panel-all-2026-08-03.json`
and `dc1da3af:conformance/detail/us-tariff-yale.json` in the local
`~/TheAxiomFoundation/axiom-oracles` clone — and re-verified the Yale
build log (`_tariff-yale/build-timing.log`: 11:11:53→12:58:01 = 6,368 s,
peak footprint 132,526,069,168 B = 123.4 GiB) and the workstation RAM
(`hw.memsize` = 137,438,953,472 B = 128 GiB). Every waterfall number the
revision added checks out against the artifact — the revision
**regenerated** its new numbers from the pinned artifacts rather than
relabeling; no relabel-without-regenerate at the data layer. The
narrative layer is another story (see "Fix-applied narrative bugs").

Note: `research/hostile-pass-r2.md` is empty (0 bytes; the r2 lane
crashed — see `hostile-pass-r2.err.log`). This report serves as the
round-2 verification.

## Prior findings audit

| # | Finding (short) | Verdict | Evidence |
|---|---|---|---|
| 1 | No auditable conformance denominator | **PARTLY CLOSED** | Waterfall added (paper.md:311–341) and verified exact against the artifact (68,400 = 20,400 + 48,000; 39,600 → 24,400/15,200; 61.6% raw; 4 exclusions named with tripwire rationale; abstract narrowed to "the tracker's own … spine over its 2025–26 coverage"). BUT the denominator's **line dimension is still undisclosed**: the pinned artifact's `scope.covered_lines` is exactly five HTS-10 lines (2203000030, 7202111000, 7601103000, 8541420010, 9506624040; 68,400 = 5 × 240 × 57). The paper names the partner (240) and date dimensions of "the reconciled slice" (315–316) and never the line count. Also: no exclusions/debt-as-failure sensitivity; Table 1 lacks the comparisons/matches/raw-rate rows (prose-only). |
| 2 | Self-awarded reference-attributed victories | **PARTLY CLOSED** | "Independent" now defined ("derivation … independent of both implementations' code", 380–386); triple label used everywhere incl. abstract ("author-attributed, derivation-backed, and as-yet maintainer-unacknowledged", 29–31; "the honest name … we use throughout", 388–389); raw mismatches reported separately (61.6% at 327). Still missing: an in-paper partition of the 15,200 (and the 8,283 within it) into named disposition classes summing correctly — the artifact HAS named classes (`mfn-fta-preference-layer`, `mfn-column2-reference-gap`, SE floor-minus-base, unencoded-§232-programs, s201 mechanism) but the paper defers wholesale to "committed disposition artifacts" (328–330). Concept-slot counts (594/476/4,560/1,920/7,887) overlap and do not partition. |
| 3 | Development-time reconciliation sold as external validation | **CLOSED** | Retitled and reframed: "That is reconciliation between independent implementations … it is not a held-out evaluation" (286–291); spine-blindness admitted ("an omission from that spine is invisible", 288); iteration-to-zero admitted (289–290); upgrades named (frozen snapshot, double-coded legal sample, third implementation, 292–294); mutation-test scope bounded (363–365). New defect: the upgrade list is attributed to Section 6, which doesn't contain it (see narrative bugs). |
| 4 | Two-endpoint IEEPA model not evidenced | **CLOSED** | The claim was deleted, per the finding's alternative: "this encodes the LEGAL endpoint … The operational wind-down … is an agency bulletin, not a rule version in this encoding; a parallel collection-status series … is future work, and nothing in this paper's data should be read as carrying it" (195–200); worked trace repeats it (268–270); abstract promises only "the IEEPA termination". |
| 5 | Rate function formally insufficient | **CLOSED** | Exact output defined: "for a (tariff line, partner country, calendar date) triple inside the encoded domain, the ex-post statutory rate stack under legal-date semantics" (214–218), with the four undetermined inputs enumerated — intra-day boundaries, quota position, entry-specific facts, knowledge-time (218–229). §1's fourth argument (interpretation) is resolved by fixing the mode explicitly ("this paper's panel computes the legal-date one", 274). Residual (→18): overlay stacking/interaction semantics still not specified. |
| 6 | Excerpts prove provenance, not legal correctness | **PARTLY CLOSED** | "Audit-grade" replaced exactly as requested: "source-traceable rate lookup — every value carrying its instrument citations — within the stated domain" (629–631); citation-integrity vs semantic-validation distinction now made (363–365; 276–277 "internally consistent and wrong"). Not delivered: legal-coding protocol, interaction/precedence table, completeness checklist; the double-coded legal sample is named only as future work (293). And §2:235–236 "the Section 232 metal programs" overstates the compared encoding — the artifact's compared component is `section_232_aluminum_component_rate` only, with unencoded §232 programs surfacing as classified mismatches (detail note) — precisely the completeness risk this finding warned about. |
| 7 | "Exact margins" meaning shifts | **PARTLY CLOSED** | Abstract now separates the two scopes with grain and measure (33–38); §5 states the rule: "Two scopes govern everything in this section and must not blur" (465–469). BUT §8:742–744 still asserts "the generator's contract is exact integer reproduction of **every published margin cell**" — the exact falsehood the finding flagged (published margins are line × country × district × month × 22 measures over 18 months; the generator reproduces customs value at line × country × month, district-aggregated, 5-month pilot). §8 blurs what §5 forbids blurring. |
| 8 | Aggregate identity sold as transaction-level validity | **PARTLY CLOSED** | Renamed throughout to "weighted synthetic entry-line allocations" (36, 462); the mid-month timing warning now cites the paper's own counterexample and prohibits boundary analyses (531–537); within-cell-joint-distribution uses prohibited (646–650); "the dataset … actually needs" deleted. Not delivered: formal weight definition, alternative distributions/timings, downstream sensitivity exhibit. |
| 9 | Self-review boundary honest in §3, not in abstract/rhetoric | **CLOSED** (residual) | Abstract: "same-project cross-model adversarial review run until a pass with no findings" (40–41) — stopping-rule phrasing; §6 discloses model families and the refute-prompt stance with per-finding closure tests (579–585); "marginal cost of rigor collapsed" removed; human adjudication enumerated (602–606); non-certification boundary kept (606–608). Residual: "the trajectory is the evidence" retained (597–598); prompts not published. |
| 10 | Weak negative-search novelty claims | **PARTLY CLOSED** | Three contributions stated plainly (127–143); tracker-firstness hedged ("a web-bounded search … a negative search cannot establish", 706–710); synthetic-firstness hedged and made non-load-bearing (744–748). Retained unhedged: "That culture has not previously reached trade law" (723–724). No comparison table or search appendix (the finding's either/or allows softening — one universal negative still stands). |
| 11 | Advertised period exceeds usable domain | **PARTLY CLOSED** | §7's four-ranges block is exactly the requested statement (650–659), incl. the July-24-seam/August-revision honesty. Abstract discloses the pilot window and the tracker-coverage framing, and mentions temporal debt via the waterfall sentence. Still: the abstract opens "We encode the 2025–26 United States tariff stack" with the composed domain start (artifact: `domain_start` 2026-02-15) stated only in §7 ("February 2026 onward", 656); title unchanged. ~70% of the tracker's in-scope intervals are pre-domain debt (48,000/68,400) — the abstract's first sentence still reads broader than the compared domain. |
| 12 | "Public, pinned, and re-runnable" not delivered | **PARTLY CLOSED** | The `@main` citation is now `termination.yaml@dbf09f44` (171); full 40-char pins for all five repos + engine version + binary sha-256 (776–787), all verified identical to the artifact's provenance block; Yale MIT noted. Archival release / DOI / one-command replication honestly deferred ("accompanies submission; until then the commits above are the replication interface", 785–787). Residual: no commands/environment/data dictionary/own-artifact licenses yet; review-inventory evidence still lives in editable PR descriptions (759–761). |
| 13 | No functioning citations | **PARTLY CLOSED** | Pandoc header + `research/references.bib` (28 entries; every `@`-cited key resolves; References section present); primary instruments now cited at the legal claims in §§1–2. BUT four keys in §8 are missing `@` and will render literally: `[amiti2019impact; amiti2020whos]` (677–678) and `[bown2021uschina; bown_piie_chart]` (682–683) — the exact defect class the finding described — orphaning those four bib entries. Also: the GN 3(b) verbatim quote (417–420) carries no citation (`hts2026rev15` sits unused in the bib), and §4's solar derivation (397–414) repeats the Proclamation 10339 table without re-citing `proc10339_2022`. |
| 14 | Universal claims exceed pinned evidence | **PARTLY CLOSED** | Solar footprint now quantified and softened ("dominated by this class", 410–411, with the 7,887 slot count). "It touches every line for four partners" (423) is retained but now mechanism-backed (the artifact's mfn note confirms the parser "never read[s]" column-2 — the universal follows from the mechanism). Retained on artifact trust: "every escaped cell names its instrument" (446; the paper claims per-cell instrument fields in the disposition artifacts, 328–330 — not independently verified here). New scoped universal: "Every pull request merged in the repositories this paper reports on" (579) — broader than the named review arcs in the fact base. |
| 15 | Validation channels not independent as claimed | **CLOSED** | "A second delivery channel of the same producer — a check that detects parsing and channel errors on either path, not errors common to the source itself" (489–491); control totals labeled internal validity with the 22/18/18 axis coverage and monetary+quantity split (494–498); strata disclosed (16 line-prefix × country pairs, 492–494). |
| 16 | 2^53 exactness claim too broad | **CLOSED** | "Cross-cell aggregations run in arbitrary-precision Python integers … cell values are validated at or below 2^53 so their parquet representation is exactly representable, and the build asserts the reproduction at run time" (504–510) — algorithm, representability phrasing, and runtime assertion, as requested. |
| 17 | Factual/labeling repairs | **PARTLY CLOSED** | "Three days after Revision 14" fixed (88); §1 enumerates "six overlay authorities" (67–69); §4 fixed to "five issues and one patch pull request in all" (430). BUT Data availability still says "our **six upstream reports are public issues** on that repository" (763) — contradicting §4's own correction; §8 says "seven overlapping legal bases" (685) without the six-overlays-plus-schedule gloss; "best available reference" (114) and "most complete" (105) survive with only the benchmark-usage citation as anchor. |
| 18 | Missing formal methods + end-to-end worked example | **PARTLY CLOSED** | Delivered: definitions block (296–309: cell, covered, debt, comparison, match, disposition, tripwired exclusion), semantic mode (legal-date, 214–218 + 304), version-selection semantics (146–153), equality ("a match is exact equality", 305), a worked trace (254–274). Not delivered: stacking/interaction semantics; time-zone/instant beyond the date-grain disclaimer; **generator equations/algorithm and a formal weight definition**; and the trace stops at version selection — it names no final composed rate, touches no Yale cell, no synthetic entry, no computed duty. Two of the new definitions also mismatch the artifact they describe (see New findings 2). |
| 19 | Missing substantive result | **CLOSED** (repositioning) | The finding's own either/or offered "explicit repositioning as a software/data-descriptor paper." The revision took it and executed consistently: "The paper is a methods-and-data contribution; the downstream analyses these enable … are deliberately out of scope" (140–143); §7 draws the boundary with a reason (663–667); title and abstract make no application claims. **This is not a dodge** — it is the sanctioned branch, done thoroughly, and it matches PLAN.md's venue strategy (data descriptor + methods split). The honest caveat: repositioning RAISES the bar on finding 18 — a data paper whose selling point is that panel and entries "compose into duty computation" (622–626, 553–556) should exhibit one composed duty computation, and none exists. The repositioning is legitimate for 19; it must not be stretched to excuse 18's missing generator algorithm and end-to-end demo, which are core content of the repositioned paper. |
| 20 | Missing publication apparatus | **PARTLY CLOSED** | Done: AI-use disclosure (789–795); drafting labels gone; Yale license + full pins; tables exist with source lines. Deferred/open: all four figures (deferral is a stated position and defensible for a working paper — but it is a deferral, not a fix); Tables 1–2 still uncited from body text; authorship placeholder; funding/conflicts absent; own-artifact licenses absent; DOI at submission. |

**Counts: 7 CLOSED, 13 PARTLY CLOSED, 0 OPEN, 0 RENAMED-NOT-FIXED.**

## Relabel-without-regenerate check (CRITICAL section)

At the data layer: **clean**. The new waterfall numbers in
`facts/ground-truth.md` and paper.md §3/Table 1 were re-derived from the
pinned artifacts and verify exactly (comparison_count 39,600; matches
24,400; rate 61.616162; slots 594/476/4,560/1,920/7,887; error_count 0;
countries 240; intervals 68,400/20,400/48,000 + 1,200 straddle-clipped;
provenance pins byte-identical to the paper's Pinned revisions block).
The two upstream-defect dispositions match the artifact's notes
(s201 staged-table mechanism; mfn column-2 "never read" mechanism).

## Fix-applied narrative bugs (claims of closure the body text does not deliver)

1. **Commit e4215c3: "all 20 findings addressed."** Addressed is not
   closed: 13 of 20 are partly closed, several with the flagged text
   surviving verbatim elsewhere in the paper (items 7, 17 below).
2. **r2 brief: "now with live citations."** Four keys are not live
   (paper.md:677–678, 682–683 lack `@`; they will render as literal
   bracket text and their bib entries will not print).
3. **§3:292 "Section 6 states what would upgrade it."** Section 6
   contains no upgrade statement; the list lives only in §3's own
   parenthetical. Mirror bug: §6:607 "external certification; Section 3
   states that boundary" — §3 states the reconciliation-not-held-out
   boundary, not the review-regime boundary. The two sections point at
   each other for content each expects the other to hold.
4. **Partial application of finding 17's fix:** §4:430 corrected to
   "five issues and one patch pull request"; Data availability line 763
   still says "our six upstream reports are public issues" — the fix
   was applied at one site and its contradiction left standing at the
   other.
5. **§5's own rule ("Two scopes … must not blur", 465–469) vs
   §8:742–744**, which blurs them with "exact integer reproduction of
   every published margin cell."

## New findings (independent audit, beyond the prior-round list)

1. **[CRITICAL] The covered reconciliation slice is five tariff lines,
   and neither the paper nor the fact base says so.** The pinned
   artifact (`reports/axiom-yale-us-tariff-panel-all-2026-08-03.json`,
   `scope`) reads: `covered_lines = [2203000030, 7202111000, 7601103000,
   8541420010, 9506624040]`, `countries = 240`, `in_scope_intervals =
   68,400` — exactly 5 × 240 × 57. All headline conformance numbers
   (39,600 compared cells, 10/10 policies conformant, 8,283
   reference-attributed cells) live on a five-line probe panel chosen to
   exercise the authority stack, against a reference panel of ~2,000
   lines (277,303,920 rows). The abstract's "cell-by-cell against the
   leading open reference … on the tracker's own line-by-country-by-date
   spine over its 2025–26 coverage" (21–24) and §3's "the reconciled
   slice covers 240 partners over the tracker's 2025–26 coverage"
   (315–316) name the partner and date dimensions of the slice and stay
   silent on the line dimension. Round 1's false universal ("every
   tariff line … the tracker covers") was deleted — but it was replaced
   by silence rather than by the true number. Any referee who opens the
   pinned artifact will read this as scope misrepresentation. One
   sentence fixes it; the abstract's spine clause must also carry it.
   The new ground-truth waterfall section has the same omission (no
   `covered_lines`, no `domain_start`).
2. **[High] The new §3 definitions contradict the artifact's counting
   semantics.** (a) The paper defines a *cell* as a "(tariff line,
   partner, date-interval, concept) tuple" (296–299), then reports
   39,600 comparisons and 15,200 mismatches that are **row-level**
   counts (artifact: every mismatch is `kind: total_difference` on the
   composed total, with per-authority slots nested inside the row), and
   §3's own census paragraph says "one cell mismatches several
   concepts … the 15,200 distinct rows" (330–332) — impossible under
   its own definition, in which a cell has exactly one concept. (b) The
   debt definition says intervals that straddle the domain boundary are
   "surfaced, never compared" (300–303), but the artifact clips
   straddling intervals — the covered part IS compared, and the 1,200
   clipped remainders are surfaced (`straddle_clipped_intervals`);
   arithmetic agrees (68,400 = 20,400 + 48,000 leaves the 1,200 outside
   the two-way split, and Table 1's "domain-straddling" row is never
   explained in prose). Define the comparison row = (line, partner,
   probe interval) evaluated on the composed total with per-authority
   slots recorded, and describe clipping.
3. **[Medium] "Per policy, 68,400 in-scope date-intervals …" (317) is
   wrong or misleading.** The scope block is suite-level; the detail
   file repeats the identical suite totals (comparisons 39,600, matches
   24,400, oracle_attributed 8,283) in each of the 10 conformant policy
   records. "Per policy" invites the reading that each of the 10
   policies contributes 68,400 intervals (a 10× denominator error).
4. **[Medium] §2:235–236 "the Section 232 metal programs" overstates
   the compared encoding.** The artifact compares
   `section_232_aluminum_component_rate` only, and its note says
   "Yale's rate_232 column spans all §232 actions, so §232 programs
   without an encoded counterpart surface as classified mismatches."
   The paper never says the compared §232 component is aluminum-only,
   and its zero-open-against-encoding claim partly rests on
   classifying unencoded programs as dispositions. State the encoded
   §232 footprint. (The 1,920 s232 mismatches are this class, e.g.
   beer line 2203000030 carrying Yale 0.5 vs axiom 0.0.)
5. **[Medium] Fact-base regressions in `facts/ground-truth.md`.** The
   pre-existing scope bullet claims the §301 family "incl. … CS" and
   "plus total_additional/total_rate reconciliation" — the pinned
   artifact **excludes** `rate_301_cs` (empty driving list at c4307e51)
   and `stacking_outputs` (which is exactly total_additional/total_rate
   plus the effective-layer columns) by tripwire. The paper got this
   right (335–341); the fact base now contradicts both the paper and
   the artifact. Fix the fact base before the next draft inherits it.
6. **[Low] Four bib entries orphaned by the bare keys** (amiti2019impact,
   amiti2020whos, bown2021uschina, bown_piie_chart — all present and
   well-formed in references.bib, all uncitable as written). Also
   unused: `hts2026rev15` (should back the GN 3(b) quote at 417 and the
   Rev 15 discussion), `proc11020_2026`, `eo14388_2026` (the last is
   deliberately held per the fact-base warning — fine).
7. **[Low] Verified rather than flagged:** "on a 128 GiB workstation"
   (370) checks out (hw.memsize = 137,438,953,472); 6,368 s and
   123.4 GiB match the build log exactly; the §338 detail note
   (Canadian beer 50% eff. 2026-08-19, Proc. 11046) confirms the
   encoding carries future-effective published instruments,
   consistent with §2's ex-post semantics.

## Overcorrection check

None found that understate verified results. The 61.6% raw rate is
reported beside the zero-unexplained figure with the correct meaning
attached to each (346–352); conformant-TRUE is preserved as "the
conformance predicate … holds on the covered slice" (344–346); the
channel-independence and internal-validity relabelings match what the
checks actually are. The revision's honesty edits are calibrated, not
excessive.

## Unresolved prior-round residue (concise)

Findings 1 (line-dimension disclosure + sensitivity), 2 (in-paper
disposition partition), 6 (legal-coding protocol/precedence apparatus),
7 (§8:742–744), 8 (weights, alternatives, sensitivity), 10 (one
unhedged universal), 11 (abstract domain start), 12 (archival release),
13 (four bare keys, uncited GN 3(b)), 14 (two retained universals),
17 (763 vs 430; "seven legal bases"), 18 (generator algorithm,
end-to-end numeric example, stacking), 20 (table integration,
authorship/funding/licenses).

## Minimal remaining list (one focused patch round)

1. Disclose the five covered lines in §3 and qualify the abstract's
   spine sentence and "ten of fourteen … covered" accordingly; add
   `covered_lines` + `domain_start` (2026-02-15) to the ground-truth
   waterfall section.
2. Rewrite the §3 definitions to the artifact's semantics (row-level
   comparisons with per-authority slots; straddle clipping); delete
   "Per policy."
3. Add the disposition-class partition (named classes, counts summing
   to 15,200 with the 8,283 identified) to §3 or an appendix.
4. §8: add `@` to the four bare keys; fix "every published margin
   cell"; hedge "has not previously reached trade law"; gloss "seven
   overlapping legal bases."
5. Data availability 763: "five public issues and one pull request."
6. Fix the §3↔§6 cross-reference pair.
7. §2: "Section 232 metal programs" → the aluminum-scoped truth.
8. Cite `hts2026rev15` at GN 3(b) and `proc10339_2022` in §4.
9. Add the generator algorithm/weight definition and extend the worked
   trace to one numeric composed rate and one synthetic entry's duty.
10. Table 1: add comparison/match/raw-rate rows; cite Tables 1–2 from
    body text.
11. Fix the ground-truth scope bullet (CS, total_additional/total_rate).
12. At submission (already promised): archival release + DOI,
    authorship, funding/conflicts, own-artifact licenses.

## Verdict

**NEEDS-ANOTHER-ROUND.** The revision is genuine — no relabeling, all
regenerated numbers artifact-exact, and the repositioning as a
methods-and-data paper is coherent and consistently executed, not a
dodge. But 13 of 20 findings retain named residue, the round introduced
internal contradictions (definitions vs. counts, §4 vs. Data
availability, §5 vs. §8, §3 vs. §6), and the audit surfaced one
disclosure gap that changes how the headline result reads: the
conformance universe is a five-line probe panel and the paper never
says so. Every item on the remaining list is enumerable and most are
single-sentence patches, but item 1 reframes the abstract's central
empirical claim and items 2–3 and 9 add content — that is a round with
a re-review, not minor fixes.
