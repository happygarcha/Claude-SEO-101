# SEO Audit: drapewell.myshopify.com (2026-11-12)

**Scope:** homepage, one product page (/products/terrazzo-shower-curtain), robots.txt, sitemap index, product sitemap. This is a sample, not a 500-page crawl.
**Business type:** E-commerce (Shopify, home/outdoor/pet/desk/fashion, Surrey BC, ships CA/US).
**Estimated health score: ~72/100** (partial data, see Limitations).

## What works
- Homepage 200, single H1, unique title (47 chars) and meta description, canonical, viewport, full OG tags, `lang`/locale set.
- robots.txt is Shopify's sensible default: blocks cart/checkout/account/sort and filter facets, lists sitemaps.
- Sitemap index live and complete: 145 product URLs, plus collections, pages and an agentic-discovery sitemap.
- Product page has a keyworded title, descriptive meta, H1, Product + ProductGroup + BreadcrumbList + Organization JSON-LD, brand and SKU.
- Agent readiness is strong: `llms.txt`, `agents.md`, UCP discovery (`/.well-known/ucp`) all return 200.
- Real 404 status for missing URLs (no soft 404s). No images missing the alt attribute.

## Findings
| # | Severity | Finding | Fix |
|---|----------|---------|-----|
| 1 | High | **Indexing domain is `*.myshopify.com`.** Canonicals, OG and schema all point at the myshopify subdomain. No custom domain was seen, which limits brand trust and long-term ranking equity. | Connect a custom domain, make it primary, and let Shopify redirect myshopify to it. |
| 2 | High | **Heavy pages.** Homepage HTML is ~348 KB with 76 script tags (28 external); product page HTML is ~734 KB. Several app scripts (wishlist, trust badges) load site-wide. Likely hurts LCP/INP on mobile. | Remove or defer unused apps, trim inline JSON, lazy-load below-the-fold sections. Measure with PageSpeed (see Limitations). |
| 3 | Medium | **Duplicate Organization/WebSite JSON-LD on the homepage** (emitted twice). | Remove the duplicate block from the theme or the schema app. |
| 4 | Medium | **Homepage schema is thin.** No SearchAction or sameAs social profiles; no ItemList for featured products. | Add `sameAs` and a SearchAction to WebSite. |
| 5 | Medium | **Product schema has no aggregateRating/review.** Observed no review data in markup. | Add a reviews app that outputs rating markup, once real reviews exist. |
| 6 | Medium | **Hero headings use H2 for product names while the real H1 sits lower** in "Home decor and everyday finds…" intro. | Make the first visible heading the H1, or move the intro up. |
| 7 | Low | 50 of 71 homepage images have `alt=""`. Fine for decorative images but verify product/category cards carry descriptive alt. | Audit card images and add alt text. |
| 8 | Low | Product SKUs look like supplier codes (`CJYD…`). No GTIN/MPN seen. | Add GTIN/MPN where available for Shopping eligibility. |
| 9 | Low | Product title H1 and title tag differ in style (H1 contains em dash and long spec list). | Keep H1 concise; keep spec detail in the body. |
| 10 | Info | Homepage is localized by cookie (`localization=CA`, CAD). No hreflang. | Only needed if separate CA/US URLs are introduced. |

## Limitations
- PageSpeed Insights was unreachable from this sandbox (404 via the proxy), so no CWV or Lighthouse numbers; finding 2 is from page weight and script counts only.
- Search Console is connected as a restricted user and the performance query returned no usable data, so no clicks, impressions or index coverage figures.
- No screenshots, backlink, Moz or DataForSEO data. Only 2 pages were fetched.
- The score is an estimate from the sampled signals, not the full weighted rubric.
