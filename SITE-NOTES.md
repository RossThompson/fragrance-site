# SITE-NOTES — claims → basis

Site: PriceOnRecord (priceonrecord.com). Static, self-contained; no external requests;
system fonts; dark default + light via prefers-color-scheme; skip-link; AA contrast both
modes; no horizontal overflow at 375px.

## Decisions (S0 gate, 2026-08-12)
- Name/domain: PriceOnRecord / priceonrecord.com (DNS checked free 2026-08-12; scentledger.com
  was found taken by an existing perfume-review site and abandoned).
- Visual direction: A "Amber" (warm near-black, amber accent). All 16 token pairs pass AA;
  ratios recorded in the S6 verification section when run against final pages.
- About page: named — run by Ross Thompson.

## Standing rules (from the design spec)
No scent descriptions of any kind. No claimed measurements — zero price observations exist;
baseline behaviour is described in future/conditional tense and the site says collection has
not started. No fabricated social proof. FTC disclosure present before any affiliate link
exists. The commission conflict is disclosed. Every factual claim on every page gets a row
below: a fetched source (URL + fetch date) or an R label (reasoning, written as reasoning).

## Claim → basis
| Claim | Page | Basis |
|---|---|---|
| "60–80% off nearly everything, nearly always" | index | R — characterisation of the discounter category, checkable by inspecting any major discount site's listing grid; written as characterisation |
| "a retail price almost nobody charges" | index | R — reasoning about list-price economics; written as reasoning |
| the two qualifying paths + 90-day/3-week framing | index | internal — bot spec §7 (private repo); described qualitatively by design |
| "collection has not started" + feed-only sourcing | index | fact, dated 2026-08-12 |
| list prices function as anchors, rarely charged | how-discounting-works | R — reasoning about reference pricing; written as reasoning |
| permanent-sale effect | how-discounting-works | R — conditional reasoning ("if nearly every listing…") |
| grey market: real savings, traded warranty/recourse | how-discounting-works | R — hedged; general knowledge of parallel-import trade-offs, no specific brand policy cited |
| testers/unboxed cheaper, distinct products | how-discounting-works | R |
| batch codes: production date, not authenticity | how-discounting-works | R |
| affiliate cookies: reader price unchanged, commission earned, windows vary | how-discounting-works | R — program-specific figures deliberately omitted as unverified |
| watchlist/daily/append-only recording design | methodology | internal — bot pipeline (private repo), described accurately |
| four baseline rules + reasons | methodology | internal — bot pipeline; each rule exists in tested code |
| pooled-median worked example ($219/$260/~$240) | methodology | arithmetic; mirrors a real bug found and fixed in our design |
| two qualifying paths, qualitative | methodology | internal — bot pipeline; constants withheld deliberately |
| history-bounded claims ("N days we've tracked") | methodology | internal — the copy generator derives claims from the record |
| zero observations, feed-only sourcing | methodology | fact, dated 2026-08-12 |
| commission conflict + qualification blind to it | methodology | internal — link selection vs qualification are separate stages |
| affiliate disclosure wording + FTC citation | about | FTC's Endorsement Guides: What People Are Asking — https://www.ftc.gov/business-guidance/resources/ftcs-endorsement-guides-what-people-are-asking — WebFetch tool returned HTTP 403 on first attempt; confirmed live via curl (HTTP 200, title verified) 2026-08-12 |
| commission conflict statement | about | internal — link selection vs qualification are separate pipeline stages |
| "no scent reviews" and the reason | about | fact — this project has no sensory apparatus; stated as such |
| named operation, contact address | about | fact — S0 gate decision |

## Verification
(filled by S6)
