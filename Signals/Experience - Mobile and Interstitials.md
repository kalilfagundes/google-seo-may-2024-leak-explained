---
tags: [signal, experience, mobile, interstitials, ux, high-confidence]
cargo: [developer, seo-specialist]
confidence: high
category: Experience
subcategory: User Experience
last_updated: 2026-04-23
---
# Experience — Mobile and Interstitials

Detection and penalization of elements that harm user experience on mobile. Google has penalized intrusive interstitials (pop-ups that block content) since 2017. The leak confirms that Google automatically detects pages with mobile UX issues and demotes them.

Detection fields include viewport analysis, presence of interstitials, and responsive layout. A page with a pop-up covering 50% of the screen when loading on mobile is penalized. Legitimate pop-ups (age gate, login) are an exception.

## In the Leak

Interstitial detection and mobile UX fields appear in page analysis modules. Google detects and flags pages with problems.

Mobile rendering analysis is performed by the **Htmlrender** pipeline at indexing time. Htmlrender renders the page in a mobile viewport and assesses DOM structure, visible content, and UI elements. Interstitials that appear at render time (rather than after user interaction) are the most likely to be flagged. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

The leak also documents a **"video-focused site" classification** applied to sites where more than 50% of pages contain video. This classification changes how content quality and engagement signals are evaluated for such sites — an important distinction for YouTube-embedded content sites, media publishers, and educational platforms. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: High

Google publicly disclosed interstitial penalties (2017), the pattern is confirmed in the leak.

## How It Works

When a page is indexed, Google renders it on mobile and detects: is there a pop-up on screen? Does it block content? Does it appear immediately or after scrolling? Is it legitimate (login, cookies, age gate) or marketing? Based on this, it applies a ranking reduction or not.

## What to Do

**Avoid:** Newsletter pop-ups on load on mobile. Ads that cover content. Overlays that require closing.

**Permitted:** Login modals (required for access). Age gates (legally mandated). Cookie notices (legal requirement). Surveys after engagement (less intrusive).

**Best practice:** Show pop-ups after the user has scrolled 50% or after 15 seconds (user is genuinely interested). On mobile, push to the bottom of the page, not the top.

## Official Reference

[Page Experience](https://developers.google.com/search/docs/appearance/page-experience) — Google Search Central: Google explains that intrusive interstitials and mobile experience problems can hurt ranking, emphasizing the importance of a user-friendly design.

## See Also

[[Speed - Core Web Vitals]] — Interstitials affect Core Web Vitals  
[[Engagement - Page Behavior]] — Interstitials increase bounce rate  
[[Authority - Document Quality]] — Intrusive interstitial detection is part of the Htmlrender rendering quality pipeline
