---
tags: [signal, content, freshness, recency, update, high-confidence]
cargo: [seo-specialist, writer]
confidence: high
category: Content
subcategory: Recency
last_updated: 2026-04-23
---
# Content — Freshness

A measure of how recent and up-to-date the content is. The weight of freshness varies dramatically by query type. For news searches (query deserves freshness — QDF), content that is hours old can outrank content a year old. For how-tos and evergreen content, year-old content may still rank well if it covers the topic completely. For product reviews, launches, trends — freshness matters moderately. For encyclopedic or historical content — freshness is minimally relevant.

The leak exposes fields like `recency`, `contentAge`, `lastSignificantUpdate`, and `freshnessEncodedSignals` that capture multiple dimensions of currency. Google does not just measure "publication date." It measures the date of significant updates, frequency of changes, and editing patterns (a "living" document that evolves continuously vs. a static snapshot).

## In the Leak

The `recency: String.t()` field captures a measure of how recent the content is. `contentAge: String.t()` records time since original publication. `lastSignificantUpdate: timestamp` marks the last time the content was materially updated (not just a typo correction). `freshnessEncodedSignals` is a compressed package with aggregated freshness signals.

The leak documents **three distinct date types** that Google uses to determine content age — each serving a different purpose: *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

- **`bylineDate`** — the date stated by the author/publisher (from the byline or `datePublished` schema)
- **`syntacticDate`** — the date extracted syntactically from the URL or HTML structure (e.g., `/2025/04/article`)
- **`semanticDate`** — the date inferred semantically from the content itself (e.g., references to recent events, mentions of current technology)

Google cross-references these three signals. If a bylineDate says 2025 but the content only references events from 2022, the semantic date is used as a freshness override. This is why backdating content or putting a current year in a title without updating the body is detectable.

## Confidence: High

Explicitly documented with multiple fields, confirmed in public search behavior (QDF explicitly confirmed by Google), and corroborated by traffic data showing that annually updated pages gain an average of 4.6 positions vs. non-updated pages.

## How It Works

Google extracts publication dates from multiple sources: the `article:published_time` meta tag (if present), the URL (sometimes the date is in the slug), `lastmod` in the XML sitemap, and semantic analysis of the text itself ("The 2022 article refers to the sitting president; it is now 2026, so it is outdated").

For news, Google uses QDF (Query Deserves Freshness), which automatically boosts very recent content. For how-tos, annual updates are sufficient. For encyclopedias (e.g., "History of Ancient Greece"), freshness is practically irrelevant.

The key metric is not "publication date," but "date of last significant update." An article published in 2020 that was updated in January 2025 with new data is fresher than one published in December 2024 that has never been reviewed.

Freshness is applied as a **Twiddler** — a post-Ascorer re-ranking function called `FreshnessTwiddler`. This means freshness can adjust a page's position *after* the primary Ascorer ranking has run, not as a base signal. The practical implication: for queries where QDF applies, a freshly published or updated page can leapfrog a higher-PageRank competitor even without strong authority. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## How to Measure on Your Site

Google Search Console does not directly disclose freshness scores. But there are proxies:

- **Google Analytics:** Segment traffic by publication date (filter by articlePublishedDate if using schema). See: do 2025 articles get more traffic than 2023 ones?
- **Search Console:** Average position on queries where freshness matters (news, trends, "best 2025"). Do recent articles rank better?
- **Sitemap lastmod:** Check whether lastmod is updated. Google trusts the sitemap for freshness
- **Schema dateModified:** Check if it is being rendered correctly in the HTML (view via Inspect Element)

Track: in the last quarter, what % of your traffic came from articles published/updated in the last 3 months?

## What to Do

**Baseline:** Identify articles in the top 10 results for your keywords that have > 2 years without an update. You don't need to rewrite from scratch. Add a section "Updated in 2025 with..." with new data, examples, or links to more recent articles. This signals to Google that the content has been reviewed.

**By query type:**

For news and trends (e.g., "best smartphones 2025," "2026 elections"), weekly updates are ideal. News articles that don't change in 1 week start losing position.

For how-tos and guides (e.g., "how to optimize site for Core Web Vitals"), annual updates are the minimum. Refresh annually with new data, corrected links, and examples.

For deep analyses and tutorials (e.g., "complete CSS guide"), an update every 2-3 years is acceptable. But add a visible "last updated" notice.

**Technical implementation:** Use `datePublished` and `dateModified` schema on each article. Update `dateModified` whenever you make a material change. Adding a visible "Updated on [date]" in the article also affects CTR — users trust visibly recent content more.

**Common mistake:** Don't confuse "we have to update everything monthly" with "evergreen content doesn't need updating." An article about "the history of digital marketing" from 2018 that was never touched may still rank well. An article about "best SEO tools 2024" published in January 2024 that doesn't mention tools that emerged in 2025 is stale.

## Official Reference

[Managing Crawl Budget for Large Sites](https://developers.google.com/search/docs/crawling-indexing/large-site-managing-crawl-budget) — Google Search Central: Google explains how crawl frequency and content updates influence how Googlebot discovers new and updated pages on your site.

## See Also

[[Content - Query Coverage]] — Updating is a chance to improve topic coverage  
[[Engagement - Navboost and Clicks]] — Fresh content gets more clicks when relevant  
[[Content - Title Matching]] — Add the year to the title for trend queries
