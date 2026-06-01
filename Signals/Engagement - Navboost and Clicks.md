---
tags: [signal, engagement, navboost, clicks, high-impact, high-confidence]
cargo: [seo-specialist, writer, developer, marketing-director]
confidence: high
category: Engagement
subcategory: SERP Behavior
last_updated: 2026-04-23
---
# Engagement — Navboost and Clicks

A weighted voting system based on clicks that is potentially the #1 ranking signal after PageRank. Navboost is not simply "how many clicks" — it is a sophisticated system that measures specific patterns: good clicks (successful), bad clicks (bounce), last longest clicks (longest dwell), unicorn clicks (from active users), aggregated by page, domain, and even geographic area.

The leak exposes fields like `navboost: float()`, `rawNavboost: float()`, `metroNavboost: float()`, along with `goodClicks`, `badClicks`, `impressions`, `lastLongestClicks`. Dr. Eric Lehman confirmed in the antitrust process: "Navboost is not an ML system. It's just a giant spreadsheet." The characterization is accurate — it is simple aggregation of click data over 13 months, but the impact is massive.

## In the Leak

The `navboost: float()` field appears in multiple modules and stores aggregated click data in a persistent format (not real-time). Key documented fields:

- **`goodClicks`** — clicks where the user did not immediately return to the SERP (satisfied)
- **`badClicks`** — clicks where the user returned quickly (unsatisfied, pogo-sticking)
- **`lastLongestClicks`** — the most recent long click (strong satisfaction signal)
- **`impressions`** — how many times the page was shown in the SERP for the query
- **`clicks`** — raw click count; combined with impressions to derive the effective CTR signal
- **`unicornClicks`** — special clicks from "unicorn users": highly active users with extensive search history

A critical nuance on how **click satisfaction** is measured: it is **not based on dwell time**. The signal is whether the user **continued searching for the same information** after clicking. If a user clicks a result and then returns to Google and searches for the same or closely related query, Navboost interprets this as dissatisfaction and applies a scoring demotion. This is behaviorally distinct from a simple bounce — it specifically detects that the page failed to answer the user's intent. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

Navboost also **bundles queries by interpreted meaning**. This means click data is not siloed per exact keyword match — Google groups semantically similar queries and applies click signals from all of them to the same set of candidate pages. A page that accumulates good click signals across a cluster of related queries benefits from those signals for all queries in the cluster. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

The module summary explicitly defines Navboost as *"click and impression signals for Craps"* (one of the internal ranking systems). Its scope extends to the **subdomain, root domain, and URL level** — which means Google treats different levels of a site independently for click purposes. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

Key structural details confirmed in the leak:

- **Users are represented as voters.** Clicks are stored as votes per query-URL pair, segmented by **country** and **device**. A click from a mobile user in Brazil on a specific query is a separate signal from a desktop user in the US on the same query.
- **`lastGoodClick` date** is tracked per document. A page that was getting good clicks but stopped receiving them signals content decay — the lack of recent good clicks is as much a signal as the presence of bad ones.
- **Squashing** is applied to click signals to prevent a single massive spike from dominating the score. This is why artificially inflating clicks does not produce proportional ranking gains.
- **Glue** is a distinct system from Navboost that handles click signals for universal search results (images, videos, news, local packs) while Navboost focuses on web results. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

Navboost is referenced **84 times** across five dedicated modules in the leaked documentation. Multiple sources from the antitrust trial have confirmed it is *"already one of Google's strongest ranking signals."* *(Source: [Search Engine Land](https://searchengineland.com/how-seo-moves-forward-google-leak-442749))*

## Confidence: High

Field is explicit in code, present in multiple modules, internal documentation is clear, corroborated by judicial confirmation in the antitrust process. Perfectly aligns with observed empirical patterns.

## How It Works

When a Chrome user clicks on a SERP result and returns to (or stays on) the page, Google records: query, clicked URL, dwell time (how long they stayed), whether they returned to the SERP. Simple aggregation: if dwell > 30s and no return = good click. If dwell < 5s and returns = bad click. Clicks from "unicorn" users (long history, trustworthy pattern) carry 2-3x more weight.

Navboost is recalculated every 13 months with new data. A page that received good clicks in 2024 gets a boost. A page that received bad clicks loses ranking.

Relative importance: after PageRank, it is the most direct signal that "users find the page useful." This is why "paid traffic generates ranking boost" — Google Ads generate clicks that Navboost processes.

Navboost also directly feeds the **Panda scoring modifier**. The Panda formula `M = IL / RQ` uses reference queries from Navboost as its denominator — meaning your Navboost query history is part of the calculation that determines whether your site gets a Panda boost or demotion. This confirms Panda refreshes were effectively rolling updates to the Navboost query window, not separate algorithm runs. A Twiddler called **"Baby Panda"** lives inside `CompressedQualitySignals` and is described as running on top of this Panda mechanism. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## How to Measure on Your Site

Google Search Console Performance tab shows clicks and CTR (approximate equivalent of good clicks). Bounce rate in Analytics is a proxy for bad clicks. If you are in position 3 with a CTR half of what is expected for position 3, Navboost is having an impact.

Benchmark: position 1 typically has 20-30% CTR depending on industry. Position 5 is 5-10%. If your numbers are 50% below, the gap is significant.

**Content decay check:** Monitor click trends per page over time in GSC. A page that is declining in clicks while holding its position is accumulating `lastGoodClick` signals that are growing stale — Google will eventually reassign rank to fresher, better-clicked competitors. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## What to Do

**Quick wins (weeks 1-2):**

The title accounts for 70% of CTR impact. For each page in positions 2-5 in Google Search Console, analyze: does the title include the keyword? Does it include a benefit or curiosity that drives clicks? Example: "How to do SEO" vs. "SEO in 2025: 7 techniques that increase traffic by 300%." The second gets 3-4x more clicks.

Meta description accounts for another 20%. Rewrite to be descriptive + include a subtle CTA ("Complete guide →", "Learn now →").

**Medium term (weeks 3-8):**

Use Google Search Console to identify queries where you have impressions but few clicks (CTR gap). For each, look at the top 3 results — how are their titles/snippets different? Do they have something yours doesn't? (year in title, emoji, number of benefits?)

Test rewriting 5-10 titles with better structure. Google Search Console shows title suggestions in some cases.

**Content:**

High CTR but still high bounce rate = content problem (user clicked expecting X but found Y). Depth helps — a 500-word generic article vs. a 2000-word specific one has very different dwell time.

Add contextual internal links in the body (not just a "read more" list at the bottom). When a user clicks an internal link and stays, it improves overall engagement signals.

## Official Reference

[In-Depth Guide to How Google Search Works](https://developers.google.com/search/docs/fundamentals/how-search-works) — Google Search Central: Google explains how it uses click and user behavior data to refine the quality and relevance of rankings, prioritizing pages that users find useful.

## See Also

[[Content - Title Matching]] — A well-aligned title increases CTR  
[[Content - Freshness]] — Fresh content attracts more clicks when relevant  
[[Engagement - Page Behavior]] — Page behavior feeds Navboost  
[[Links - PageRank]] — PageRank is another top-level signal alongside Navboost  
[[Authority - Site Authority]] — Site with good Navboost gains authority  
[[Voice Search - Assistant and Featured Snippets]] — Featured snippet CTR feeds back into Navboost click signals
