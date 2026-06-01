---
tags: [signal, authority, site-authority, trust, high-confidence]
cargo: [seo-specialist, link-builder]
confidence: high
category: Authority
subcategory: Site Authority
last_updated: 2026-04-23
---
# Authority — Site Authority

A score that estimates the general reliability and authority of a domain. Google publicly denied having a "site authority" metric for years; the leak proves the metric exists, is calculated, and is actively used in ranking.

`siteAuthority` is a composite score that fuses link analysis (PageRank), user behavior signals (Navboost), and the site's topical focus. It is persistent and "generally static across multiple queries," functioning as the site's reputational baseline. Calculated at the domain or subdomain level, it is then propagated to all pages of the site.

## In the Leak

`siteAuthority (type: integer())` appears in `CompressedQualitySignals` — an optimized structure that pre-computes and caches critical data points for each document. The fact that it lives here (rather than being calculated on demand) means it is required for fast ranking decisions at serving time.

The `qualityNsrSiteAuthority: float()` field stores a normalized, computed authority score at the **site level** (not per URL). This is a confirmed site-wide metric — explicitly contradicting Google's public statements that they have no domain-level authority score. The `siteAuthority` field represents the cumulative strength of the domain in Google's ranking model.

The **`isElectionAuthority`** field is documented in the `QualityNsrNsrData` section. It stores a bit that determines whether a site has "election authority" — potentially the mechanism behind what SEOs have long hypothesized as "seed sites": domains with the highest PageRank or topical authority that serve as trust reference points for the entire web graph. Note: `nsrIsElectionAuthority` is documented as deprecated, but `isElectionAuthority` remains active. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

**NSR chunking** is documented explicitly: Google divides a domain into chunks (groups of pages by topic or section) and computes NSR values per chunk. If NSR has not been computed for a specific chunk, the system falls back to averaging NSR scores from other chunks on the same site (`nsrdataFromFallbackPatternKey`). This averaging mechanism means that low-quality chunks **actively drag down the NSR score** applied to unscored chunks — making consistent quality across all site sections a structural requirement. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

**`ScaledIndyRank`** (and the experimental `ExptIndyRank3`) appear in the leak. The SEL analysis interprets this as potentially related to information gain at the sitewide level — a measure of how much original or unique content a site contributes compared to the broader topic cluster. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

`CompressedQualitySignals` also contains adjacent fields that directly adjust the effective authority score at ranking time:

- **`ugcDiscussionEffortScore`** — an integer (stored ×1,000) measuring the quality and effort level of user-generated discussion on the page. It coexists in `CompressedQualitySignals` alongside `siteAuthority`, indicating it is considered at the same evaluation stage, though the exact interaction between the two fields is not explicit in the leak.
- **`productReviewPPromotePage`** and **`productReviewPDemoteSite`** — product review quality signals that can promote an individual page or apply a demotion at the entire site level. Poor reviews are penalized at the domain level, not just the page.
- **`productReviewPPromoteSite`**, **`productReviewPReviewPage`**, **`productReviewPUhqPage`** — further product review granularity rewarding sites with consistently high-quality review content.

Separately, **`clientSpamminess (type: integer())`** is a spam score associated with the **client or publishing system** used to create or submit the content — not a personal creator score. A higher value indicates Google considers the publishing tool or submission mechanism to be spammy. This is relevant for UGC platforms, forum systems, or any site where third-party tools generate content at scale.

When a demotion is applied, **`demotionreason (type: integer())`** stores a numeric code specifying the exact category of demotion, confirming that demotions are categorized and tracked per document within the same pipeline as `siteAuthority`.

Two additional site-level fields measure **topical authority through embeddings**:

- **`siteFocusScore`** — captures how much a site sticks to a single topic. It is generated from site2vec vectors that represent the site as a whole.
- **`siteRadius`** — measures how far an individual page deviates from the core site topic based on the same site2vec vectors. A page with a high siteRadius is off-topic relative to the rest of the domain.

