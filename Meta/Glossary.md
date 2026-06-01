---
tags: [glossary, terms, definitions]
cargo: [all]
confidence: n/a
category: Meta
last_updated: 2026-04-23
---
# Glossary

Reference for technical terms that appear in the leak and SEO documentation.

## Anchor Text

The clickable text of a link. Google extracts and analyzes anchor text to understand the topic of the linked page. The `anchorText` field is present in the leak within CompressedQualitySignals. Natural and descriptive anchor text is preferred over forced constructions like "click here."

## API Content Warehouse

Google's internal system that stores structured data for every processed page. This is where all ranking signals (PageRank, Navboost, freshness scores, etc.) live. The leak exposes the structure of this repository.

## Authority Score

A reliability/authority score for a domain or site. See [[Authority - Site Authority|Site Authority]].

## Bad Clicks

Clicks on the SERP followed by a quick return to search (typically within 30 seconds or less). Google interprets this as a negative signal: the user did not find what they were looking for on the page. The `badClicks: float()` field appears in the Navboost module.

## Backlink

An external link pointing to your page. Processed through the PageRank system. The more authoritative the source site, the more value the link transfers.

## Bitvector

A compressed true/false representation for multiple variables in a single number. In the leak, used to store which query terms appear in which parts of the page (title, body, headers). Saves space at the scale of billions of pages.

## Canonical

The `rel="canonical"` tag that indicates which version of a duplicate page is preferred for indexing and ranking. Google explicitly processes this signal. Essential when you have multiple URLs serving the same content.

## Chrome Data

Data collected anonymously from users browsing the web via the Chrome browser. Includes information about which sites are visited, how long users stay, and navigation patterns. Confirmed in the antitrust process as a direct source of the Popularity signal and input for Navboost.

## CLS (Cumulative Layout Shift)

A Core Web Vitals metric that quantifies visual instability during page loading. Score from 0 to 1; below 0.1 is considered "good." An official Google ranking criterion.

## Content Warehouse

See API Content Warehouse.

## Core Web Vitals

Three official Google page quality metrics: LCP (time until the largest content loads), CLS (visual instability), and INP (interactivity responsiveness). Confirmed as a direct ranking factor. Data available in PageSpeed Insights and Google Search Console.

## CTR (Click-Through Rate)

The proportion of impressions that resulted in clicks on the SERP. Calculated as Clicks ÷ Impressions. Measurable in Google Search Console and acts as an approximate proxy for Navboost signals that Google does not publicly disclose.

## Dwell Time

The time a user spent on your page before returning to the SERP. The longer, the better for Google. There is no direct dwell time metric in Google Search Console, but it can be approximated in Analytics 4 with "session duration" or in Search Console with Navboost signals (last longest clicks).

## Domain Authority

A proprietary 0-100 score from SEO tools like Moz and Ahrefs that attempts to estimate domain authority. Not a Google metric, but correlates with `siteAuthority` found in the leak.

## EEAT

Acronym for Experience, Expertise, Authoritativeness, Trustworthiness. A public framework disclosed by Google in its Search Quality Rater Guidelines. The leak exposes technical fields like `topicExpertise` and `authorInfo` that measure these attributes.

## Engagement

A general measure of how users interact with a page: clicks, time on page, scroll depth, interactions with elements. Multiple signals in the leak contribute to engagement (goodClicks, unicornClicks, dwell time).

## Entity

A recognizable thing or concept: person (Albert Einstein), place (Paris), brand (Google), concept (Democracy). Google maintains a database of interconnected entities in the Knowledge Graph. Optimizing for relevant entities improves topical relevance.

## Featured Snippet

A quick-answer box at the top of the SERP that displays summarized information directly. Processed through the AssistantSnippets module in the leak. Achieving a featured snippet boosts CTR and perceived authority.

## Freshness

Content recency. Google gives more weight to recently updated or created content for time-sensitive queries (news, events, prices, scientific discoveries). The `recency` and `freshnessScore` fields appear in the leak.

## Geostore

Google's internal database with local business information (names, addresses, hours, photos). Critical for Local SEO. The leak exposes 1,480 signals dedicated to Geostore and local ranking.

## Good Clicks

Clicks on the SERP not followed by a quick return to search. Google interprets this as a positive signal: the user found what they were looking for. The `goodClicks: float()` field is one of the most important signals in the Navboost module.

## Google Search Console

Google's official free tool that reports impressions, clicks, and average position of your pages on the SERP. Allows you to approximately measure the impact of signals like Navboost (through CTR and click behavior). Essential for SEO monitoring.

## Graph (Knowledge Graph)

Google's database that maps entities and the relationships between them. Powers Knowledge Panels on the right side of search results. Presence in the Knowledge Graph increases perceived authority.

## Host-level

Aggregation of signals at the entire domain level (e.g., metrohosts.com as a whole). Google analyzes the aggregate health and quality of the host in addition to page-by-page signals.

## Impression

A display of a search result on the SERP. Counted when your URL appears to a user in a specific search. The `impressions: float()` field records this data. Measured in Google Search Console.

## INP (Interaction to Next Paint)

A recent Core Web Vitals metric that measures overall latency between a user interaction (click, tap) and the next visual paint in the browser. Reflects the general responsiveness of a page.

## Interstitial

