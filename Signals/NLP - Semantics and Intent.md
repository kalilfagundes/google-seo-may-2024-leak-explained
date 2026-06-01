---
tags: [signal, nlp, semantics, intent, natural-language, medium-confidence]
cargo: [seo-specialist, writer]
confidence: medium
category: NLP
last_updated: 2026-04-23
---
# NLP — Semantics and Intent

Google has 1,397 NLP models in the leak — the second largest category of documented models. These models do not look for exact keywords, but for semantic meaning. Google tokenizes queries (breaks them into words), identifies part-of-speech (nouns, verbs, adjectives), analyzes grammatical dependencies and maps words into embeddings where synonyms are close in vector space. This means "car," "automobile," and "vehicle" are treated as semantically equivalent, not as competing terms.

Intent detection works on top of this semantic understanding. Google does not just recognize that a query contains the word "buy" — it understands the grammatical context, the entities involved (brand, category, attributes) and the transactional or informational intent. This understanding allows Google to rank pages that respond to the intent without requiring exact keyword matching.

## In the Leak

Google's NLP systems do not have documentation as explicit as other signals, but the leak confirms:

- **Morphosyntactic parsing:** part-of-speech and grammatical dependency analysis
- **Entity Recognition:** detection of names, brands, locations within queries and content
- **Word Embeddings:** mapping words in vector space to find semantic similarity
- **Intent:** binary or multi-class classification of queries as informational, navigational, transactional, local
- **`siteFocusScore`** — a scalar generated from site2vec embeddings measuring how tightly a site concentrates on a single topic
- **`siteRadius`** — measures how far individual pages diverge from the site's core topic vector; high siteRadius = semantically off-topic page

These two embedding fields confirm Google holds a **vector model of what a site is "about"** at the site level, not just at the keyword level. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

**YMYL classifiers** are explicitly documented with dedicated scoring for `YMYL Health` and `YMYL News`. For queries never seen before, Google predicts YMYL classification before serving — these are called **"fringe queries."** YMYL scoring operates at the **chunk level**, indicating embedding-based classifiers rather than rule-based heuristics. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

**Gold Standard Documents** are referenced as pages with "human-labeled" annotations (vs. automatically labeled), used to calibrate scoring models. Their existence alongside automatic annotations confirms a hybrid human+ML quality evaluation system. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: Medium

The existence of 1,397 NLP models is documented in the leak. Google publicly confirmed in 2019 that BERT (Bidirectional Encoder Representations from Transformers) was integrated into the search algorithm. However, the leak does not detail the exact workings of these models or how they convert to ranking signals. The inference that these models affect ranking is reasonable (why would Google maintain them if they weren't used?), but it is not explicitly described in the document as a ranking factor.

## How to Measure on Your Site

You cannot access or directly measure NLP scores, but you can validate whether your site is being semantically understood through:

- **Search Console > Performance:** See which queries bring your site up. If you appear in queries that don't contain your exact keywords, it is a sign that Google understood your semantics
- **Rich Results Test:** Check if Google can extract and validate schema markup (entities, structured content)
- **SERP Analysis:** Compare your pages with those ranking for the same query — does Google consider them semantically equivalent?
- **Featured Snippet eligibility:** Do you appear in featured snippets? That is a sign that Google understood your intent

## What to Do

Write content naturally. Use synonyms, related terms, and variations. If you write about "SEO," it is natural to mention "search engine optimization," "search ranking," "organic positioning."

Explicitly respond to the query intent. If the query is "how to improve SEO," structure the content pedagogically. If the query is "free SEO tool," produce a comparison with prices. Content structure reflects intent.

Use headers (H2, H3) to structure semantically. Well-hierarchized content is easier for NLP models to process.

Include named entities when relevant. Mention the full name and provide context — "Apple" can be the company or the fruit, but mentioning "iPhone" or "iOS" disambiguates.

**Keep topical focus tight.** `siteFocusScore` and `siteRadius` confirm Google evaluates semantic coherence at the embedding level. Publishing off-topic content measurably increases `siteRadius` and weakens domain authority for core topics.

**For YMYL topics** (health, finance, news), the scoring pressure is higher. YMYL classifiers generate dedicated scores at the content chunk level. Strong EEAT signals, accurate information, and up-to-date content are critical because YMYL pages face a higher quality threshold. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## See Also

[[Content - Query Coverage]] — NLP intent maps directly to query coverage requirements  
[[Voice Search - Assistant and Featured Snippets]] — The Assistant system sits on top of NLP processing  
[[Authority - Document Quality]] — Semantic HTML structure feeds the NLP parsing pipeline
