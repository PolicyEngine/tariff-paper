# Round-diff review 3 — verifying revision 3 (e117d94)

Date: 2026-08-07. Reviewer: round-diff lane, final-round verification.
Inputs: `paper.md` @ e117d94 ("Round 4: the verifier's enumerated list,
with the two content additions"), `research/round-diff-2-report.md`
(verdict NEEDS-ANOTHER-ROUND, enumerated list). Independently re-opened:
`axiom-oracles @ dc1da3af` (`reports/axiom-yale-us-tariff-panel-all-
2026-08-03.json`, `conformance/detail/us-tariff-yale.json`,
`dispositions/us-tariff-panel.yaml`), `rulespec-us @ dbf09f44`
(`composition.yaml`), and the full 328a120..e117d94 diff.

## Headline

All nine briefed items landed and verify against the pins — including
the two content additions, both of which are artifact-exact (the
partition was re-verified computationally: 15,200 case ids across the
30 entries, zero duplicates; the numeric endpoint matches case
`family-8541420010-0076` slot for slot). For the first time in four
rounds the commit message does not overstate its coverage. One new
finding: §4's column-2 paragraph claims the disagreement "touches all
five lines for the four partners"; the artifact shows four of five
(beer's mfn is 0.0 = 0.0 for all four column-2 partners; the mfn
slot's 594 decomposes as 528 column-2 = 4 lines × 4 partners × 33
probes, + 66 FTA-layer). The sentence entered in round 3 and slipped
past the round-2 audit. One-word fix.

## Briefed items audit

| # | Item | Status | Evidence |
|---|------|--------|----------|
| 1 | Probe-date comparison unit (§3 definition + abstract) | **CLOSED** | Abstract:25 "39,600 probe-date comparisons"; §3:334–338 defines a comparison as one covered row at one probe date, 33 per line-partner; waterfall bullet 357–359 "(5 lines × 240 partners × 33 probes)". Artifact: `case_count = 39,600`; per-(line,country) distinct probes = {33: all 1,200 pairs}; sum of `unit_count` = 39,600; per-line probe range 2026-02-15→2026-12-31. "Interval boundaries and their neighbors" matches the observed boundary-pair placement (e.g. 03-31\|04-01, 02-19\|02-20, 02-23\|02-24). |
| 2 | Contribution 2 witness qualifier (§1) | **CLOSED** | paper.md:136–138 "a cross-implementation reconciliation against the leading open reference, executed depth-first on a five-line witness slice of its spine". Residual (unchanged, was the round-2 aside): contribution 1 still carries no line-domain gloss; §2/§3/§7 disclosures now bound it within two paragraphs, so Low. |
| 3 | Cavallo at the flagged §3 site; §8 consistent | **CLOSED** | §3:294–297 now attaches the citation to "the Budget Lab's published rate series … a benchmark other measurement work checks against"; §8:758–761 same construction plus the corrective parenthetical. The two sites now agree; the tool is nowhere claimed as the benchmarked object. Bib entry (Cavallo/Llamas/Vazquez, version 2026-01-30) predates the four-month-old tool — internally consistent. |
| 4 | In-paper disposition partition | **CLOSED — artifact-exact** | §3:361–370. File `dispositions/us-tariff-panel.yaml @ dc1da3af`: header carries "Every mismatched unit appears in exactly one entry."; `grep -c '^- id:'` = 30; computational check: 15,200 case-id references, 15,200 distinct, 0 duplicates. Family census from entry ids: ieepa-metals-exclusion 13 pure (paper: "13 entries" ✓), mfn-column2-reference-gap 4 pure "plus combinations" ✓ (7 combination entries exist), s232-beer-aluminum-content-basis 2, mfn-fta-preference-layer 2, s122-metal-exclusion 1, s201-solar-safeguard-expiry 1 — exactly the six families the paper names. 8,283 = units under `disposition: upstream_engine_gap` (+6,917 explained_residual = 15,200) ✓. Entries carry concept, case_selector, and instrument citations (checked entry `7202111000-mfn-6p5v1p4`: GN 3(b) proof-atom reference, ch. 99 U.S. note 30(c), upstream source URL, arithmetic, selector_binding with sha) ✓. |
| 5 | Numeric endpoint (Canada solar, 2026-02-24) | **CLOSED — artifact-exact** | §2:278–283. Report case `family-8541420010-0076`: hts 8541420010, countries = ['1220'] only, match: true, '2026-02-24' in probe_dates; expected = axiom = {mfn 0.0, ieepa 0.0, section_122 0.1, section_201 0.0, …, total 0.1}. "Both implementations", "column rate zero, IEEPA zero, Section 201 zero, Section 122 at 0.10 — a total of exactly 10 percent" all exact. Adjacent families corroborate the narrative arc (0089: ieepa 0.35 through 02-19; 0090: all-zero 02-20..02-23; 0080: s122→0, forced-labor 0.1 from 07-24). |
| 6 | §7 composed-domain five-line gating | **CLOSED** | §7:680–685 "the pinned composition gates on the five witness lines, so entry-level duty computation is currently defined for entries on those lines, and extends with the encoding"; four-ranges paragraph 714–715 "(the five witness lines, February 2026 onward)". Confirmed at the pin: composition.yaml gates on `entry_is_line_a..e`. Residual (pre-existing, Low): §5's closing sentence (603–608) still glosses composition without the line dimension; §7, which governs use, now bounds it. |
| 7 | Table 1 waterfall rows + straddle relabel | **CLOSED** | New rows: witness slice, 68,400 = 20,400 + 48,000, 39,600 (33 probes per line-partner), 24,400/15,200 (61.6% raw), 30 disposition entries (each unit in exactly one) — all artifact-exact. "Temporal debt surfaced (domain-straddling intervals)" → "Boundary-straddle clip events recorded \| 1,200" = `temporal_debt.straddle_clipped_intervals` ✓, now consistent with §3's wholly-predates definition. Body now cites Table 1 (§3:386). |
| 8 | Ground-truth scope bullet | **CLOSED** (residual note) | facts/ground-truth.md:20–27 rewritten: CS now among the four excluded:technical (other, rate_301_cs, stacking_outputs, swiss_framework) ✓ = detail file; the total_additional/total_rate-reconciliation claim is gone ✓. Residual (Low, fact file only): its enumeration of the covered 10 merges the detail file's two IEEPA records (ieepa_fentanyl, ieepa_reciprocal) into one and adds "total", which is a comparison slot, not one of the 14 policy records. The paper itself never enumerates the ten, so no paper-facing effect. |
| 9 | One-liners | **CLOSED (all)** | "Per policy": zero hits. §2:238 "the Section 232 aluminum program (the witness composition's 232 family)" — matches the pin (sole 232 rate component is aluminum; beer aluminum-content-basis Judgment rule). §8:784 "To our knowledge that culture had not previously reached trade law." "Seven overlapping legal bases" → "a base schedule plus six overlay authorities" (§8:744), consistent with §1's framing. `hts2026rev15` cited twice (§1:89 Rev 15; §4:461 GN 3(b)); bib entry (Rev 15, Aug 3 2026 release, General Notes retrieved) supports both uses. Bonus: the F3/N5 abstract review-clause scoping also landed (42–45, scoped to harness + entries pipelines). |

## New findings this round

**R3-1 [Must-fix, one word] §4's column-2 footprint claim is
artifact-false.** §4:467–469: "within the witness slice it touches all
five lines for the four partners." At the pin the column-2
disagreement touches **four** of the five lines: every beer
(2203000030) case family containing the four column-2 partners
(2390/4621/4622/5790) has expected mfn 0.0 = axiom mfn 0.0 (beer's
column-2 rate is specific, not ad valorem, so both panels carry zero);
no beer-mfn disposition entry exists among the 30. Decomposition
proof: mfn slot mismatches = 594 = 528 column-2 (4 lines × 4 partners
× 33 probes; 7202 1.4→6.5, 7601 2.6→18.5/RU 70, 8541 0→35, 9506
0→30) + 66 FTA-layer units. Introduced in round 3 (328a120), missed
by the round-2 audit. Fix: "touches four of the five lines" (optionally
noting beer's ad-valorem column-2 coincides at zero, so the gap is
invisible there).

**R3-2 [Minor] Mixed unit vocabulary survives the probe-date fix.**
Under §3's own definitions (cell = line × partner × date-interval
row; comparison = row × probe date), the mismatch counts are unit
counts, but four sites still say "cell(s)"/"rows": §3:338 "A
*disposition* closes a mismatched cell"; §3:368 "8,283 cells";
§3:374–375 "exceed the 15,200 distinct rows"; §4:454 "7,887
mismatched cells"; Table 1 "Reference-attributed cells". The partition
sentence itself says "unit" correctly. Swap to "units"/"comparisons"
(or define the shorthand once).

