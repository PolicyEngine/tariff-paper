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
tariff-rate-tracker; our six upstream reports are public issues on
that repository. The Census source archives are public no-auth
downloads whose URL pattern, sizes, and sha-256 digests appear in the
committed source manifest; the CBP page bytes our anchors parse from
are archived beside the facts they ground.

Replication is therefore not a package assembled for this paper but
the working state of the projects it reports on: re-running the
conformance derivation at the pinned revisions reproduces the
scoreboard; re-running the entries build against the manifested
archives reproduces the artifacts byte-for-byte, a property the review
regime enforced rather than aspired to.