*([iPullRank — Secrets from the Google Algorithm Leak](https://ipullrank.com/google-algo-leak))*

Finally, **`hostAge`** is a field stored at the document level specifically used *"to sandbox fresh spam in serving time."* This confirms that domain age acts as a trust gating mechanism, not just a vague quality signal. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: High

Explicit field with data type, present in the critical ranking module, implicitly confirmed by the antitrust process (which revealed that "Site Authority" is real and used). Google had denied its existence for years in public documentation.

## How It Manifests

`siteAuthority` is not a single number pulled from thin air. It incorporates:

- **Domain PageRank:** Quantity and quality of links pointing to the site
- **Engagement signals:** Clicks, dwell time, and user patterns via Navboost
- **Domain age:** Established domains trigger a lower `hostAge` sandbox risk; new domains face trust gating regardless of content quality
- **Penalty history:** Any manual penalty reduces the score; the reason is logged in `demotionreason`
- **Topical focus:** `siteFocusScore` measures how tightly a site sticks to a single topic; `siteRadius` measures how far individual pages deviate from that core. Sites with high focus and low radius rank better
- **UGC quality:** Pages with low-effort comments or thin discussion receive a lower `ugcDiscussionEffortScore`, evaluated at the same pipeline stage as `siteAuthority`
- **Product review quality:** Sites with poor or thin product reviews can receive a site-level demotion via `productReviewPDemoteSite`, independent of backlink health
- **Creator/client tools:** `clientSpamminess` tracks the spam history of the publishing system used to generate content — relevant for sites using mass-publishing tools or automated content submissions

For **new pages** without their own PageRank or click history, Google uses the homepage's PageRank (Nearest Seed version) and `siteAuthority` as proxies until the page accumulates its own signals. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

The **Panda scoring modifier** — which functions as a Twiddler re-ranking adjustment — is documented as the formula `M = IL / RQ`, where IL = independent links (unique linking root domains) and RQ = reference queries (queries from Navboost that successfully led users to the site). This modifier can be applied at the domain, subdomain, or subdirectory level. A related Twiddler called **"Baby Panda"** is referenced inside `CompressedQualitySignals`, described as running on top of Panda. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

The leak also documents a **"small personal site" flag**. Sites tagged with this flag can theoretically receive boosting or demotion Twiddlers — the documentation confirms the classification exists, but does not specify the current weight applied. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## How to Measure on Your Site

Google Search Console does not directly disclose siteAuthority. But there are measurable proxies:

- **Domain Rating (Ahrefs):** Correlates strongly with siteAuthority, 0-100 scale
- **Authority Score (Moz):** Alternative Domain Authority
- **Backlink Profile (SEMrush):** Volume and quality of backlinks
- **Penalty history:** Check the "Security & Manual Actions" tab in GSC
- **CTR and impressions by domain:** In GSC, aggregate data shows overall health

Track these proxies monthly. Consistent improvement in Domain Rating is a good indicator that siteAuthority is growing.

## What to Do

**Building quality links** is the most obvious direct impact. But it's slow (6-12 months for measurable change). In parallel:

- **Consolidate theme:** `siteFocusScore` rewards topically tight sites. A site about "basketball" ranks better than "basketball + finance + cooking mixed together." Use `siteRadius` as a conceptual test: would a new article clearly fit under the site's core topic umbrella?
- **Improve engagement:** Content that generates good clicks (Navboost) contributes to siteAuthority. Write to keep users on the page.
- **Avoid spam:** Any spam signal drains siteAuthority. Audit your backlink profile (Ahrefs, SEMrush) for suspicious links and disavow via Google Search Console.
- **Publish consistently:** Active sites (1-2 articles/month) gain more trust than dormant sites.
- **Engage with EEAT:** Links from well-known columnists, certifications, appearances in reputable media raise perceived credibility.
- **Prioritize new pages' link-building:** Since new pages use `siteAuthority` and homepage PageRank as a proxy, internal linking from high-authority pages on your site is especially important for pages without their own established click or link history.

## Official Reference

[In-Depth Guide to How Google Search Works](https://developers.google.com/search/docs/fundamentals/how-search-works) — Google Search Central: Google explains that its ranking systems use links between pages to determine which are most useful and relevant, with PageRank being one of the most important ranking systems.

## See Also

[[Links - PageRank]] — Critical component of siteAuthority  
[[Engagement - Navboost and Clicks]] — User signals that feed authority  
[[Authority - Spam Scores]] — Penalties that reduce authority; `clientSpamminess` and `demotionreason` live alongside siteAuthority in the same pipeline  
[[Content - EEAT]] — Expertise that complements technical authority  
[[Chrome - Visit Signals]] — Site-level visit signals contribute to the authority composite  
[[Structured Data - Schema]] — Product review markup is tracked directly in CompressedQualitySignals  
[[Authority - Document Quality]] — Document quality and site authority are both stored in CompositeDocQualitySignals
