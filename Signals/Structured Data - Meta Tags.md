---
tags: [signal, structured-data, meta-tags, high-confidence]
cargo: [developer, seo-specialist]
confidence: high
category: Structured Data
last_updated: 2026-04-23
---
# Structured Data — Meta Tags

HTML instructions that inform Google about your page. Meta tags are not a direct ranking factor (Google does not rank for "having a meta description"), but they affect ranking indirectly: meta description affects CTR on the SERP (more clicks = Navboost), canonical affects which version is ranked, robots affects indexing.

The leak exposes that Google processes meta tags through specialized modules: Alexandria (semantic analysis of meta descriptions), Mustang (metadata classification), and systems that parse robots directives. WWWDocInfo stores meta tags as hard-coded boolean attributes of the document in the index.

## In the Leak

Meta tags do not appear as named rankable fields ("metaDescriptionScore"), but appear as part of document parsing. Canonical tag is explicitly processed to consolidate duplicate versions. Robots meta tag determines boolean flags in the index.

**WWWDocInfo** is a documented structure in the leak that stores meta tags as hard-coded **boolean attributes** of the document in the index. This means meta directives (noindex, follow, canonical) are not re-evaluated at serving time — they are baked into the indexed representation of the document. Changing a robots meta tag only takes effect after Googlebot re-crawls and re-indexes the page. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

**Alexandria** (semantic analysis) and **Mustang** (metadata classification) both process meta tag content. Alexandria analyzes meta descriptions for semantic relevance to the page topic. If the meta description is unrelated to the page content, Alexandria may override it with a dynamically generated snippet for a given query. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: High

Explicit processing documented, public Google confirmation about canonical use, and obvious logic — Googlebot needs instructions about how to treat a page.

## How It Works

When Googlebot crawls a page, it extracts all meta tags from the `<head>`. For each tag, it takes the corresponding action: `meta name="robots" content="noindex"` sets the noindex flag; `<link rel="canonical" href="...">` marks the page as duplicate pointing to the canonical; `meta name="description" content="..."` is used to generate the snippet on the SERP.

Meta description does not affect ranking, but affects CTR. A descriptive and relevant snippet with keywords increases the chance of a click. Low CTR in positions 3-5 may be a symptom of a weak meta description.

Canonical is critical for technical SEO. Without canonical on duplicate pages, Google picks which to rank (often the wrong one). With canonical pointing to the preferred version, all equity is consolidated there.

Robots meta affects indexing decisions. `noindex` removes from the index. `follow` allows link crawling. `nofollow` blocks. These are not ranking factors, but determine whether a page is ranked.

## How to Measure on Your Site

**Meta descriptions:**

- Google Search Console: "Performance" tab shows whether Google uses your meta description or rewrites it. A high % of rewrites = your descriptions are weak
- Manual audit: search "intitle:your_keyword" and compare your descriptions with the top 3. More descriptive/with keywords? Less generic?

**Canonical:**

- Screaming Frog or Ahrefs crawl your site and report canonical issues (chained canonicals, self-referential, conflicting)
- Search Console: index coverage shows "Excluded by User-selected Canonical" if canonical was implemented

**Robots meta:**

- Screaming Frog: filter by noindex pages and check if they are intentional
- Search Console: "Excluded" in index coverage shows pages Google chose not to index

## What to Do

**Meta descriptions:**

Each page deserves a unique description of 150-160 characters. It should include the main keyword if possible, but without forced reading. Useful structure: "[Content description]: [Benefit/differentiator]." Example: "Complete SEO guide 2025: proven techniques to increase organic traffic — updated with recent data."

Google sometimes rewrites descriptions with "..." — there is nothing you can do. Prioritize pages in positions 3-5 that have low CTR.

**Canonical:**

If you have duplicates (URL parameters, http vs. https, www vs. non-www, printer-friendly versions), implement canonical pointing to the preferred version. Tool: Screaming Frog detects where it's missing. Fix with `<link rel="canonical" href="https://example.com/preferred-version">`.

Common mistake: canonical to a different subdomain. It works, but consolidating to one domain is better.

**Robots meta:**

Not needed for 99% of pages (default is index, follow). Use only for: test pages, staging pages, non-relevant filters/parameters. If a page should be indexed, leave it without a robots meta (or explicit index, follow — both work).

**Open Graph (for social sharing):**

Meta tags `og:title`, `og:description`, `og:image`. They affect how an article appears on Facebook, LinkedIn, Twitter. Not a ranking factor, but affects CTR in social. Tool: Facebook Sharing Debugger validates implementation.

## Official Reference

[Snippets and Featured Snippets](https://developers.google.com/search/docs/appearance/snippet) — Google Search Central: Google explains how meta descriptions and content are used to generate snippets in search results, and how to optimize them to improve clicks.

## See Also

[[Content - Title Matching]] — Title and description work together on the SERP  
[[Structured Data - Schema]] — Schema is more powerful than meta tags  
[[Engagement - Navboost and Clicks]] — Meta description affects CTR which feeds Navboost
