# 6. Provenance engineering

Every number in this paper is recomputable from public artifacts, and
the machinery that makes that true was built by AI agents. We state
both facts plainly because together they are the methods section: the
pipeline's outputs are only trustworthy because its architecture
assumes its authors — human or model — will err, and gates
accordingly.

**The gates.** Corpus documents enter under signed manifests; an
encoding cannot cite what the corpus does not hold. Every rule change
must compile, must carry proof atoms whose excerpts appear in the
cited document, and must pass companion tests that pin behavior at its
effective boundaries — the merge machinery refuses the change
otherwise. Panel derivations bind each row to a content digest and
rebuild byte-identically. Conformance reports pin the reference
commit, the engine build, and the encoding revision they were computed
from, and the scoreboard numbers quoted in this paper carry their
snapshot hashes because the live reports refresh as the encoding
grows.

**The adversary.** Every pull request merged in the repositories
this paper reports on passed same-project cross-model adversarial
QA — a reviewing agent from a different frontier model family (an
OpenAI GPT-5.6-class reviewer against Anthropic Claude-class
authoring agents) prompted to refute rather than confirm, with each finding closed by a
code change and a test that fails on the pre-fix implementation —
mutation-proven, not narrated. The entries pipeline of Section 5 is
the instructive case: its publication machinery (atomic directory
replacement with crash recovery) went through eight consecutive review
rounds, each finding a strictly narrower defect class than the last —
symlink-target validation before recursive deletion, a race in lock
takeover, asynchronous exceptions landing after a rename's commit
point, rename durability ordering under power loss — until the final
round found the structural invariant the piecewise fixes had been
approximating: no recovery marker may be removed until every mutation
it records is durable. The reviewer's last pass swept every marker-
removal site against that invariant, verified the closing test fails
on the previous implementation, and returned no findings. We report
the trajectory rather than just the endpoint because the trajectory is
the evidence: a review process that converges to zero by narrowing
finding classes is doing something different from one that runs out of
patience.

**The division of labor.** Model-written code, model-run reviews,
machine-checked gates — and human judgment exactly where it is load-
bearing: scope decisions (what counts as law versus estimation), the
disposition standard of Section 4, anything that leaves the project
(upstream reports, this paper), and the decision to ship. We do not
claim the review regime is external certification; Section 3 states
that boundary. We do claim the artifact trail is complete enough that
a skeptic need not trust any of it: the encodings, the corpus
manifests, the comparison harness, the entries pipeline, the review
verdicts, and the evidence packs (build reports, reconciliation
records, cross-check reports) are public, pinned, and re-runnable.

One synthesis sentence, scoped to what this project observed: the
gate-and-adversary architecture is what allowed agent speed — the
149-test battery, the per-change panel re-derivations, the twelve
review rounds — to accumulate as checked artifacts rather than as
unchecked claims.
