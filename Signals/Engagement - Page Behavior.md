---
tags: [signal, engagement, behavior, dwell-time, scroll, high-confidence]
cargo: [seo-specialist, developer, writer]
confidence: high
category: Engagement
subcategory: Page Behavior
last_updated: 2026-04-23
---
# Engagement — Page Behavior

Signals of how users interact within the page. Complements Navboost (which measures SERP clicks). Page behavior — dwell time, scroll depth, internal link clicks — is collected anonymously via Chrome and feeds the Popularity system. A page where users scroll deeply and stay 3+ minutes receives a positive signal. A page where 80% of users leave in 10 seconds receives a negative signal.

Fields like scroll depth (%, how far they scrolled), dwell time (how long they stayed), and engagement events (clicks, video plays) are recorded for each page. They correlate strongly with Navboost — a site with good page behavior tends to have good SERP engagement as well.

## In the Leak

Engagement signals appear in a distributed way across behavioral modules. There is no single `engagementScore` field, but multiple signals from `sessionDuration`, `scrollDepth`, `clicksPerSession` that are aggregated. Chrome collects this data continuously and anonymously.

Page behavior data feeds the **Popularity system (P\*)**, one of the two top-level ranking pillars documented in the leak. Unlike quality signals (Q\*) which are evaluated at the document level during indexing, P\* signals are continuously updated as users interact with pages. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

Poor page behavior can trigger a **SERP demotion** — one of the named demotion categories documented in the leak. A page that consistently receives bad Navboost signals (high bounce rate, quick returns to SERP) accumulates enough negative engagement data to trigger an automated demotion applied by the Twiddler pipeline. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

The leak documents **`ImageQualityNavboostImageQualityClickSignals`** — a set of click-based quality signals applied specifically to images in search results. Named sub-signals include `usefulness`, `presentation`, `appealingness`, and `engagingness`. These are classified as **Search CPS Personal data**, meaning they are derived from individual user interactions and aggregated at a privacy-preserving level. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

Practical implication: images in search results are evaluated not just for indexing but for their click-through quality. Images that are appealing and useful in context accumulate positive signals that strengthen the page's overall Navboost profile.

## Confidence: High

Chrome collection explicitly confirmed in the antitrust process. Correlation with ranking empirically validated — pages with high bounce rate lose position in direct competition.

## How It Works

When a Chrome user visits a page, the browser records: how long they stayed, how much they scrolled (%), how many links they clicked, whether they hovered over elements. All data is aggregated anonymously. Google then uses this to refine its quality understanding. A page where 90% of users leave in 5 seconds without scrolling? Signal of "did not meet intent." A page where 60% of users scroll to the end? Positive signal.

Page behavior affects Navboost indirectly: users who find the page useful (long dwell time, deep scroll) do not return to the SERP or return less frequently. The pattern of "user clicked and stayed" without return = good click in Navboost.

## How to Measure on Your Site

**Google Analytics 4** is the primary tool. Relevant metrics:

- **Session Duration:** Average time users stay (Analytics > Audience > Overview)
- **Bounce Rate:** % that leave without interaction (Analytics > Pages and Screens)
- **Scroll Depth:** Requires manual event setup (create event in GA4 when user scrolls 25%, 50%, 75%, 100%)
- **Link Clicks:** Create event for each important CTA

Indirect metric in Search Console:
- **CTR vs. Position:** If you are in position 3-5 with low CTR, it may be lack of page engagement (users click on 1-2 because those retain better)
- **Query correlation:** Queries where your page has high bounce may be losing position

## What to Do

**Page structure:** Keep relevant content at the top. The first paragraph should answer the main question, not be a generic introduction. A user who sees an irrelevant page leaves in 5 seconds. A user who sees an immediate answer stays.

**Formatting:** Look for "walls of text" — long paragraphs without breaks. Break them up with h2/h3, bullet points, highlight boxes, images. Visual to scan = more time on page.

**Internal linking:** Contextualize links to related articles. Example: in an article about "technical SEO," link to "Core Web Vitals" within the relevant text (not generically at the end). Users who click internal links have higher engagement.

**Call-to-action:** Place a relevant CTA (e.g., "Read our complete SEO guide") where it makes sense, not forced at the top. A well-placed CTA increases click depth.

**Remove distractions:** Ads, pop-ups, or elements that impair reading reduce time on page. Remove as many as possible.

**Speed:** A slow page affects scroll depth — users wait for loading, bounce increases. Core Web Vitals matter here for indirect impact.

Practical metric: for a page in position 5, compare bounce rate/dwell time with positions 1-2 via Analytics. If the gap is large (your page has 60% bounce vs. competitor's 30%), content/format gap is probably the reason.

## Official Reference

[Page Experience](https://developers.google.com/search/docs/appearance/page-experience) — Google Search Central: Google explains how page experience factors, including loading speed and interactivity, affect ranking, while also recognizing engagement signals as important.

## See Also

[[Engagement - Navboost and Clicks]] — System that uses page behavior  
[[Content - Word Count and Structure]] — Formatting affects scroll depth  
[[Speed - Core Web Vitals]] — Speed affects page behavior
