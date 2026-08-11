# Tariff paper — plan and gates

Working title shape: **"Executable tariff law: a conformance-tested statutory panel
and synthetic customs entries for the 2025–26 trade shock."**

One working paper first (SSRN/arXiv), then peeled venue submissions:
the dataset descriptor (Scientific Data or IJM) and the conformance
methodology (ICAIL/AI & Law). The distributional wedge paper (tariff vs
income tax over synthetic entries) is a follow-on, blocked on the PE
wedge build, and is NOT this paper.

## Hard gates (all Max)

- **Nothing leaves this machine without Max**: no repo push, no preprint
  post, no submission, no Yale contact. Publishing a benchmark against
  Yale's tracker IS Yale engagement — framing is Max's call.
- **Message-House.md loads before any outward-facing copy pass** (Axiom
  writing guardrail).
- Authorship slots are Max's call.

## Pipeline mapping (longform-writing skill, paper-sized)

1. Fact catalog + ground-truth: `facts/ground-truth.md` (this session,
   from artifacts read/produced today; recalled-not-read items carry
   `[NEEDS VERIFICATION]`).
2. Research lane (sol/terra, NOT yet dispatched): resolve every
   `[NEEDS VERIFICATION]` against primary sources; prior-art sweep
   (Fajgelbaum–Goldberg–Kennedy–Khandelwal QJE 2020, Amiti–Redding–
   Weinstein, Flaaen–Pierce, Bown/PIIE trackers, restricted LFTTD,
   EUROMOD/TAXSIM validation literature, law-as-code literature:
   Catala, OpenFisca, Merigoux et al.); check whether Yale's tracker
   methodology has been formally cited anywhere.
3. Writing = Fable only. Exemplar = the abstract (`drafts/abstract.md`,
   written). Full sections only after verification verdicts land.
4. Scoreboard numbers pin snapshot commits (cert-stack rule: committed
   reports refresh; quote pinned SHAs only).

## Honesty constraints carried into every draft

- Internal sol review is "independent adversarial cross-model review,"
  never "certification" — the non-self-certification boundary (notary
  pattern) is future work and the paper says so.
- Yale defect claims rest on the independent legal derivations (GN3(b)
  text; Proclamation 10339 staged table), filed upstream and
  unacknowledged as of 2026-08-07 — state exactly that.
- Estimation vs law boundary: statutory panel = deterministic law
  (Axiom); synthetic entries = estimation with a registered assumptions
  ledger (Microcosm). Metal shares / USMCA utilization / effective-rate
  constructs are out of scope and labeled as such.
- The agentic pipeline (AI encoders + adversarial cross-model review
  behind oracle gates) is stated plainly in methods.
- Policy-neutral: no advocacy; numbers speak.

## Naming (as of 2026-08-07)

"The Axiom Foundation" (never "nonprofit" in copy); Microcosm (repo
renamed from populace 8/7; packages still `populace.*` until
microcosm#638); Chronicle (renamed from Ledger 8/7 — schema ids still
`policyengine_ledger.*`, frozen v1); PolicyEngine. No Thesis mention.
Products capitalized in prose.

## Archival-release prerequisites exposed by revision round 6

These are named dependencies in their owning repositories, not work to perform
in this paper repository:

- **Disposition publication (`axiom-oracles`):** regenerate
  `dashboard/public/data/dispositions/us-tariff-panel.json` from the
  authoritative `dispositions/us-tariff-panel.yaml`, then add a synchronization
  tripwire that compares the source and mirror dates, entry counts, selector
  coverage, and per-concept footprints before publication.
- **Tariff composition (`rulespec-us` / Axiom side):** add a fail-closed guard
  for inputs outside the five declared witness lines and negative off-slice
  tests. Any application to synthetic entries must prefilter to the true
  five-line intersection until that guard lands, and its row, weight, and value
  counts must be committed as a receipt before they are reported.
- **Review reproducibility:** archive the exact component-review prompts,
  model/version/settings, per-round outputs, finding dispositions and
  adjudicator, and prospective stop/restart rules. Until then, round counts and
  final verdicts are development provenance, not a reproducible validation
  protocol.
- **Release package:** retain the existing containerized one-command rebuild
  and persistent-identifier gate. No archival release accompanies the current
  local draft.
