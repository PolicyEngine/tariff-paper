# Reproducibility index

This index collects the revisions and SHA-256 identifiers cited in the manuscript’s Data and code availability section.

| Project or artifact | Pinned revision or SHA-256 | What it reproduces or verifies |
|---|---|---|
| `rulespec-us` encoding | `dbf09f44eddd00b7ad5520f89371ebe8fdf0b7df` | Witness tariff composition and authority overlays consumed by this paper. |
| `axiom-rules-engine` | `ffd8213271947b0189a9dd61a055c1e0e78908a0` | Exact evaluation of the encoded rules. |
| `axiom-rules-engine` v0.1.0 binary | `674ca6e7…bbe32d7` | Identifies the engine binary cited by the manuscript; the manuscript records this SHA-256 in abbreviated form. |
| `axiom-oracles` reconciliation snapshot | `dc1da3af067c50fa7138458faf3703b4b9efd7cb` | The authoritative disposition evidence, comparison harness, conformance report, and corpus manifests. |
| Budget Lab at Yale tariff-rate tracker | `c4307e514196618afcbf88cf7fd33746417eeabf` | The reference tariff trajectory and built rate panel used in the tracker comparison. |
| Microcosm entries ingest | `d4b0855157af996bd367146bc200a2f72ee7d15d` | P1 source ingest, manifests, and reconciliation evidence for the synthetic-entry pipeline. |
| Microcosm entries generator | `6707ed5912d33ff0a340474a1a24f31546c6dec5` | Synthetic-entry generation from the ingested official monthly margins. |
| P2 validation receipt (`validation_report.json`) | `45276e944ff8cb6680e50ba27238d68a5b37da09b0d860db2ccfbd577ec5a03e` | Checks the local P2 validation receipt named in the availability limitation. |
| P2 assumptions register (`assumptions.json`) | `b3bcad3347d83c3ab9f9b937e1e6133ab002cb9432a2225e37a10e2c5f944a43` | Checks the local P2 assumptions register named in the availability limitation. |
| P2 synthetic entries (`synthetic_import_entries.parquet`) | `fbc64fd807eff3b2c43bfe88a39ccf5740be5a17786c1d110afd75c07c1d0972` | Checks the local P2 output named in the availability limitation. |
| PolicyEngine scorecard decomposition | `f9e7acf` | Section 2 tracker-decomposition leg outputs and their derivation annotation. |
| `rulespec-us` schedule spine | `f062088f` | The generated full-schedule rate tables and byte-comparison checks. |
| `rulespec-us` generated compositions | `747d54f5` | One hundred chapter compositions, tests, specifications, generator, and gate evidence. |
| `rulespec-us` action-incidence tables | `956a5474` | Action-family incidence tables and differential checks. |
| `rulespec-us` decoupled compositions | `96d5e7c1` | Decoupled compositions and the heading-9903.82.02 steel component. |

Abbreviated revisions and SHA-256 values are recorded exactly as cited by the manuscript. The availability section also identifies the full-schedule provisions feedstock as corpus version `2026-08-09-usitc-hts-2026-rev15-full-schedule`; it is a version identifier rather than a commit or SHA. The three P2 artifacts are local and uncommitted, as the manuscript deliberately states, so their hashes verify files when available but do not provide archival access.