**R3-3 [Nit] Leftover cross-reference polish.** `proc10339_2022`
cited in §2's trace but still not in §4's derivation paragraph
(same content, one section apart); Table 2 is never cited from the
body (round-2 item 10's last quarter); orphan bib keys
`eo14388_2026`, `proc11020_2026` are uncited (harmless — pandoc
drops them; eo14388 is correctly never cited per the fact base's
prohibition).

## Regression check

None found. The rebuilt `build/paper.pdf` contains the round-4 text
("probe-date comparisons", "39,600") with no unresolved citations;
all 31 cited keys resolve against references.bib; every number the
round touched re-verifies at the pins (39,600 = 5×240×33; 30/15,200/
0-dup partition; 8,283 upstream_engine_gap; 10 conformant + 4
excluded:technical with the named IDs; 61.616162; 1,200 clip events;
Canada-solar endpoint). Cross-references (abstract ↔ §3 ↔ Table 1)
are consistent. The commit message's "Closes" list matches what
actually closed — the first round of the four for which that is true.

## Verdict

**READY-AFTER-MINOR-FIXES.** All nine briefed items closed, verified
independently against the pinned artifacts; both content additions are
artifact-exact, not narrated. The minor list, in priority order:

1. R3-1 (mandatory): §4 "all five lines" → four of the five lines.
2. R3-2 (recommended): unify mismatch-count nouns to units/comparisons
   at the five listed sites.
3. R3-3 (optional): proc10339_2022 in §4; cite Table 2 from §5; the
   ground-truth 10-construct enumeration (IEEPA = two records, drop
   "total"); contribution 1 / §5-closing line-domain glosses.

Item 1 is the only claim a reader with the artifact could falsify;
nothing on the list requires regenerating any number. Known-remaining
per the round-4 commit (figures, archival release, second cross-model
round, venue/authorship) are disclosed in-paper and stand as stated.
