# Round-diff review 2 — verifying revision 2 (328a120)

Date: 2026-08-07. Reviewer: round-diff lane, round 3 verification.
Inputs: `paper.md` @ 328a120 ("Round 3: witness-slice disclosure
everywhere, truthful section 201 trace, and both referees' remaining
items"), `research/round-diff-report.md` (round-2 audit, 12-item patch
list), `research/red-team-report.md` (2 Critical / 3 Major / 4 Minor).
Beyond the briefing, this audit re-opened the pinned artifacts:
`axiom-oracles @ dc1da3af` (`reports/axiom-yale-us-tariff-panel-all-
2026-08-03.json`, `conformance/detail/us-tariff-yale.json`) and
`rulespec-us @ dbf09f44` (`us/policies/cbp/us-tariff-duty/
composition.yaml`), and diffed e4215c3..328a120 in full.

## Headline

The two Criticals are genuinely closed and artifact-verified. The
round also skipped roughly half of the enumerated patch list while its
commit message claims "both referees' remaining items" — the second
consecutive round whose commit message overstates its own coverage.
One Major (F5/Cavallo) was fixed at the site that was already
defensible and left standing at the site that was flagged.

## Briefed item 1 — five-line witness-slice disclosure

| Site | Status | Evidence |
|---|---|---|
| Abstract | **CLOSED** | paper.md:22–31 "on a five-line witness slice of the tracker's spine — one tariff line per major authority family, crossed with all 240 partners and the tracker's full 2025–26 date intervals"; "extending the reconciliation from the witness slice to the full schedule is stated future work"; waterfall clause names "the witness-line design". |
| §3 | **CLOSED** | paper.md:301–317 design paragraph names all five lines with HTS codes; "roughly 0.025 percent"; "exact within the slice and says nothing outside it"; waterfall bullet carries "5 lines × 240 partners × 57 intervals" (343–344). |
| §7 | **PARTIAL** | Reconciliation range carries the slice (691–692). But the duty-computation range still glosses "the composed spine's domain" as "(February 2026 onward)" — temporal only (694–696) — and §7 opens "duty computation runs at entry grain: for any entry" (663–664). At the pin the composed domain is five lines (composition.yaml gates every component on `entry_is_line_a..e`); entries off those lines have no computable rate stack. The line dimension is undisclosed at the one place that governs *use*. Same silent scope in §5's closing sentence ("compose into duty computation at the grain where duties are assessed", 589–591). |
| Contributions (§1) | **OPEN** | Contribution 2 still reads "a cross-implementation reconciliation against the leading open reference **on its own spine**" (135–137) with no witness qualifier — the red team's F1 fix explicitly asked for contribution 2 to be reframed as a witness-set regime with a burn-up path. Contribution 1 ("the 2025–26 stack encoded") likewise carries no line-domain gloss. |

Arithmetic vs the pinned artifact — **exact**:
`scope.covered_lines = [2203000030, 7202111000, 7601103000,
8541420010, 9506624040]` (the paper's five, same order);
`countries = 240`; `reference.extract_revisions = 57`;
`in_scope_intervals = 68,400` = 5 × 240 × 57;
`covered_intervals = 20,400`; `temporal_debt.pre_domain = 48,000`;
`straddle_clipped_intervals = 1,200`; `domain_start = 2026-02-15`
(matches "our encoded rule history begins 2026-02-15"). The 0.025%
claim checks (5 / ~20.3k lines behind 277,303,920 rows).

## Briefed item 2 — §2 worked trace vs the pinned §201 rule

**CLOSED — verified against `dbf09f44` at the atom level.**
`section_201_component_rate` has exactly one version,
`effective_from: '2026-02-15'`, formula `if entry_is_line_e: 0 /
else: 0` — a constant zero ("The operative formula is a constant" ✓;
"the rule's single version is a zero" ✓; "the encoded domain begins
February 15, 2026" ✓ = artifact `domain_start`; "nine days after the
safeguard's staged schedule expired" ✓ Feb 6 → Feb 15).
`entry_is_line_e` is HTS 8541.42.00.10, crystalline-silicon PV cells —
the trace's line. The proof atoms quote FR 2022-02906 (Proclamation
10339) verbatim: all four period-dated rates — "February 7, 2022
through February 6, 2023"/"14.75%", …"14.5%", …"14.25%", "February 7,
2025 through February 6, 2026"/"14%" — **and** the HTS compiler's note
"[Compiler's note: This subheading and its related note, U.S. note 18
to this subchapter, have expired. …]". The paper's claim that the
atoms carry "the extension proclamation's staged table … and the
schedule's own compiler's note" is exactly true. The oracle detail
note corroborates: "our side is a proved zero grounded in the staged
table, quota change, and HTS expiry note." Red-team F2 is dead.

