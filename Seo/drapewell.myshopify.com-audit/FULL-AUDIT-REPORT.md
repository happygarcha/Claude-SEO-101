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

---
# Addendum: full sitemap crawl (2026-11-12)
Crawled all 186 sitemap URLs (144 products, 23 collections, 16 pages, 2 blog URLs, home).

| Check | Result |
|---|---|
| HTTP status | 184 x 200, **2 x 404** |
| Duplicate titles / meta descriptions | none |
| Missing meta description | 3 (`/pages/reviews` plus the 2 blog 404s) |
| Titles over 60 chars | **43** (all products; avg product title 58 chars, so many truncate in SERPs) |
| Meta descriptions over 160 chars | 7 (incl. homepage) |
| Meta description under 70 chars | 1 (`/collections/fresh-this-week`) |
| Pages without exactly one H1 | 2 (the blog 404s) |
| noindex pages | 0 |
| Canonical mismatch | 1 (`/products/micro-grill-egg-mate%E2%84%A2-...`, URL-encoded trademark symbol) |
| Product pages with Product schema | 144 of 144, none with aggregateRating |
| Image missing alt attribute | 1 page (`carbon-steel-nail-clipper...`) |
| HTML size | avg ~339 KB; largest 1.07 MB (`geometric-shower-curtain`, `botanical-coastal-boho-peva-shower-curtain` ~1.07 MB, `terrazzo-shower-curtain` ~725 KB) |

## New findings
- **High: sitemap lists a blog that returns 404.** `/blogs/seo-news` and its one article are in the sitemap but 404 (likely unpublished or hidden). Remove it from the sitemap by republishing/deleting the blog, or restore it. Wasted crawl budget and a "submitted URL not found" signal.
- **Medium: 43 product titles exceed 60 chars.** Shorten to about 55-60, leading with the product type and key attribute.
- **Medium: shower-curtain product pages are up to 1.07 MB of HTML.** Likely variant JSON for many sizes/colours. Heavy for mobile parsing; consider trimming variant data or app output.
- **Low: 7 long meta descriptions, 1 short, 1 missing** on `/pages/reviews`.
- **Low: canonical differs on the egg-cooker product** (encoded ™ in the handle). Shorten the handle to plain ASCII and add a redirect.
- **Positive:** unique titles and descriptions across 184 live pages, 100% product schema coverage, solid content pages (size guides, shipping and refund policies, FAQ) supporting E-E-A-T.

---
# Addendum 2: AI search / agent readiness
- `llms.txt` present and descriptive (brand, market, currency, product themes). **Low risk note:** it publishes a personal-looking contact email (hotmail address). Consider a role address such as support@ on your own domain.
- `/.well-known/ucp` returns 200 and `robots.txt` points to the UCP/MCP endpoint and `agents.md`: strong agentic-commerce readiness. WebMCP hooks are present in the homepage.
- No `/.well-known/ai-catalog.json` (404). Optional, low priority.
- No AI-bot-specific rules in robots.txt (GPTBot, ClaudeBot, PerplexityBot, Google-Extended all fall under `User-agent: *`, which allows them). Decide deliberately whether to allow AI crawlers.
- Markdown delivery via `Accept: text/markdown` not supported. Optional.
- Homepage has no `og:image:alt`, and no `rel="icon"` was found in the HTML (check the favicon in theme settings).
- GEO: strong content pages (size guides, materials, FAQ, policies) are good citation candidates; add concise definition-style paragraphs and sourced specs to product pages to improve citability.

## Consolidated priorities
1. High: custom domain; fix or remove the 404 blog from the sitemap; cut script/variant weight on shower-curtain pages.
2. Medium: shorten 43 product titles; dedupe homepage Organization/WebSite JSON-LD; fix homepage heading order; add review markup when available.
3. Low: meta description lengths, favicon and og:image:alt, GTIN/MPN, role-based contact email.
