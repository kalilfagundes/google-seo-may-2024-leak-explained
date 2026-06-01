---
tags: [signal, link, anchor-text, quality, high-confidence]
cargo: [seo-specialist, link-builder]
confidence: high
category: Links
last_updated: 2026-04-23
---
# Links — Anchor Text

The clickable text of a link. Google analyzes anchor text to understand the topic of the linked page. A link with anchor "SEO guide" communicates that the destination page is about SEO. Unnatural anchor text (excessive exact match) triggers manipulation filters.

The leak exposes fields like `anchorText` and `anchorTextDomain` that capture the anchor and its context. Google detects abnormal patterns: 50+ links with anchor "buy cheap laptops" = unnatural, spam signal.

## In the Leak

Fields `anchorText: String.t()`, raw and clean versions of the anchor. Bitvectors record which terms appear at which position in the anchor.

The leak documents **`droppedLocalAnchorCount`** — a field tracking the number of **internal links** that were dropped (not counted) by Google's link spam detection. This confirms that Google does not automatically count all internal links — it can selectively discard internal links that look manipulative (e.g., excessive keyword-exact anchors in site-wide sidebars or footers). *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

The **anchor mismatch demotion** is a named demotion category in the leak: if the anchor text of incoming links consistently describes a different topic from the page content, a demotion is applied. This makes anchor text a two-edged signal — helpful when consistent, harmful when misaligned. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

**Font size of anchor text** is tracked as a weighted signal. Anchor text rendered in larger fonts (e.g., within headings or prominently styled links) carries more weight than small-print body text anchors. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: High

Explicit fields, obvious validation (natural anchors rank better than exact-match spam).

## How It Works

When Google processes an external link, it extracts the anchor text. If the anchor is "click here," it learns little. If the anchor is "how to do SEO in 2025," it learns that the destination page is about SEO, updated for 2025.

Google detects patterns: if 100 PBN sites link with the same exact anchor = spam. Natural combinations of variations = legitimate.

## What to Do

**Receiving links:** Do not control anchor text of received links (spam signal). Let the linking site use whatever anchor it finds appropriate. A natural mix of branded, exact-match, and generic anchors is healthy.

**Your own links:** When you link internally or in guest posts, use descriptive but natural anchors. "Read our SEO guide" vs. "SEO guide" vs. "click here." Mix it up.

**Backlink audit:** Look for abnormal patterns in Ahrefs. If 50% of links have the same exact anchor = past problem. Disavow via GSC if you can't remove them.

## Official Reference

[In-Depth Guide to How Google Search Works](https://developers.google.com/search/docs/fundamentals/how-search-works) — Google Search Central: Google explains how it analyzes links and their context, including anchor text, to determine the relevance and quality of linked pages.

## See Also

[[Links - PageRank]] — PageRank from the source site  
[[Links - Quality]] — Overall backlink quality
