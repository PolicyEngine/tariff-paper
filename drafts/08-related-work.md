# 8. Related work

**Tariff-rate data for the trade-war literature.** The empirical
literature on the 2018–19 tariffs built its rate data by hand, wave by
wave. Fajgelbaum, Goldberg, Kennedy, and Khandelwal digitized each
wave's product lists and statutory rates from the official
announcements to estimate the trade war's incidence
[@fajgelbaum2020return]; Amiti, Redding, and Weinstein assembled the
same sequence for pass-through event studies [@amiti2019impact;
@amiti2020whos]; Flaaen and Pierce mapped tariff-line changes into
industry exposure measures [@flaaen2019disentangling]. In each case the
tariff schedule is a bespoke research input, frozen at publication.
Bown's widely used trackers institutionalized the hand-compiled
approach as a maintained public timeline [@bown2021uschina;
@bown_piie_chart]. The 2025–26 environment strains this tradition on
two margins the earlier waves mostly spared it: authority count
(seven overlapping legal bases with distinct lifecycles) and tempo
(terminations, expiries, and revision-level rate surgery inside single
months). Teti's Global Tariff Database extends statutory rate coverage
impressively in space and time — two hundred importers back to 1988 —
but at HS-6, without the 2025–26 emergency authorities, and as data
rather than executable derivations [@teti2024missing].

**The tracker we validate against.** The nearest neighbor to our
statutory panel is its own validation reference. Yale Budget Lab's
tariff-rate-tracker is an open-source pipeline producing an
interval-encoded panel of statutory rates at the tariff-line ×
country level for the 2025–26 regime, built from the trade
commission's schedule archives with documented policy parameters
[@yaletracker_repo; @budgetlab2026tracker]; the Budget Lab's published rate series are already a benchmark other
measurement work checks against [@cavallo2026tracking] (the citation
benchmarks the Lab's report series; the tracker tool itself is
newer). We are not, therefore, the first
executable statutory tariff panel; the tracker is one, and a good
one. The contribution is the form and what the form enables: rules
at the instrument grain, each version citing and quoting its legal
source, with mandatory boundary tests — versus one pipeline whose
judgment calls live in code — and, on top of that form, a
cross-implementation conformance regime. We find no formal citation of the tool itself as of August 2026
(a web-bounded search; the tool is four months old), which suggests —
though a negative search cannot establish — that Section 3's
reconciliation is the first external research engagement with the
tracker's internals; Section 4's
derivation-backed defect reports are what that engagement produces
when a disagreement survives audit.

**Rules as code and calculator validation.** Executable encodings of
law have an established line: OpenFisca's deployed tax-benefit
engines [@openfisca], Catala's formally grounded statute-to-code
language [@merigoux2021catala], and the policy agenda articulated for
rules-as-code generally [@mohun2020cracking]. Cross-validation is
likewise institutionalized practice in tax microsimulation — NBER's
TAXSIM as a reference implementation [@feenberg1993introduction],
EUROMOD's country-report validation regime [@sutherland2013euromod],
and maintained harnesses that reconcile independent calculators
line-by-line [@taxcalculator_taxsim_validation]. That culture has not
previously reached trade law. Tariffs are, if anything, the easier
target for it — the instruments are public, the schedule is versioned
by the issuing agency, and the reference tracker already exists — and
the 2025–26 record supplies the volatility that makes the exercise
informative rather than ornamental.

**Synthetic microdata.** The synthetic-data tradition in official
statistics runs through disclosure avoidance: synthetic establishment
panels standing in for confidential business registers
[@kinney2011towards], noise-infused releases with formal privacy
guarantees [@machanavajjhala2008privacy], and, in transport and
demography, synthetic populations fit to published margins
[@beckman1996creating]. Customs data specifically have seen synthesis
for machine-learning research — artificial Korean import declarations
generated for fraud-detection benchmarks [@jeong2022customs] — while
the true U.S. transaction record remains restricted-access
[@bernard2009importers; @census_lfttd] or proprietary. Our entries
invert the disclosure-avoidance objective: the inputs are already
public, no confidentiality constraint binds, and the generator's
contract is exact integer reproduction of the customs-value margin at
its stated grain, with a declared assumptions register below it. We find no prior public U.S. synthetic customs-entry dataset with
that contract; the claim is bounded by our search (August 2026) and
Section 1's contribution list is written to survive even if one
surfaces — the representation and the reconciliation regime do not
lean on the dataset's novelty.
