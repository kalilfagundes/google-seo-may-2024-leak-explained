---
tags: [signal, link, pagerank, authority, critical, high-confidence]
cargo: [seo-specialist, link-builder]
confidence: high
category: Links
last_updated: 2026-04-23
---
# Links — PageRank

A link-voting algorithm where a page receives authority based on the authority of pages linking to it. PageRank still exists and is one of the two top-level ranking signals (along with Navboost). A page linked by 10 high-authority sites gains more PageRank than a page linked by 100 low-authority sites.

The leak exposes multiple PageRank variations: `pagerank: float()` (raw), `pagerankNs: float()` (namespace-specific for localized queries), `firstCoveragePagerank: float()` (PageRank based on when the link was first found). It is still calculated and actively used.

## In the Leak

Fields `pagerank: float()`, `pagerankNs: float()`, with namespace-specific variants. Calculation is an iterative model similar to the original by Page and Brin.

The leak exposes additional PageRank variants not commonly known: *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

- **`IndyRank`** — an independent rank calculation variant used in specific scoring contexts
- **`PageRankNS`** — a namespace-specific PageRank for localized or segmented queries
- **`firstCoveragePagerank`** — PageRank calculated from when a link was *first* found (not current state), providing a historical anchor
- **Homepage PageRank (Nearest Seed)** — the homepage PageRank is associated with every sub-page on the site as a proxy for new pages that have not yet accumulated their own link equity. This is the mechanism that makes internal linking from the homepage strategically valuable.

The SEL analysis identifies **7 total PageRank types** referenced in the leak: *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

1. **PageRank 0** — baseline
2. **PageRank 1** — variant 1
3. **PageRank 2** — variant 2
4. **ToolBarPageRank** — the legacy public PR metric (still present in the system, though not exposed publicly)
5. **PageRank NR** — Named / normalized rank
6. **PageRankNS** — Nearest Seed (topical, localized)
7. **IndyRank** — independence rank

**PageRank NS (Nearest Seed)** operates differently from classic PR: instead of web-wide link graph propagation, it focuses on a **localized subset of the network around seed nodes**. Proximity and topical relevance are the key factors. This allows PageRank to be effectively personalized by topic cluster — pages within the same topical neighborhood receive more relevance credit from each other than from the broad web graph. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

Google only uses the **last 20 changes** for a given URL when analyzing its link profile. This creates a bounded window where recent link acquisition patterns have disproportionate visibility — a spike of 50 links in one week is extremely visible within that window. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: High

Explicit fields, algorithm publicly confirmed by Google as still active, obvious empirical validation.

## How It Works

Links are "quality votes." Site A with PageRank 7 linking to site B transfers more authority than a site with PageRank 2. PageRank is calculated iteratively — Site B gains PageRank from all sites linking to it, weighted by the PageRank of each.

Critical difference: PageRank flows through `follow` links. `nofollow` links do not transfer PageRank. Importance: a Wikipedia link is worth a lot (high PR, trusted), a comment spam link is worth nothing (nofollow).

## What to Do

**Link building:** Look for high-authority sites in your niche. Guest posting, editorial links, partnerships. Quality >> quantity.

**Backlink analysis:** Use Ahrefs/SEMrush to see: who links to you? What is their Domain Rating? If most have DR < 20, that's a problem. If there's a mix with DR 50+, that's good.

**Disavow spam:** If you have spam links (PBN, blog network, zero relevance), disavow via Google Search Console. But many small spam links < importance of disavowing.

**Internal linking:** Distribute PageRank internally. Homepage has more PR, link from it to important pages. Internal link structure matters.

## See Also

[[Authority - Site Authority]] — Site Authority is the result of aggregated PageRank  
[[Links - Anchor Text]] — Link context matters alongside PageRank  
[[Links - Quality]] — Link quality that transfers PageRank
