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
Run 2026-08-12, against the four final pages (index.html, how-discounting-works.html,
methodology.html, about.html), served via `python3 -m http.server` and checked with the
Claude Browser tooling.

**Console errors** — zero on all four pages. `read_console_messages` returned "No console
logs" on every page load.

**Color schemes** — both observed directly via viewport color-scheme emulation
(`resize_window` with `colorScheme: "dark"` / `"light"`), not just inferred from the CSS.
Dark (the default) and light were each loaded and screenshotted on at least one page
(methodology.html in dark, index.html and about.html in light); all rendered correctly —
correct backgrounds, text, link/accent colors, nav "current page" highlight. No pages were
screenshotted in both modes exhaustively, but the same shared `site.css` and `prefers-color-scheme`
block drive all four, so the two checked pages stand for the set.

**375px overflow** — `document.documentElement.scrollWidth` measured 375 on all four pages
at a 375px viewport (index 375, how-discounting-works 375, methodology 375, about 375). No
horizontal overflow on any page.

**External requests** — `read_network_requests` on every page showed only same-origin
requests (the page's own HTML + `assets/site.css`; localhost origin only). Static grep
confirms: `grep -rnE 'https?://' *.html | grep -v 'ftc.gov'` returned no output — the FTC
URL on about.html is the only `http(s)://` string in any of the four shipped pages. It is an
`<a href>` a reader clicks (verified in the source), not a resource the page loads.

**Scent-vocabulary sweep** — `grep -rinE "\b(accord|notes?|opens? with|dry.?down|sillage|projection|longevity|smell(s|ed|ing)?)\b" *.html`
on the four shipped pages returned exactly one hit: about.html's "Nothing at this project has
ever smelled anything" — the deliberate, intentional line about the project's own lack of
sensory apparatus, not a scent description. No fix needed.

**Contrast audit** — computed WCAG 2.x ratios from the literal hex values in `assets/site.css`
with a throwaway Python script (deleted after use). All ratios:

| Pair | Dark | Light |
|---|---|---|
| text/bg0 | 15.19:1 | 15.01:1 |
| text/bg1 | 14.22:1 | 16.06:1 |
| text2/bg0 | 7.15:1 | 6.57:1 |
| text2/bg1 | 6.70:1 | 7.03:1 |
| muted/bg1 (footer) | **3.90:1** | **4.19:1** |
| accent/bg0 | 8.31:1 | 5.18:1 |
| accent/bg1 | 7.78:1 | 5.54:1 |
| btn-label/accent | 8.31:1 | 5.63:1 |

All body-text pairs (text/bg0, text/bg1, text2/bg0, text2/bg1) clear 4.5:1 in both modes.
**Flag: `muted` (footer fine print and the small `.r-label` status tags) sits between 3:1 and
4.5:1 in both modes — 3.90:1 dark, 4.19:1 light.** It clears the 3:1 large-text floor but not
the 4.5:1 body-text floor, and the footer/`.r-label` text is small (0.9rem / 0.8rem), so this
is a real AA gap for that token, not a false alarm. Per the S6 spec this is flagged rather
than silently fixed since it's above 3:1; a follow-up should darken/lighten `--muted` a few
points (e.g. dark `#7D766C` → `#8D877D`-ish, light `#807A6F` → `#6E695F`-ish) to clear 4.5:1
before this copy is treated as load-bearing for accessibility compliance. This corrects the
S0 note's claim that "all 16 token pairs pass AA" — one does not, currently.

**Link check** — every internal `href` across the four pages (nav links, in-body cross-links,
`assets/favicon.svg`, `assets/site.css`, `#main` skip-link target) resolves to an existing
file or in-page id; confirmed by listing all `href="..."` values per page and checking each
against the filesystem/DOM. The one external link, the FTC citation on about.html, returned
HTTP 200 via `curl -s -o /dev/null -w "%{http_code}" -A "Mozilla/5.0"`.

**Claim-row count** — counted directly from the table above: index 4, how-discounting-works 6,
methodology 7, about 4. All four match the expected counts; no page is short.
