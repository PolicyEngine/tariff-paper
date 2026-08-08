# Red-team review — adversarial referee report

Reviewer role: hostile referee, fresh eyes, verification-first. Every quantitative
claim traced to `facts/ground-truth.md` / `research/verification-report.md` and then
past them to the pinned artifacts, public repos, and primary legal sources.
Executed 2026-08-07. Verdict at bottom.

What I could NOT break (stated up front, because it matters): every pinned number I
recomputed reproduces exactly — the conformance waterfall from the `dc1da3af`
artifacts, the Yale build envelope from `build-timing.log` (6368.27 s;
132,526,069,168 B = 123.4 GiB; machine `hw.memsize` = 128 GiB), the entries-leg
evidence pack (38,841,305 detail rows; 0 reconciliation failures in sampled months;
108,977 crosscheck cells / 0 mismatches; $1,467,109,590,515 pilot identity), the
termination.yaml excerpt byte-for-byte, EO 14389's operative quote against the
Federal Register full-text XML, CSMS #67834313's date and cutoff, *Learning
Resources* (607 U.S. 229, decided 2026-02-20, exact holding, Nos. 24-1287/25-250),
Proclamation 11012's Feb 24 EST → Jul 24 EDT window, the forced-labor notice (60
investigations, note 52, 12.5% tier, TRQs), the HTS Rev 15 change record (sole
entry 9903.04.63, Aug 3), and all six upstream filings (open, 0 comments, author
MaxGhenis). Both §4 defect derivations are corroborated by Yale's own artifacts
(`config/policy_params.yaml` mislabels Year 8 as 14.5%; `docs/statutory_deviations.md`
records neither the solar staleness nor the column-2 gap). All five repos are
public and every pinned SHA is reachable upstream. The paper's numbers are real.
The problem is what the paper says they mean.

---

## Findings

### F1. CRITICAL — The reconciliation universe is five tariff lines, and the paper never says so

The entire conformance exercise — the abstract's headline "39,600 compared cells
… zero remain unexplained," Table 1, the §3 waterfall, the "conformant TRUE"
verdict — is computed on a witness set of **five HTS-10 lines**: 2203000030
(beer), 7202111000 (ferromanganese), 7601103000 (unwrought aluminum), 8541420010
(solar cells), 9506624040 (sport balls).

Evidence:
- `axiom-oracles @ dc1da3af`: `reference/us-tariff-panel/covered_lines.txt` (five
  lines; header: "Burn-up: append lines here as rulespec-us coverage grows");
  `reports/axiom-yale-us-tariff-panel-all-2026-08-03.json` `scope.covered_lines`
  = those five; 5 × 240 countries × 57 intervals = 68,400 in-scope intervals —
  exactly the paper's number.
- `rulespec-us @ dbf09f44`: `us/policies/cbp/us-tariff-duty/composition.yaml`
  gates on `entry_is_line_a` … `entry_is_line_e`; the encoding itself covers five
  lines of the schedule. The feeding PR is titled "Encode beer and solar tariff
  witness lines" (rulespec-us #1200).
- The tracker's spine materializes 277,303,920 rows ≈ 20,000+ HTS-10 lines. The
  compared slice is ~0.025% of it.

Against this, the paper (paper.md):
- Abstract, lines 22–24: "we reconcile the encoding cell-by-cell … on the
  tracker's own line-by-country-by-date spine over its 2025–26 coverage."
- §3, line 315–316: "The reference panel materializes 277,303,920 rows; the
  reconciled slice covers 240 partners over the tracker's 2025–26 coverage" —
  the only sentence bridging 277M → 68,400 names the country dimension (all 240)
  and the time dimension, and omits the line dimension, where the ~4-orders-of-
  magnitude restriction lives.
- §3, line 343: "Ten of the reference's fourteen policy constructs are therefore
  covered and conformant" — covered on five lines.
- §7, line 625: "duty computation runs at entry grain: for any entry, the rate
  stack in force on its date" — only entries on the five encoded lines; §7's
  "four ranges govern use" states temporal ranges only.
- Title: "a conformance-tested statutory panel … for the 2025–26 trade shock."