## Briefed item 3 — the three Majors

| Finding | Status | Evidence |
|---|---|---|
| F3 review universal | **CLOSED** (minor residual) | "Every pull request" — zero grep hits. §6:614–621 now scopes to "the comparison harness, the entries ingest, and the entries generator … run per change on those components (six rounds on the harness, twelve and four on the two pipeline stages)" — matches the ground-truth review-coverage bullet. Residual: the abstract's "AI agents built the encodings and datasets behind compile, test, and oracle gates, with same-project cross-model adversarial review run until a pass with no findings" (42–45) leaves the review clause attachable to the encodings; one scoping phrase would close it. |
| F4 AI-use disclosure | **CLOSED** | Lines 829–839 now state the actual record: one cross-model hostile round (20 findings addressed), then same-family (Claude-class) round-diff + red-team verification rounds "whose findings this version incorporates." Matches the repo trail (hostile-pass-report.md; empty r2 + err.log; the two Claude reports). "Revised under the same adversarial-review regime" is gone. No claim of a completed second cross-model round. |
| F5 Cavallo citation | **OPEN — fixed at the wrong site** | §8 got the corrective parenthetical (737–740: "the citation benchmarks the Lab's report series; the tracker tool itself is newer"). §3:287–290 — the sentence the red team flagged — is unchanged: "The reference — Yale Budget Lab's tariff-rate-tracker … is the series other measurement work already benchmarks against [@cavallo2026tracking]". §3 and §8 now contradict each other. One-sentence fix in §3 ("whose published rate series other measurement work already benchmarks against" or move the citation to the Lab's series). |

## Briefed item 4a — round-2 patch-list spot-check (12 items)

| # | Item | Status | Evidence |
|---|---|---|---|
| 1 | Disclose five lines (§3, abstract, "ten of fourteen", ground truth) | **CLOSED** (residuals under briefed item 1) | Paper ✓; "holds on the covered slice" ✓ (373–374); ground-truth round-3 section adds covered_lines + domain_start ✓. |
| 2 | Rewrite §3 definitions to artifact semantics; delete "Per policy" | **PARTIAL** | Cell = row with concept slots ✓ (matches artifact: mismatches are `kind: total_difference` with nested authority slots); straddle clipping described ✓ (1,200 clip events ✓). But **"Per policy" survives** (343) — the bullet was rewritten around it — and the comparison definition still contradicts the artifact (see New finding N1). |
| 3 | In-paper disposition-class partition | **OPEN** | §3:353–356 still defers wholesale to "the committed disposition artifacts"; overlapping slot counts are not a partition of the 15,200 / 8,283. |
| 4 | §8: @-keys; "every published margin cell"; hedge trade-law universal; gloss "seven legal bases" | **PARTIAL (2/4)** | Four keys now `@`-cited ✓ (716–717, 725–726); generator contract corrected ✓ (782–784). "That culture has not previously reached trade law" (763–764) still unhedged; "seven overlapping legal bases" (724) still unglossed. |
| 5 | Data availability filings sentence | **CLOSED** | 803–804 "five public issues and one patch pull request" — consistent with §4:458–459. |
| 6 | §3↔§6 cross-reference pair | **CLOSED** | §3 holds its own upgrade list (296–299); §6 states its own boundary (645–647). |
| 7 | §2 "Section 232 metal programs" → aluminum truth | **OPEN** | Phrase intact (237). Pin confirms the sole §232 rate component is `section_232_aluminum_component_rate` (plus a beer aluminum-content Judgment rule, terminated 2026-04-06); detail note: unencoded §232 programs "surface as classified mismatches" — the 1,920. |
| 8 | Cite hts2026rev15 at GN 3(b); proc10339_2022 in §4 | **OPEN (half)** | `hts2026rev15`: zero citations — orphan bib entry; the GN 3(b) verbatim quote (443–449) is uncited. `proc10339_2022` now cited in §2's trace (269) but not in §4's derivation paragraph. |
| 9 | Generator algorithm/weights + numeric end of worked trace | **PARTIAL** | Largest-remainder algorithm + weight meaning added ✓ (§5:529–537, matches ground truth). Trace still names no composed numeric rate; no synthetic-entry duty computation exists anywhere in the paper. |
| 10 | Table 1 comparison/match/raw-rate rows; cite Tables 1–2 from body | **OPEN** | Table 1 unchanged (no comparisons/matches/raw-rate rows); "Table 1"/"Table 2" appear only as the tables' own headings. |
| 11 | Fix ground-truth scope bullet (301-CS, total_additional/total_rate) | **OPEN** | facts/ground-truth.md:19–24 still claims the §301 family "incl. … CS" and "plus total_additional/total_rate reconciliation" — contradicting the artifact (both `excluded:technical` with tripwires), the paper's §3, and now the round-3 section appended in the same file. |
| 12 | Submission apparatus (release, DOI, authorship, licenses) | **DEFERRED as promised** | "accompanies submission; until then the commits above are the replication interface" — stands. |

Score: 3 closed, 3 partial, 5 open, 1 deferred-as-promised.

## Briefed item 4b — new findings this round

**N1 [High] The comparison unit still contradicts the artifact, and
the witness arithmetic now makes it visible.** §3 defines "A
*comparison* evaluates one covered cell" with cell = (line, partner,
date-interval) row; the waterfall says "Covered cells yield 39,600
comparisons" from 20,400 covered cells. 39,600 ≠ 20,400 and the text
never explains the expansion. The artifact's unit is a **probe-date
evaluation**: `case_count = 39,600` = 5 × 240 × **33 probe dates** per
line-partner (each covered interval evaluated at its boundary dates;
mismatch ids are `panel-{line}-{country}-{probe_date}`, e.g.
`panel-2203000030-1000-2026-02-15`), spanning the 17 covered intervals
per line-partner. The abstract's "39,600 compared cells" (25) is
wrong under §3's own cell definition. One sentence fixes it: define
the comparison as a covered interval evaluated at probe dates (33 per
line-partner) and re-term "compared cells" → "comparisons" or
"probe-date evaluations." This is round-2 finding 2's residue made
more prominent by the round-3 disclosure, so it now reads as an
internal arithmetic contradiction.

