# Research brief — verification + prior art for the tariff paper

You are a fact-verification and literature agent for an academic working
paper. Work read-only on the local filesystem; use your network access
for primary sources. Your final message is machine-harvested — return
the structured report only, no preamble.

The paper: encodes 2025–26 US tariff law as dated executable rules,
conformance-tests them against Yale Budget Lab's tariff-rate-tracker,
reports two tracker defects upstream, and releases synthetic customs
entries reproducing Census margins exactly. You verify claims and map
prior art; you do NOT write prose.

## Part A — verify against PRIMARY sources (never Wikipedia, never news
summaries when the instrument itself is reachable)

For each item return: VERDICT (CONFIRMED / CORRECTED / UNVERIFIED),
the primary URL, the exact value, and a BibTeX entry where citable.

A1. Executive Order 14388 — does it set tariff COLLECTION end
2026-02-24 for the IEEPA duties? (Federal Register document number,
date, exact operative language.)
A2. Learning Resources, Inc. v. Trump (Supreme Court) — decision date,
citation, precise holding on IEEPA tariff authority.
A3. Section 122 balance-of-payments surcharge — imposition instrument
and expiry date (claimed 2026-07-24); the 150-day statutory limit in
19 U.S.C. 2132.
A4. Forced-labor Section 301 action — Federal Register doc 2026-15181:
does it finalize 60 determinations and create HTS chapter-99 note 52?
A5. USITC HTS 2026 revision count as of 2026-08 (claimed Revision 15,
with UK pharmaceutical §232 rates zeroed in it).
A6. HTSUS General Note 3(b) — quote the current operative text listing
the column-2 countries (expect Cuba, North Korea, Belarus, Russia).
A7. Proclamation 10339 (solar safeguard extension) — confirm the staged
duty schedule and its final period end date (claimed 2026-02-06).
A8. Yale Budget Lab tariff-rate-tracker — repository URL, license,
maintainer org, and whether commit c4307e51 is reachable upstream.

## Part B — prior-art sweep

For each: full citation (BibTeX), one sentence on what it does, and one
sentence on how it differs from this paper. Cover at minimum:
B1. Fajgelbaum, Goldberg, Kennedy, Khandelwal (QJE 2020) "The Return to
Protectionism" — how they constructed statutory tariff schedules.
B2. Amiti, Redding, Weinstein (JEP/AER-Insights 2019/2020) tariff
pass-through work — their tariff-rate data construction.
B3. Flaaen & Pierce (Fed) tariff studies — data construction.
B4. Bown (PIIE) tariff trackers — method (hand-maintained?), coverage.
B5. The restricted LFTTD (Census Longitudinal Firm Trade Transactions
Database) — access model, contrast with public synthetic entries.
B6. Law-as-code: OpenFisca; Catala (Merigoux, Chataing, Protzenko ICFP
2021); any tax-calculator validation literature (EUROMOD, TAXSIM
cross-validation practice, NBER TAXSIM papers).
B7. Synthetic microdata literature relevant to transaction-level
synthesis with exact marginal reproduction (e.g. synthetic
establishment/LEHD work, SynLBD, OnTheMap noise infusion).
B8. Has Yale's tariff-rate-tracker been cited in any paper, preprint,
or agency document? Search Google Scholar/SSRN/arXiv/RePEc.
B9. Anything occupying THIS paper's exact spot: an executable,
instrument-cited statutory tariff panel, or public synthetic customs
entries. If something exists, say so plainly — that changes the paper.

## Part C — hostile-expert pass

List the 10 claims from facts/ground-truth.md (read it at
/Users/maxghenis/TheAxiomFoundation/tariff-paper/facts/ground-truth.md)
a hostile referee would attack first, each with the check they would
run and whether the current evidence survives it.

## Output format

```
## A. Verifications
A1. VERDICT — value — URL
    @bibtex{...}
...
## B. Prior art
B1. citation — what it does — how this paper differs
    @bibtex{...}
...
## C. Hostile-expert list
1. claim — the check — survives? y/n/needs-X
...
```
