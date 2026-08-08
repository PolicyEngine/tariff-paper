# Data and code availability

Everything this paper reports predates it in public. The encodings
live in the rulespec-us repository (the tariff composition and its
authority overlays, with mandatory companion tests); the corpus
manifests, comparison harness, conformance reports, and disposition
records in axiom-oracles, with the quoted scoreboard pinned at
snapshot dc1da3af; the entries pipeline, its 149-test battery, and the
committed evidence packs (build report, source manifest, eighteen
per-month reconciliation records, the gated cross-check report) in the
Microcosm repository, merged as pull requests #620 and #621 with the
full adversarial review inventories in their descriptions. The Yale
reference is pinned at commit c4307e51 of Budget-Lab-Yale/
tariff-rate-tracker; our six upstream filings — five public issues and one patch pull
request — are on that repository. The Census source archives are public no-auth
downloads whose URL pattern, sizes, and sha-256 digests appear in the
committed source manifest; the CBP page bytes our anchors parse from
are archived beside the facts they ground.

Replication is therefore not a package assembled for this paper but
the working state of the projects it reports on: re-running the
conformance derivation at the pinned revisions reproduces the
scoreboard; re-running the entries build against the manifested
archives reproduces the artifacts byte-for-byte, a property the review
regime enforced rather than aspired to.

**Pinned revisions.** Encoding: rulespec-us
`dbf09f44eddd00b7ad5520f89371ebe8fdf0b7df`. Engine:
axiom-rules-engine `ffd8213271947b0189a9dd61a055c1e0e78908a0`
(v0.1.0; binary sha-256 `674ca6e7…bbe32d7`). Reconciliation snapshot:
axiom-oracles `dc1da3af067c50fa7138458faf3703b4b9efd7cb`. Reference:
Budget-Lab-Yale/tariff-rate-tracker
`c4307e514196618afcbf88cf7fd33746417eeabf` (MIT). Entries pipeline:
microcosm merge commits `d4b0855157af996bd367146bc200a2f72ee7d15d`
(ingest) and `6707ed5912d33ff0a340474a1a24f31546c6dec5` (generator).
An archival release with containerized one-command replication and a
persistent identifier accompanies submission; until then the commits
above are the replication interface.

**AI-use disclosure.** The encodings, pipelines, tests, and reviews
described in Section 6 were produced by AI agents under the stated
gates, with human direction of scope, dispositions, upstream
communication, and publication. This manuscript was drafted by the
authoring agents from a primary-source-verified fact base; its
revision record to date comprises one cross-model hostile-referee
round (GPT-5.6-class) whose twenty findings were addressed, followed
by same-family verification rounds (a round-diff audit of those
closures and a fresh red-team pass, Claude-class) whose findings this
version incorporates. The human author is responsible for all
claims.