**N2 [Major, = F5] §3 vs §8 Cavallo contradiction** — see briefed
item 3. New this round because §8 was corrected and §3 was not.

**N3 [Low] Table 1's straddle row vs §3's new definition.** §3 now
defines temporal debt as intervals that "wholly predate" the domain
and describes straddlers as clipped-and-compared; Table 1 still labels
the 1,200 "Temporal debt surfaced (domain-straddling intervals)". The
label follows the artifact's field nesting
(`temporal_debt.straddle_clipped_intervals`) but no longer matches the
paper's own definition; rename the row ("Domain-straddling intervals,
clipped and compared (clip events)" or similar).

**N4 [Process] Commit message overstates the round again.** 328a120
says "witness-slice disclosure everywhere … and both referees'
remaining items." The disclosure is absent from the contributions
paragraph; at least seven enumerated referee items were untouched
("Per policy", metal programs, §3 Cavallo, trade-law universal,
seven-bases gloss, GN 3(b) cite, Table 1 rows, disposition partition,
ground-truth bullet). Round 1's commit had the same defect ("all 20
findings addressed"). Reviewers downstream should continue to treat
commit messages as claims to verify, not records.

**N5 [Low] Abstract review-clause scoping** — see F3 residual.

## Relabel-without-regenerate check

Data layer: **clean, again**. Every number the round touched or that I
re-derived is artifact-exact at the pins: covered_lines (the five, in
order), 240, 57, 68,400 = 20,400 + 48,000 (+1,200 clip events),
domain_start 2026-02-15, 39,600/24,400/15,200, 61.616162, slot
mismatches 594/476/4,560/1,920/7,887 (sum 15,437 > 15,200 as the
overlap sentence says), error_count 0, 10 conformant / 4
excluded:technical with the paper's four names and reasons, and the
§201 rule byte-for-byte. The §2 trace fix is a true **regenerate**:
the prose was rewritten to the artifact's mechanism and verifies at
the atom level. The one relabel-shaped move this round is narrative:
F5 was "fixed" by editing the site that was already defensible (§8)
while the flagged site (§3) kept the misattribution verbatim.

## Verdict

**NEEDS-ANOTHER-ROUND** — but a short, mechanical one. The items that
reframed the paper (five-line disclosure, truthful §201 trace, scoped
review claim, honest AI-use record) are done and verified against the
pins; nothing at the data layer is wrong anywhere. What remains: one
open Major with a new internal contradiction (F5, one sentence), one
forced arithmetic contradiction (N1, one or two sentences), two
skipped content items (disposition partition; numeric trace/entry
duty), roughly eight one-line patches (items 2's "Per policy", 4's
two universals, 7, 8, 10, 11, contributions qualifier, §7 line-domain
gloss, N3 label), and the F3/N5 abstract scoping phrase. Given two
consecutive rounds of overstated closure commits, the next patch
round needs this same verification pass before the paper is called
ready; if every item on this list lands, that pass should be
READY-AFTER-MINOR-FIXES at most.