The words "witness," "five," or any line count appear nowhere in paper.md, the
drafts, or facts/ground-truth.md — the fact base itself omits the single most
material scope parameter, so every draft inherited the omission while the
campaign's own artifacts (covered_lines.txt, PR #1200, dispositions header
"covered slice grew 3->5 HTS-10 lines") state it plainly. Whatever the intent,
the effect is a systematically misleading denominator: readers of the abstract
and Table 1 will conclude the 2025–26 tariff schedule was encoded and reconciled;
five lines were. Temporal debt gets a full honesty apparatus (48,000 intervals,
surfaced, carried into §7's limits); the line-dimension restriction — far larger —
gets none. This is the difference between "we validated an executable encoding of
the tariff stack" and "we validated a five-line pilot of one," and it invalidates
the paper's framing, not its arithmetic. Fix: state the witness-line design in
the title/abstract/§3 definitions (a *cell* is currently defined "on the
reference's spine," which is false — it is on the witness slice of the spine),
report per-line results, and reframe contribution 2 as a witness-set conformance
regime with a burn-up path.

### F2. CRITICAL — The §201 worked trace describes an encoding that does not exist at the pin

§2 (lines 258–264): "The Section 201 overlay's staged versions — 14.75, 14.5,
14.25, 14 percent across the extension proclamation's four annual periods —
contribute nothing: the final period's version ends February 6, 2026 … and no
later version exists, so the overlay's contribution on February 22 is zero by
absence of a version in force, not by an edit." §4 (line 407): "Our encoding
carries the staged schedule and its end, citing the proclamation's table."

The pinned code (`rulespec-us @ dbf09f44`,
`us/policies/cbp/us-tariff-duty/composition.yaml`, `section_201_component_rate`):
there is no Section 201 overlay module, no staged versions, and no version ending
February 6. There is exactly one version —

    versions:
      - effective_from: '2026-02-15'
        formula: |-
          if entry_is_line_e: 0
          else: 0

— an explicit zero whose proof atoms quote the staged table as *evidence for the
zero*. Every clause of the trace inverts the artifact: a later version does
exist (it is the only one); the zero is by presence of an explicit zero version,
not "by absence of a version in force"; the encoding does not "carry the staged
schedule," it cites it. The oracle's own note says it correctly: "our side is a
proved zero grounded in the staged table" (`conformance/detail/us-tariff-yale.json`).
This is the paper's flagship illustration of its central thesis ("the derivation
is the data," "endings are law, not deletions"), and it is a fabricated mechanism
— prose describing the idealized representation rather than the pinned one. Fix:
rewrite the trace to match the artifact (proved-zero pattern, like the IEEPA
termination — which the paper does describe accurately), or encode the staged
history and re-pin.

### F3. MAJOR — False universal: "Every pull request merged in the repositories this paper reports on passed same-project cross-model adversarial QA"

§6, lines 579–583, plus "the review verdicts … are public, pinned, and
re-runnable." Counterexamples on the public record in the primary encodings
repo: rulespec-us #1239 and #1188 (both merged; zero reviews, no public review
verdicts of any kind). The fact base verifies named review arcs only (harness
r2→r7; microcosm P1 r1–r12, P2 r1–r4), and round 1 of the hostile pass already
flagged this exact all-quantifier pattern (its finding 14); the revision
responded by *broadening* the claim from "every substantive change" to "every
pull request." Scope it to the named arcs and artifacts or it is simply false.

### F4. MAJOR — The AI-use disclosure overstates the manuscript's review process

Data availability, lines 789–795: the manuscript was "revised under the same
adversarial-review regime." The record shows: hostile pass round 1 returned
NEEDS-MAJOR-WORK with 20 findings; the revision commit asserts "all 20 findings
addressed"; the round-2 adversarial verification **never executed** —
`research/hostile-pass-r2.md` is empty and `hostile-pass-r2.err.log` shows the
reviewer lane died on a usage limit ("try again at Aug 13th"). The regime the
paper describes for code is "run until a pass with no findings"; the manuscript
never received any completed post-revision adversarial pass, and this review
finds two critical defects the revision did not close (F1 was flagged as the
missing-denominator finding and closed with a waterfall that still omits the
line dimension). State the actual history: one completed hostile round, revision,
no completed verification round at submission.

### F5. MAJOR — Citation used for a claim it does not support (Cavallo → the tracker)

§3, lines 282–285: "The reference — Yale Budget Lab's tariff-rate-tracker … is
the series other measurement work already benchmarks against
[@cavallo2026tracking]." Cavallo, Llamas & Vazquez benchmark against Budget Lab's
2025 *published headline rates* ("State of U.S. Tariffs: September 4, 2025") —
publications that predate the tracker tool (released April 2026). The paper's own
verification report (B8) draws exactly this line and concludes the tracker itself
has **no** formal citation — a fact §8 then relies on for the
"first external research engagement" claim. §3's sentence quietly transfers the
Budget Lab publications' benchmark status to the tracker, inflating the
validation reference's standing. §8's phrasing ("the Budget Lab's rate series
are already the benchmark") is defensible; §3's is not. Fix §3 to say the Budget
Lab's published rate series, not the reference/tracker.

### F6. MINOR — Waterfall definition contradicts its own artifact on straddling intervals

§3 defines temporal debt as intervals that "predate that domain or straddle its
boundary — debt is surfaced, never compared." The artifact clips straddling
intervals and compares their covered portion (`temporal_debt.straddle_clipped_
intervals: 1200`; in_scope 68,400 = 20,400 covered + 48,000 pre-domain — the
1,200 are not additive). Under the paper's own definition the split does not
reconcile (20,400 + 48,000 + 1,200 ≠ 68,400); Table 1 lists the 1,200 as a
separate debt row without saying they are clipped covered intervals.

### F7. MINOR — "Our six upstream reports are public issues on that repository"

Data availability, line 763. Five issues + one patch pull request (#24). §4 gets
it right ("five issues and one patch pull request"); the availability section
relapses into the error round 1 already flagged (its finding 17).

### F8. MINOR — Section 338 duties asserted with no citation and no fact-base entry

§1 (lines 68–69, 79) lists §338 among authorities under which the U.S. "imposed
… overlapping duties" "over eighteen months," and §2/abstract include §338 in the
encoded stack. No instrument is cited anywhere in the paper, and neither
ground-truth.md nor the verification report verifies any §338 action. The only
§338 evidence in the artifact chain is the tracker's Canada layer with rates
effective 2026-08-19 — twelve days *after* the paper's date — and 3 nonzero
interval-rows out of 68,400 in the compared slice. Either cite the §338
instrument and date it precisely, or strike §338 from the "imposed" list.

### F9. MINOR — "It touches every line for four partners" (§4, line 423)

In the compared artifact, "every line" means the five witness lines (594 mfn
mismatch rows; the column-2 class is the oracle-attributed remainder, 8,283 −
7,887 = 396 cells). As a claim about the tracker's full panel it is an
extrapolation from the parser derivation (probably correct — `04_parse_products.R`
reads only the `general` field), not from compared cells; say which one is meant.

---

## Notes below the bar

- N1. "That morning the Supreme Court held" (§1): decision *date* verified; the
  time-of-day color is not in any source.
- N2. Upstream, #28 is titled as a request to "record the column-2/GN3(b) scope
  decision" in Yale's deviations registry; the paper calls it a "defect." The
  derivation supports the paper (statutorily wrong rates for CU/KP/BY/RU either
  way), but a referee who reads the issue queue will notice the softer upstream
  framing. #27/#28 were filed 2026-08-03 — "as-yet maintainer-unacknowledged" is
  literally true after four days, and honestly labeled.
- N3. The paper never partitions the 8,283 reference-attributed cells (or the
  remaining 6,917 explained cells) into classes in the text — deferred to
  artifacts; round-1 finding 2 asked for the census in-paper.
- N4. The corpus "138 signed versions" split (47+44+47) and the harness-history
  anecdotes (slim-CI artifact, all-zero-column vacuity kill) trace to campaign
  files (CAMPAIGN.md close block corroborates the arc and battery/report counts)
  but were not independently rebuilt here.
- N5. Reconciliation months: I byte-verified failure_count = 0 in 2 of 18
  committed per-month reconciliation records (first and last); the build report
  and PR body assert all 18.

## Verification table (core claims)

| Claim (paper) | Independent check | Result |
|---|---|---|
| 39,600 / 24,400 / 15,200 / 61.6% / errors 0 | `reports/axiom-yale-us-tariff-panel-all-2026-08-03.json` @ dc1da3af | reproduces exactly |
| 8,283 reference-attributed; slot counts 594/476/4,560/1,920/7,887 | same + `conformance/detail/us-tariff-yale.json` | reproduces; slots verified; s201 signature = 7,887 units on line 8541420010 |
| 14 constructs: 10 conformant, 4 excluded (named) | detail file | matches, incl. tripwire notes |
| 277,303,920 reference rows; 240 partners | -all report | matches — but universe = 5 lines (F1) |
| 68,400 = 20,400 + 48,000; 1,200 straddle | -all report scope block | matches artifact; contradicts §3's definition (F6) |
| Yale build 1h46m / 123.4 GiB / 128 GiB machine | build-timing.log + sysctl | 6368.27 s; 132,526,069,168 B; hw.memsize 128 GiB — verified |
| termination.yaml excerpt | rulespec-us @ dbf09f44 | byte-faithful |
| §201 staged-version trace | composition.yaml @ dbf09f44 | CONTRADICTED (F2) |
| EO 14389 quote, no date for collection end | FR full-text XML 2026-03832 | exact |
| CSMS #67834313, Feb 22, 12:00 a.m. Feb 24 cutoff | govdelivery bulletin | exact |
| Learning Resources, 607 U.S. 229, 2026-02-20, holding | preliminary print PDF | exact (Vol. 607 Pt. 2, pp. 229–390) |
| Proc 11012: 10%, Feb 24 EST → Jul 24 EDT (150 days) | FR full-text XML 2026-03824 | dates verified |
| FL §301: 60 investigations, note 52, 10/12.5%, TRQs, eff. Jul 24 | FR full-text XML 2026-15181 | verified |
| HTS Rev 15 (Aug 3): sole change 9903.04.63, 3 days after Rev 14 | usitc change record PDF | verified |
| Yale flat 14.5% + no col-2 branch = defects, unacknowledged | Yale config comment (Year 8 "14.5%"), deviations registry (absent), issues #23–28 (open, 0 comments) | corroborated |
| Entries: 38,841,305 rows; 0 failures; 108,977 cells; $1.467T identity; σ=2.6916; is_synthetic | microcosm @ d4b08551/6707ed59 evidence pack + PR bodies | verified |
| "All code, corpora, evidence public at pinned revisions" | gh api ×5 repos + 3 pins | public, reachable |
| "Every merged PR passed cross-model adversarial QA" | rulespec-us #1239, #1188 | FALSE (F3) |

## Falsification attempt on the headline number

Headline: "39,600 compared cells … zero remain unexplained and zero are open
against our encoding." I attempted to falsify it three ways. (1) Arithmetic:
recomputed from the pinned report — holds. (2) Dispositions: sampled the two
escalated classes against primary instruments and against Yale's own code and
config — both derivations hold; Yale's config comment even contains the error
(Year 8 labeled 14.5%). (3) Vacuity: checked whether "conformant" slots are
zero-vs-zero artifacts — the committed slice carries nonzero forced-labor
(1,290 rows), Brazil-301 (18), and §338 (3) intervals, so those slots are
exercised, thinly but genuinely. I could not falsify the number. What I falsified
is its advertised scope: the zero is a five-line, post-2026-02-15, 33-probe-date
result presented as a reconciliation of the tracker's 2025–26 spine (F1), and one
of its two showcase dispositions is narrated with a mechanism the pinned encoding
does not contain (F2).

## Verdict

**Reject in current form (reject-and-resubmit / major revisions).** The artifact
chain is unusually good — every number traces, pins resolve, primary sources
check out, and the upstream defect reports are real contributions. But the
paper's framing misrepresents the comparison universe by roughly four orders of
magnitude on the dimension it never mentions, its central worked example
misdescribes the pinned code, a §6 universal is contradicted by the public
record, and the disclosed review regime did not complete. The honesty framings
(raw 61.6% beside the zero; author-attributed defect labels) are genuine rigor
*within the disclosed dimensions* — which is precisely why the undisclosed
dimension reads, to a hostile referee, as constructed rather than accidental.
A resubmission that states the witness-line design plainly, fixes F2, and scopes
F3–F5 would be a strong methods paper.

Counts: 2 Critical (F1, F2) · 3 Major (F3, F4, F5) · 4 Minor (F6–F9) · 5 notes.