A pop-up, overlay, or intrusive element that blocks or obstructs main content upon loading. Google has penalized intrusive interstitials on mobile since 2017. Exceptions: legitimate patterns like login, age gates, cookie notices.

## Knowledge Graph

See Graph (Knowledge Graph).

## LCP (Largest Contentful Paint)

A Core Web Vitals metric that measures the time until the largest content element (image or text block) becomes visible in the viewport. Below 2.5 seconds is "good." Highly optimizable with CDN, image optimization, and CSS minimization.

## Link Building

The practice of acquiring backlinks from other sites. A classic SEO strategy driven by the fact that PageRank is still a critical signal. The quality of the source site matters more than the quantity of links.

## Meta Tag

An HTML element that provides metadata about a page (not visible to users). Google explicitly processes meta description, robots, charset. Meta description does not affect ranking directly, but affects CTR on the SERP.

## Metro-level

Aggregation of signals by metropolitan geographic area. The leak exposes signal variants like `metroNavboost` that refine ranking by region.

## Navboost

Google's internal voting system based on clicks and navigation aggregated from 13 months of Chrome data. Refines and adjusts rankings based on real user patterns. Confirmed in the antitrust process as "not ML, just a giant spreadsheet" according to Dr. Eric Lehman. One of the two top-level signals (along with PageRank).

## NLP (Natural Language Processing)

Computational processing of natural language. Google uses multiple NLP models (BERT, T5, etc.) to understand the semantics of content, queries, and relationships between them. Impacts how content is understood without relying on exact keyword matching.

## Original Query Term Coverage

A measure of how deeply each individual query term is covered on the page. Not about presence (is it there or not), but depth of coverage of the concept.

## PageRank

The classic link-voting algorithm created by Page and Brin in 1998. A page receives authority based on the authority of pages linking to it, weighted by how much each page is linked. One of the two confirmed top-level ranking signals.

## Page Experience

An aggregated signal that includes Core Web Vitals (LCP, CLS, INP), mobile-friendliness, HTTPS, and absence of intrusive interstitials. Used as a ranking criterion.

## Proto / Protobuf

Protocol Buffers, a serialization format used internally by Google. The leak is in proto format converted to Markdown for readability.

## Query Coverage

A measure of how well a page covers all aspects and subtopics related to a search query. A page that covers more aspects of the query ranks better. Related to "topical authority."

## Quality Score

An overall document quality score compressed in CompressedQualitySignals. Reflects originality, depth, authority, and reliability of content.

## Recency

How recent the content is. The `recency` field in the leak marks the publication date or last update. Critical for queries where currency matters (news, product reviews, evolving topics). Less critical for evergreen content.

## Rendering

The process of converting HTML/CSS/JavaScript code into a visually rendered page. Google renders all pages before indexing them. Blocking resources (CSS/JS loaded in the `<head>`) delay rendering and affect Core Web Vitals.

## SafeSearch

Google's filter that removes adult content, violence, and spam from search results. The `safesearchScore` field appears in the leak. Content following Google's policies is not affected.

## Schema.org

Standard vocabulary for semantically annotating content. Google explicitly processes Article, FAQPage, Product, Rating schemas. Structured data helps Google understand content but is not a direct ranking factor.

## Search Console

See Google Search Console.

## SERP (Search Engine Results Page)

The search results page. Where your site appears (or not) when a user searches for relevant keywords.

## Site Authority

A score that estimates the general reliability and authority of a site. The `siteAuthority: float()` field explicitly appears in CompressedQualitySignals in the leak. Google denied having a site authority metric for years; the leak proves otherwise.

## Snippet

A 150-160 character summary that appears below the title on the SERP. Automatically extracted from meta description or content. Directly affects CTR.

## Spam Score

A score that estimates the probability of a page or site being spam. The `spamrank` and `spamScore` fields appear in the leak. Black-hat tactics such as buying links, thin content, and unnatural anchor text patterns raise the spam score.

## SpamBrain

Google's ML spam detection system. The leak exposes the structure of `SpamBrainData`. It continuously evolves to detect new spam techniques.

## Title Tag

An HTML element that defines the page title (appears in browser tabs and as blue text in the SERP). One of the most direct relevance signals. Title analysis fields (`titleMatch`, `titleMatchingScore`) appear in the leak.

## Title Matching

A score of how well the title aligns with the intent and terms of the query. Not keyword stuffing, but the natural presence of the main terms.

## Unicorn Clicks

A special subset of clicks associated with "unicorn users": very active users with an extensive search history. The `unicornClicks: float()` field appears in Navboost. Clicks from active users may carry different weight.

## UGC (User Generated Content)

Content created by users: comments, reviews, replies. The leak exposes UGC signals. Reviews and community-generated content increase trust.

## Velocity

The speed of signal application and propagation. "A page with frequent updates has high velocity." Implicit in Freshness and Recency.

## Web Vitals

A set of page experience quality metrics officially disclosed by Google. Includes Core Web Vitals (LCP, CLS, INP) and others like TTFB (Time to First Byte).

## Webref Entity

Google's internal system for referencing and linking entities within documents and to the Knowledge Graph. Used in Entity Recognition. Linking to entity pages improves entity relevance.

## Word Count

The total number of words on the page. The `wordCount` field in the leak. There is no magic threshold, but typically 300-3000 words for main content is expected. Quality matters more than quantity.

---

## See Also

[[Confidence Methodology]]  
[[About the Leak]]
