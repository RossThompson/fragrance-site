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

## Verification
(filled by S6)
