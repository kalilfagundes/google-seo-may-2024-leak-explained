---
tags: [signal, authority, spam, spambrain, high-confidence]
cargo: [seo-specialist]
confidence: high
category: Authority
subcategory: Spam Detection
last_updated: 2026-04-23
---
# Authority — Spam Scores

Google's spam detection system that identifies and disqualifies pages with manipulative or fraudulent patterns.

SpamBrain is not a single score, but a system that generates multiple metrics. The leak exposes fields like `spamrank` (0-65535, a scale similar to PageRank), `scamness` (0-1023, the probability of a page being deceptive), and `clientSpamminess` (evaluates the credibility of the content creator). There are also legacy versions (`spamscore1`, `spamscore2`) that are deprecated. These scores are pre-computed and made available in the Mustang ranking system, transforming spam detection from reactive (manual punishment) to proactive (automatic disqualification).

## In the Leak

The `spamrank` field appears in PerDocData as an integer type. The `scamness` field uses a 0-1023 scale, indicating the probability of a page being fraudulent — a probabilistic approach instead of a simple boolean (is or isn't spam). There is `SpamBrainData` as an aggregated structure and `clientSpamminess` which evaluates the publishing client/system (important for UGC and reviews).

The leak documents multiple **demotion categories** that are tracked per document. iPullRank's analysis of the leak identified at least the following named demotion types: *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

- **Anchor mismatch demotion** — anchor text of incoming links does not match the page topic
- **SERP demotion** — triggered by bad Navboost signals (too many "bad clicks" for the query)
- **Nav demotion** — poor navigation/site structure preventing proper crawl
- **EMD demotion** — Exact Match Domain penalty for thin-content sites using keyword-rich domains
- **Product review demotion** — low-quality or non-expert product reviews (`productReviewPDemoteSite`)
- **Location demotions** — applied for globally or super-globally inappropriate content
- **Porn demotions** — safe search enforcement categories

Additionally, **`phraseAnchorSpamDays`** is documented as a field tracking the **link velocity of spammy anchor patterns** — it measures how many days a suspicious anchor-text pattern has been active. This confirms Google tracks spam over time, not just as a snapshot. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

**Domain registration** information is stored in the composite document data. This is directly linked to the `hostAge` sandboxing mechanism — freshly registered domains face an elevated spam threshold before links and content from them are fully trusted. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: High

Multiple explicit fields with clear data types, confirmed by Google's spam updates in 2024 (June and December) that demonstrate the system in action. Several fields with different versions indicate continuous system evolution.

## How It Works

SpamBrain trains on known spam patterns to detect signs of manipulation. Techniques that raise spam scores include:

- **Mass link buying:** Primarily links with unnatural exact anchor text or link profiles with a clear buying pattern
- **Content spinning:** Tools that generate variations of duplicate content
- **Keyword stuffing:** Forced insertion of search terms without natural context
- **Cloaking:** Serving different content to Googlebot vs. real users
- **PBN (Private Blog Networks):** Networks of satellite sites with artificial cross-links
- **Scammy patterns:** Deceptive redirects, phishing, malware

The SEL analysis of the leak documents additional named spam fields not covered elsewhere: *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

- **`gibberishScores`** — explicitly targets spun content, filler AI content, and incoherent text. Google evaluates whether generated content makes semantic sense, not merely whether it passes a grammar check.
- **`trendSpam`** — defined as "count of matching trend spam queries." This is interpreted as targeting CTR manipulation through trending keyword injection and clickbait that hijacks trending terms without topically relevant content.
- **`spamWordScore`** — certain vocabulary terms are classified as intrinsically spammy in Google's model. Found primarily in the context of anchor text evaluation.
- **`phraseAnchorSpamPenalty`** — a combined penalty specifically tied to the anchor score (not a link demotion or authority demotion), applied when spam phrases are found in anchor patterns.
- **`spamRank`** — measures the likelihood that a document links to known spammers, stored as values 0 and 65535.

A structurally important dynamic documented in the anchor spam analysis: **`trustedTarget`** marks URLs that are on a "trusted source" list. These URLs face a lower spam threshold for their anchor patterns — trusted sources can use anchor text patterns that would penalize less established sites. *(Source: [Search Engine Land](https://searchengineland.com/unpacking-googles-massive-search-documentation-leak-442716))*

An important constraint in Google's link analysis: the system only uses the **last 20 changes** for a given URL when analyzing its link history. This means a dramatic improvement or spike in link acquisition is observed within a bounded window — spam velocity (acquiring many links in a short period) is more visible because it concentrates in that window. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

Domains with a history of rapid niche changes, suspicious buying/selling, or prior manual penalties receive higher spam scores.

## How to Measure on Your Site

Google Search Console manually reports spam-related actions ("Unnatural links," "Thin content," "User-generated spam"). But SpamBrain scores are calculated continuously without manual intervention.

Measurable proxies:

- **Backlink profile integrity:** Audit links via Ahrefs/SEMrush — look for unnatural anchor text patterns, link clusters from the same IPs, or obvious satellite domains
- **Malware/Security signals:** GSC "Security & Manual Actions" tab shows malware or suspicious redirect warnings
- **Content quality:** Tools like Copyscape detect duplication. Original content is the baseline.
- **Link acquisition patterns:** If you acquired 1,000 links in 1 month from "SEO services," spam score is high

## What to Do

Avoiding black-hat techniques is the obvious first step. But there are nuances:

- **Clean up bad links:** If you inherited a domain or worked with a bad agency, audit links and disavow via GSC those that look like spam (PBNs, anchor text spam, low-quality domains)
- **Maintain niche consistency:** Rapid topic changes (e.g., travel blog becomes supplement store) trigger spam alerts. If pivoting, do it gradually or on a new domain
- **Transparency in UGC:** If your site has user comments or reviews, the quality of `clientSpamminess` depends on how you moderate. Remove spam reviews
- **Growth velocity:** Links acquired slowly (2-3/week) raise less suspicion than 100 in a month

Original content, slow and active quality link building, and cohesive topical focus naturally keep spam scores low.

## Official Reference

[Google Search Spam Policies](https://developers.google.com/search/docs/essentials/spam-policies) — Google Search Central: Google defines its spam policies and emphasizes that link manipulation, duplicate content, cloaking, and other fraudulent patterns can result in search penalties.

## See Also

[[Authority - Site Authority]] — Overall authority that suffers with high spam scores  
[[Links - Quality]] — Backlink quality as a spam factor  
[[Links - PageRank]] — Comparison of positive signals vs. spam negations
