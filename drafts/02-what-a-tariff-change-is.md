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
# source: rulespec-us us/policies/usitc/us-tariff-duty/overlays/ieepa/termination.yaml@dbf09f44 (excerpt)
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
citing the order that zeroed it — the panel this encoding generates
carries the termination as a dated fact, exactly as it carries the
imposition. One scope note, stated precisely: this encodes the LEGAL
endpoint, which is the semantics the reference panel publishes by
default and the semantics we reconcile against in Section 3. The
operational wind-down of Section 1 — CBP's February 24 collection
cutoff — is an agency bulletin, not a rule version in this encoding;
a parallel collection-status series sourced from such bulletins is
future work, and nothing in this paper's data should be read as
carrying it. A companion test evaluates the composed rates on the one-day period of
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

The engine's operational semantics are part of the claim, not an
implementation footnote. At the pinned engine revision `ffd82132`, they
are:

| Operation | Runtime rule | Consequence for this paper |
|---|---|---|
| Query time | Compare inclusive version bounds at the query period's start. | A day-grain query uses that day's start; intra-day legal cutoffs are not represented. |
| Version selection | Among applicable versions, select the greatest `effective_from`; a gap raises a missing-version error. Equal-start ties fall through to document order. | The encoding avoids relying on an equal-start tie as legal precedence. |
| Branch precedence | Evaluate the formula's authored, nested conditionals. The engine has no general tariff-authority hierarchy solver. | Exceptions and priority must be explicit inside each component formula. |
| Stacking | Add the component outputs explicitly in the composition formula. | No duty stacks merely because two instruments coexist. |
| Types and errors | Enforce declared scalar-versus-judgment shapes and reject unknown outputs, parameters, relations, or units; missing inputs, versions, or values; type mismatches; and division by zero. | `Rate` labels the composition's scalar output; it does not supply a duty base or turn a rate into money. |

The caller precondition is equally important. The composition defines
exact-line predicates for five witness lines and uses them within
components, but it does not require their disjunction as a top-level
domain guard. Outside the slice, the MFN component can fall through to
zero and, during the Section 122 window, a non-exempt line can receive
the blanket surcharge; their sum can therefore look plausible rather
than error. All tariff-composition comparisons in Sections 3–4
restrict the input to the true five-line intersection. A fail-closed
guard and negative off-slice tests are prerequisites for archival
release.

Within that caller-enforced slice, the composed function maps a
(tariff line, partner country, query period) triple to the ex-post,
posted ad valorem component-rate stack under legal-date semantics. It
does not compute specific duties requiring physical quantities,
Section 232 duties requiring declared aluminum-content value, quota
position, or sub-monthly timing. Nor does it resolve entry-specific
facts such as in-transit exceptions or claimed exclusions, or
knowledge-time: `effective_from` records legal-valid time, so a
retroactive instrument enters the ex-post record when encoded. Those
uses need inputs and state absent from this function, and Section 8
repeats the boundary.

The full stack composes from these pieces. A composition module wires
the column rates of the tariff schedule to the authority overlays —
the Section 232 aluminum program (the witness composition's 232
family), the Section 301 families including the forced-labor program, the per-country IEEPA reciprocal modules and
their fentanyl-order siblings, Section 122, Section 201, Section 338 —
and the engine evaluates the composed rate for a caller-restricted
(line, country, period) triple by resolving every overlay's version in
force. Nothing in the
pipeline is hand-transcribed from a secondary source: the corpus
snapshot for this work comprises 138 signed versions — 47 Federal
Register instruments, 44 tariff-schedule revision snapshots, and 47
chapter-99 and general-note extractions — and every operative number
on the evaluated witness paths traces to one of them.

We do not claim this representation is novel as an idea; executable
encodings of statutes have a literature (Section 9), and dated
parameters are standard in tax microsimulation. The claim is about
fit: 2025–26 tariff law is the environment where the alternatives
visibly fail, because the thing being represented changed character.
A rate that steps down on a proclamation schedule, dies in two stages,
or applies to a line that stopped existing mid-year is not a cell in a
table. It is a small legal argument, and the representation that
survives contact with it is the one that stores the argument.

**A worked trace.** Take the solar query of Section 1 — the
crystalline-silicon cell line, one of the five witness lines of
Section 3, from Malaysia on February 22, 2026 — and read the actual
rules at the pin rather than a stylized version of them. The
column-rate module contributes the line's general rate per the
tariff-schedule revision in force. The Section 201 component is an
explicit zero: its only operative version in the modeled temporal
window begins February 15, 2026, nine days after the safeguard's
staged schedule expired. The historical stages are not executable
versions in this component; its proof atoms document the derivation of
the operative zero by quoting the extension proclamation's staged
table (14.75, 14.5, 14.25, 14 percent, each period dated) and the
schedule's compiler's note that the safeguard has expired
[@proc10339_2022].
The operative formula is a constant; the legal argument for the
constant travels with it, which is the representation's point. The
IEEPA component resolves through the termination rule shown above:
from February 20 the termination's zero governs [@eo14389_2026], so
the legal-date answer carries no IEEPA contribution — while the
collection cutoff two days later [@csms67834313_2026] is, per the
scope note, outside this function's semantics. Every step is a
version lookup carrying instrument citations. A separate boundary
probe changes both the partner and date: at the February 24, 2026 probe
for solar cells from Canada, the pinned report shows both implementations return column rate
zero, IEEPA zero, Section 201 zero, Section 122 at 0.10 — a total of
exactly 10 percent, the balance-of-payments surcharge standing alone
atop an otherwise-terminated stack. The "two defensible answers" of
Section 1 become two different, explicit functions — and this paper's
panel computes the legal-date one.
