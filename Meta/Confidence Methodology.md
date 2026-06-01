---
tags: [meta, methodology, confidence, framework]
cargo: [seo-specialist]
confidence: n/a
category: Meta
last_updated: 2026-04-23
---
# Confidence Methodology

How we classify High, Medium, or Low confidence in signals from the Google Leak 2024.

Confidence reflects the degree of evidence we have that a signal is effectively used in ranking. It comes from three sources: (1) explicit presence in the Content Warehouse code, (2) external confirmations such as the U.S. vs. Google antitrust process 2024-2025, and (3) correlations observed in SEO tests that validate the theory.

## High Confidence

A signal receives a High classification when it is present as an explicit field in the code with a clear data type, appears in multiple ranking modules, and/or has been publicly confirmed by Google or revealed in antitrust testimony.

**Examples:**

- `goodClicks`, `badClicks` (Navboost) — float type field, referenced in NavBoost, QualitySignals, and RankingSignals, confirmed in testimony by Dr. Eric Lehman in court
- `pagerank`, `pagerankNs` (PageRank) — float type field, present since Google's beginnings, still active in the code
- `chromeVisits` (Chrome data) — float type field, confirmed in the antitrust process as direct input for the Popularity signal
- `siteAuthority` (Site Authority) — float type field in CompressedQualitySignals, contradicts Google's public denials about site authority metrics

High confidence means: the signal exists, the type is clear, the internal documentation is explicit or there is external confirmation, and it is not marked as deprecated or experimental. Implement with priority.

## Medium Confidence

A signal receives a Medium classification when the field exists and is active, but its calculation method or usage context is partially ambiguous, or when it is inferred from multiple related fields that converge on the same idea.

**Examples:**

- `unicornClicks` (Navboost) — field exists, type is clear, but "Unicorn user" (a rare user with specific behavioral patterns) is not formally defined in the code. It is interpreted via context.
- Entity Strength — no single field with that name exists, but `knowledgeGraphAnnotations`, `webrefEntity`, `entityAliases`, and `entityScore` converge on the concept of entity strength
- `freshnessScore` — field present, but how it interacts with `contentAge` and which query types benefit most from freshness requires inference

Medium confidence means: the field or concept is firmly present, but there is room for refinement through testing. Implement with validation tests.

## Low Confidence

A signal receives a Low classification when it is deprecated in the code, deduced from a pattern without explicit declaration, or appears in experimental modules.

**Examples:**

- Fields marked as `// DEPRECATED` — still in the code, but Google stopped using them
- `socialMediaLinkWeight` — no such field exists in the code. The idea that social links pass PageRank is an educated guess, not a declaration
- Fields in `// EXPERIMENTAL` — subject to change or removal in future versions

Low confidence means: speculation, obsolete technique, or hypothesis without explicit anchoring. Experiment later, do not prioritize.

## Why This Classification Matters

High confidence justifies immediate investment. Medium confidence merits structured testing. Low confidence is secondary learning.

Confidence is not about the signal's weight in ranking (that is unknowable), but about how certain we are that the signal exists and is used. A Medium confidence signal may have more impact than a High confidence one. The difference is that we know more about how the High confidence signal works.

## Official Reference

[In-Depth Guide to How Google Search Works](https://developers.google.com/search/docs/fundamentals/how-search-works) — Google Search Central: Google explains how the three stages (crawling, indexing, and serving) work and how the ranking systems use hundreds of factors to determine the quality and relevance of pages.

## See Also

[[About the Leak]]  
[[Glossary]]
