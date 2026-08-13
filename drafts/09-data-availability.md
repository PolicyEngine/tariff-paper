# Data and code availability

The committed replication surface is distributed across the source
projects. The rulespec-us repository contains the tariff composition,
authority overlays, and companion tests. Axiom-oracles contains the
corpus manifests, comparison harness, conformance report, and the
authoritative disposition source. Microcosm contains the entries code
and the P1 evidence pack: build report, source manifest, eighteen
monthly reconciliation records, and gated cross-check report. The Yale
reference is pinned at commit `c4307e51`. Census archive URLs, sizes,
and sha-256 digests are in the P1 source manifest, and the CBP page bytes
are archived beside the facts they ground.

Three limitations prevent an archival-replication claim for this draft:

1. The authoritative disposition evidence is
   `axiom-oracles@dc1da3af067c50fa7138458faf3703b4b9efd7cb:dispositions/us-tariff-panel.yaml`,
   dated 2026-08-03: 30 entries and an MFN footprint of 594. The public
   mirror has 46 entries and an MFN footprint of 462; its file is
   `dashboard/public/data/dispositions/us-tariff-panel.json` at that same
   pin, and it is stale, dated 2026-08-02. It is not evidence for this
   paper's disposition claims and must
   be regenerated from the authoritative source under a synchronization
   tripwire before archival release.
2. The P2 validation receipt and outputs are currently local rather
   than committed. Their sha-256 values are
   `45276e944ff8cb6680e50ba27238d68a5b37da09b0d860db2ccfbd577ec5a03e`
   (`validation_report.json`),
   `b3bcad3347d83c3ab9f9b937e1e6133ab002cb9432a2225e37a10e2c5f944a43`
   (`assumptions.json`), and
   `fbc64fd807eff3b2c43bfe88a39ccf5740be5a17786c1d110afd75c07c1d0972`
   (`synthetic_import_entries.parquet`). They must enter the archival
   package before its release.
3. Exact component-review prompts, model versions and settings,
   adjudication records, and prospective stop/restart rules are not
   preserved. Review-round counts remain development provenance until
   that protocol is archived.

The committed pins reproduce the comparison and P1 receipts. The local
P2 hashes make the present outputs checkable on this machine but do not
replace publication of those artifacts.

**Pinned revisions.** Encoding: rulespec-us
`dbf09f44eddd00b7ad5520f89371ebe8fdf0b7df`. Engine:
axiom-rules-engine `ffd8213271947b0189a9dd61a055c1e0e78908a0`
(v0.1.0; binary sha-256 `674ca6e7…bbe32d7`). Reconciliation snapshot:
axiom-oracles `dc1da3af067c50fa7138458faf3703b4b9efd7cb`. Reference:
Budget-Lab-Yale/tariff-rate-tracker
`c4307e514196618afcbf88cf7fd33746417eeabf` (MIT). Entries pipeline:
microcosm merge commits `d4b0855157af996bd367146bc200a2f72ee7d15d`
(ingest) and `6707ed5912d33ff0a340474a1a24f31546c6dec5` (generator).
No archival release accompanies this local draft. Before release, the
project must also add the fail-closed five-line composition guard and
negative tests, regenerate and tripwire the disposition mirror, archive
the P2 outputs and review protocol, and retain the planned containerized
one-command rebuild and persistent identifier.

The Section 4 decomposition's leg outputs are committed in the public
scorecard repository [@scorecard_repo] at `f9e7acf` under
`data/pe/diagnostics/`, with the derivation annotation under
`sources/`; the weight bases with hash receipts, the 2025 recipe-build
log, the Census archive manifest chain, and the statistical-membership
map live in the project lane pending the archival release. The Section 7 generated schedule ships in the rules repository under
`us/policies/usitc/us-tariff-duty/lines/generated/` at merge
`f062088f`, with its reproducer
(`tools/generate_hts_rate_tables.py`), whose check mode re-derives and
byte-compares all 200 committed files. The full-schedule provisions
feedstock is corpus version
`2026-08-09-usitc-hts-2026-rev15-full-schedule`.

**AI-use disclosure.** The encodings, pipelines, tests, and reviews
described in Section 7 were produced by AI agents under the stated
gates, with human direction of scope, dispositions, upstream
communication, and publication. This manuscript was drafted by the
authoring agents from a primary-source-verified fact base and revised
through hostile, round-diff, red-team, and fresh-eyes referee passes.
The component-review reproducibility limit above applies; manuscript
review cannot substitute for the pinned artifacts and checks reported
with each claim. The human author is responsible for all claims.
