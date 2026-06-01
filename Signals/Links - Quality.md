---
tags: [signal, link, quality, spam, detection, high-confidence]
cargo: [seo-specialist, link-builder]
confidence: high
category: Links
last_updated: 2026-04-23
---
# Links — Quality

Assessment of the quality of who links to you, not just quantity. Google detects spam backlinks, PBNs, bought links. The leak exposes fields like `badBacklinks` and detection of suspicious anchor patterns. A link from a trustworthy site with a clean history is worth 10x more than a link from an obscure site with a pattern of link selling.

Importance: 10 quality links outperform 1,000 spam links. Google penalizes sites with an excess of low-quality or bought-detected links.

## In the Leak

Fields `badBacklinks: integer()`, detection of suspicious anchor patterns, analysis of the linking site's context.

**`sourceType`** is a field documented in the leak that records the relationship between where a page is indexed (its tier in Google's indexing hierarchy) and the link value it can transfer. Pages indexed in lower tiers (TeraGoogle — cold storage equivalent) pass less effective link equity than pages indexed in the primary index (Alexandria). *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

This means a link from a frequently crawled, highly visible page in Google's primary index is structurally more valuable than a link from a page that Google has deprioritized to secondary storage — even if both pages have similar surface-level domain authority metrics.

The **`freshdocs` link value multiplier** is documented in the leak. Links from **newer webpages** receive a value multiplier compared to links inserted into older existing content ("niche edits"). This challenges the conventional wisdom that niche edits are valuable primarily because of the age of the page — the SEL analysis clarifies that it is traffic or internal links to that older page that create value, not its age itself. A new page with strong internal link support may pass link equity more efficiently than an old, forgotten page. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

Related to this: Google maintains a **version memory of every URL** (up to the last 20 versions). Historical versions are associated with weights and scores. Theoretically, by updating a page and waiting for 20 crawl cycles with significant changes, old negative scoring versions can be displaced from this window. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

## Confidence: High

Explicit fields, public confirmation of link spam penalties (Penguin update), empirical validation.

## How It Works

Google analyzes the source site: history (is it new or established?), content type (relevant or spam farm?), linking patterns (sells links or organic links?), presence of ads/monetization.

A site with a clean history, quality content, few outbound links = quality link. A new site, thin content, hundreds of links to various sites = spam.

Anchor text also matters: natural variation = good. Repeated exact match = suspicious.

## What to Do

**Backlink audit:** Ahrefs/SEMrush show Domain Rating, source domain. Links from DR < 10 are low-quality, DR 20-40 are medium, DR 50+ are high-quality.

**Remove bad links:** If you have many links from clearly spammy sites, disavow via GSC. But Google is tolerant of bad links if they are a minority.

**Guest posting:** Look for quality sites in your niche, offer original content. Editorial links (contextualized in the article) are worth more than footer links.

**Avoid:** "Quick link building" services, suspicious reciprocal link programs, blog comments. Modern links are harder to acquire, which is the point.

**Monitor:** Audit backlinks monthly. A new site linking to your domain with 50 links? Potential PBN, disavow.

## See Also

[[Links - PageRank]] — PageRank transferred by a quality link  
[[Authority - Spam Scores]] — Spam backlinks increase spam score  
[[Authority - Site Authority]] — Link quality affects authority
