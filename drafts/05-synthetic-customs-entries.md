# 5. Synthetic customs entries from official margins

The statutory panel answers what the rate was. Applying it to trade
requires the other half: what crossed the border, at what value, in
which tariff line, from where. The public record answers this at the
margin — monthly totals by line, country, and district — while the
transaction-level record (the entry summaries importers actually file)
is either restricted to secure-enclave access or not assembled at all.
We release the bridge: weighted synthetic entry-line allocations
whose customs value reproduces the public margins exactly at a stated
grain, with every assumption below that grain declared. Three scopes
govern everything in this section and must not blur. The bulk ingest
preserves eighteen months of detail at line × country × country
subcode × entry district × unlading district × rate provision × month.
It separately publishes district-aggregated margins at line × country
× month. The entry generator uses that second record for a five-month,
all-line pilot at the same margin grain.

**Data records and relationships.** The artifact is a small relational
system, not a single flat file:

| Record | Observation or key | Relationship |
|---|---|---|
| `detail/period=YYYY-MM.parquet` | Published monthly detail keyed by HTS-10, Census country and subcode, entry and unlading districts, and rate provision | Preserves the source publication grain and all 22 monthly measures. |
| `margins_hts10_country_month.parquet` | One active cell per `(period, hts10, cty_code)` | Aggregates the detail over subcode, both districts, and rate provision; it is the generator input. |
| `district_entry_month.parquet` | Publisher control total by entry district and month | A separate reconciled district record, not a dimension of the margins-table key. |
| `synthetic_import_entries.parquet` | One weighted synthetic allocation row | Disaggregates each positive margins-table customs-value cell. |
| `assumptions.json`; `validation_report.json` | Dataset-level register and receipt | Authenticate the input publication, state assumptions, and record exact reaggregation. |

The synthetic table's fields are `entry_id`, `entry_date`, `period`,
`hts_number`, `hts10`, `chapter`, `country_of_origin`,
`census_country_code`, `customs_value`, `shipment_value`,
`is_postal_shipment`, `is_synthetic`, `weight`, and `size_stratum`.
The generator requires a unique `(period, hts10, cty_code)` input key
and emits rows only for positive customs-value cells; a zero cell has
no synthetic row. `weight` is the integer multiplicity represented by
the row, so weighted value is `weight × customs_value`, not an
unweighted transaction observation. Validation rejects a null in any
emitted field, a non-positive value or weight, unequal shipment and
customs values, a true postal flag, or a synthetic marker other than
true. These rules support exact reaggregation and weighted summaries
under the registered assumptions; they do not identify true transaction
counts or distributions.

**The margins, from the loading dock rather than the front door.**
Census publishes the complete monthly U.S. Imports of Merchandise
database as public archives — one ZIP per month, no authentication, at
a stable URL pattern. Eighteen archives (January 2025 through June
2026, ~3.3 GB, every byte sha-manifested at retrieval) parse under the
record layouts shipped inside the archives themselves into 38,841,305
detail rows: tariff line × partner country × country subcode × entry
district × unlading district × rate provision × month, with twenty-two monthly measures spanning customs value, dutiable
value, calculated duty, charges, quantities, and air/vessel/
containerized transport splits. The same archives carry the
publisher's own control-total files, which makes reconciliation an
internal affair: our parse must reproduce Census's own totals, in
integer dollars, on three independent axes — by country, by commodity,
by district. Across all eighteen months and every published measure,
it does, with zero tolerance and zero failures (Table 2 consolidates
the pipeline's validation results). The archives replace an API path we built first and demoted: the
equivalent extraction through the Census International Trade API took
thousands of calls and failed server-side on the largest chapters,
and the bulk files carry strictly more detail. The API survives as a
second delivery channel of the same producer — a check that detects
parsing and channel errors on either path, not errors common to the
source itself. A gated cross-check fetches a stratified sample
through it and compares cell for cell: 108,977 cells across sixteen
(line-prefix, country) strata, exact on all four dollar measures,
zero mismatches. The reconciliation against control totals is
likewise internal validity — the archive against its own publisher's
sums, monetary and quantity measures alike across the 22 commodity,
18 country, and 18 district measures — and we label both checks as
what they are.

**Down to entries, assumptions on the table.** The generator
disaggregates each (line × country × month) customs-value cell into
weighted synthetic entries by integer largest-remainder allocation:
entry counts and the within-cell size distribution fix each stratum's
target dollars, integer division allocates the floor, and the
remainder distributes one dollar at a time by largest fractional
part — so each stratum resolves to at most two weighted rows and the
allocation is integer arithmetic end-to-end, with the weights
carrying how many identical entries each row represents. The identity constraint is absolute:
weighted customs value reproduces every line-by-country-by-month cell
to the integer dollar. The arithmetic earns the word exact: cross-
cell aggregations run in arbitrary-precision Python integers (the
review of Section 6 caught and killed a fixed-width accumulation that
could wrap), cell values are validated at or below 2^53 so their
parquet representation is exactly representable, and the build
asserts the reproduction at run time rather than trusting the
construction. In the pilot window of February through June 2026, every
synthetic date (the fifteenth) is inside the composition's modeled
temporal window. Spatially, however, the generator is unrestricted: it
applies no HTS-line filter and includes every positive customs-value
cell in those months. Its 3,806,050 allocation rows carry 44,881,145
weighted entries and a weighted customs value of $1,467,109,590,515,
equal to the all-line window's margins total exactly. These are data-
construction totals, not results from applying the tariff composition;
this paper reports no composed rate over the pilot.

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
effect). Three fields have no public anchor at all — postal-shipment status,
sub-monthly timing, the shipment-value/customs-value distinction —
and each is set to a declared constant with a sensitivity note, not
imputed and forgotten. The timing constant deserves its own warning
because this paper's own Section 1 is the counterexample: every
allocation is dated mid-month, so nothing in this dataset can resolve
an intra-month legal boundary — the February 20 termination, the
February 24 collection cutoff, the July 24 seam. Analyses at those
boundaries need the margins plus the rule history, not these
allocations. Every row carries `is_synthetic = true`.

The honesty machinery extends to the anchors themselves. CBP's
statistics page mixes completed fiscal years with in-progress ones;
our parser emits in-progress years only as fiscal-year-to-date records
with explicit as-of endpoints, and it fails closed — wording it cannot
read, impossible calendar dates, notes displaced from their table,
endpoints later than the retrieval instant, all raise rather than
default. A fiscal year becomes an annual total only after its final
day has elapsed.

The result is not a substitute for the restricted transaction data,
and the paper does not offer it as one. Its intended uses are the
ones its contract supports: weighted synthetic allocation records
whose margins are exactly the official ones and whose departures from
the observable record are enumerated. Applying the statutory
composition requires first filtering to the five witness lines and
returns only a posted ad valorem component-rate stack. Complete duty or
revenue accounting additionally requires bases and state this dataset
does not supply.
