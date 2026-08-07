# 5. Synthetic customs entries from official margins

The statutory panel answers what the rate was. Applying it to trade
requires the other half: what crossed the border, at what value, in
which tariff line, from where. The public record answers this at the
margin — monthly totals by line, country, and district — while the
transaction-level record (the entry summaries importers actually file)
is either restricted to secure-enclave access or not assembled at all.
We release the bridge: a synthetic transaction-level dataset that
reproduces the public margins exactly and declares every assumption it
adds on the way down to entry grain.

**The margins, from the loading dock rather than the front door.**
Census publishes the complete monthly U.S. Imports of Merchandise
database as public archives — one ZIP per month, no authentication, at
a stable URL pattern. Eighteen archives (January 2025 through June
2026, ~3.3 GB, every byte sha-manifested at retrieval) parse under the
record layouts shipped inside the archives themselves into 38,841,305
detail rows: tariff line × partner country × customs district × month,
with twenty-two monthly measures spanning customs value, dutiable
value, calculated duty, charges, quantities, and air/vessel/
containerized transport splits. The same archives carry the
publisher's own control-total files, which makes reconciliation an
internal affair: our parse must reproduce Census's own totals, in
integer dollars, on three independent axes — by country, by commodity,
by district. Across all eighteen months and every published measure,
it does, with zero tolerance and zero failures. The archives replace
an API path we built first and demoted: the equivalent extraction
through the Census International Trade API took thousands of calls and
failed server-side on the largest chapters, and the bulk files carry
strictly more detail. The API survives as something better than a
primary source — an independent second channel. A gated cross-check
fetches a stratified sample through the API and compares cell for
cell: 108,977 cells, exact on all four dollar measures, zero
mismatches. Two official channels agreeing is stronger provenance
than either alone.

**Down to entries, assumptions on the table.** The generator
disaggregates each (line × country × month) customs-value cell into
weighted synthetic entries. The identity constraint is absolute:
weighted customs value reproduces every cell to the integer dollar, on
an enforced domain (cell values at or below 2^53, where integer
arithmetic is exact; the build asserts the reproduction at run time
rather than trusting the construction). In the pilot window of
February through June 2026 — chosen to sit inside the composed
statutory spine's domain — 3,806,050 entry rows carry 44,881,145
weighted entries and a weighted customs value of $1,467,109,590,515,
equal to the window's margins total exactly.

What the margins do not determine, the dataset does not pretend to
know. An assumptions register ships beside the data, and its entries
are calibrated where an anchor exists and labeled where one does not:
entry counts derive from Customs and Border Protection's published
fiscal-year-to-date mean entry value, with the coverage window
(October 1, 2025 through July 27, 2026) carried explicitly rather than
laundered into an annual figure; within-cell entry sizes are
lognormal, with σ = 2.6916 solved so that the share of entries at or
under $2,500 matches CBP's published informal-entry share — labeled a
proxy moment, because the regulatory informal-entry categories map
imperfectly onto a value threshold, and the residual gap is registered
(achieved share within 2.6 × 10⁻⁵ of target; achieved mean $32,689
against a $32,916 anchor, the difference a documented small-cell floor
effect). Three fields have no public anchor at all — postal-shipment
status, sub-monthly timing, the shipment-value/customs-value
distinction — and each is set to a declared constant with a
sensitivity note, not imputed and forgotten. Every row carries
`is_synthetic = true`.

The honesty machinery extends to the anchors themselves. CBP's
statistics page mixes completed fiscal years with in-progress ones;
our parser emits in-progress years only as fiscal-year-to-date records
with explicit as-of endpoints, and it fails closed — wording it cannot
read, impossible calendar dates, notes displaced from their table,
endpoints later than the retrieval instant, all raise rather than
default. A fiscal year becomes an annual total only after its final
day has elapsed.

The result is not a substitute for the restricted transaction data,
and the paper does not offer it as one. It is the dataset that
downstream tariff microsimulation actually needs: entry-grain records
whose margins are exactly the official ones, whose every departure
from the observable record is enumerated, and whose fields conform to
the statutory spine's input contract — so that the panel of Section 3
and these entries compose into duty computation at the grain where
duties are assessed.
