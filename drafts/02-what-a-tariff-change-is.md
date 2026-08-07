# 2. What a tariff change is, formally

Every rule in our encoding is a list of dated versions. A version has
an `effective_from` date, a formula or value, and a proof: one or more
atoms, each citing a path into a signed corpus of legal instruments and
quoting the operative text verbatim. A policy change appends a version;
it never edits one. The history is not metadata attached to the
representation — the history is the representation, and the engine
answers "the rate on date X" by selecting the version in force at X.

Three properties follow, and each one earns its keep in the 2025–26
record.

**Changes cannot outrun their instruments.** A version's proof atoms
cite corpus paths — a Federal Register document, a tariff-schedule
heading at a specific revision — and the corpus is ingested under
signed manifests before any encoding can reference it. There is no way
to encode "the §232 aluminum rate doubled" ahead of possessing the
proclamation that doubled it, and the citation carries an excerpt, so
a reviewer checks the claim against quoted text rather than against a
maintainer's memory.

**Endings are law, not deletions.** The IEEPA termination that opened
Section 1 is encoded as a rule, not as the removal of one:

```yaml
# source: rulespec-us us/policies/usitc/us-tariff-duty/overlays/ieepa/termination.yaml@main (excerpt)
- name: terminated_ieepa_additional_ad_valorem_duty_rate
  kind: parameter
  dtype: Rate
  source: Executive Order 14389 section 1
  metadata:
    proof:
      atoms:
        - path: versions[0].formula
          kind: parameter
          source:
            corpus_citation_path: us/rulemaking/federal-register/2026-02-25/2026-03832
            excerpt: "shall no longer be in effect"
  versions:
    - effective_from: '2026-02-20'
      formula: |-
        0
```

The terminated rate is a zero that took effect on February 20, 2026,
citing the order that zeroed it — which means the panel this encoding
generates carries the termination as a dated fact, exactly as it
carries the imposition. The two-endpoint character of the IEEPA wind-
down survives into the data because both endpoints are just versions.
A companion test evaluates the composed rates on the one-day period of
February 20 itself and asserts that the additional duty no longer
adds; the test is mandatory, so the change could not have merged
without pinning its own boundary.

**Schedule churn is encoded, not smoothed.** When the trade commission
issues a revision that restructures lines — consolidating headings,
retiring statistical suffixes — that restructuring is itself a dated
module (the aluminum family, for instance, carries a
revision-12 consolidation module alongside its rate overlays). A
downstream user never faces the silent question of which revision's
line structure a number refers to; the revision boundary is in the
derivation.

The full stack composes from these pieces. A composition module wires
the column rates of the tariff schedule to the authority overlays —
the Section 232 metal programs, the Section 301 families including the
forced-labor program, the per-country IEEPA reciprocal modules and
their fentanyl-order siblings, Section 122, Section 201, Section 338 —
and the engine evaluates the composed rate for a (line, country, date)
triple by resolving every overlay's version in force. Nothing in the
pipeline is hand-transcribed from a secondary source: the corpus
snapshot for this work comprises 138 signed versions — 47 Federal
Register instruments, 44 tariff-schedule revision snapshots, and 47
chapter-99 and general-note extractions — and every operative number
in the panel traces to one of them.

We do not claim this representation is novel as an idea; executable
encodings of statutes have a literature (Section 8), and dated
parameters are standard in tax microsimulation. The claim is about
fit: 2025–26 tariff law is the environment where the alternatives
visibly fail, because the thing being represented changed character.
A rate that steps down on a proclamation schedule, dies in two stages,
or applies to a line that stopped existing mid-year is not a cell in a
table. It is a small legal argument, and the representation that
survives contact with it is the one that stores the argument.
