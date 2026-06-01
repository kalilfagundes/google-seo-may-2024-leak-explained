---
tags: [signal, voice-search, assistant, featured-snippets, direct-answers, high-confidence]
cargo: [seo-specialist, writer, content-strategist]
confidence: high
category: Voice Search
last_updated: 2026-04-24
---
# Voice Search — Assistant and Featured Snippets

Google's `AssistantVerticalsCommon` and `KnowledgeAnswers` systems together represent the single largest documented system in the leak, with 1,685 models. This scale confirms that optimizing for voice search, direct answers, and featured snippets is not an edge case — it is a primary ranking surface. The system handles three distinct jobs: selecting position-zero featured snippets, resolving direct answer queries (facts, calculations, lists), and understanding conversational intent for Google Assistant.

## In the Leak

Key fields and structures from this system:

- **`KnowledgeAnswersEntityType`** and **`KnowledgeAnswersBooleanType`** — the base types used when extracting direct answers. Boolean (yes/no), entity (person, place, thing), and numeric answers are each handled by separate extraction paths.
- **`KnowledgeAnswersIntentQueryAnnotationLayerSignals`** — signals that annotate and classify conversational query intent. This feeds directly into assistant ranking decisions.
- **`KnowledgeAnswersIntentModifiers`** — detects intent-modifying words ("how," "when," "where," "why") that change how a query must be answered.
- **`KnowledgeAnswersDialogReferentialResolution`** — resolves references across a multi-turn conversation (e.g., "tell me more about it" following a prior entity query).
- **`AssistantVerticalsCommonContactMatchSignal`** — an assistant-specific ranking score applied when matching content to voice queries.
- **`NlpSemanticParsingLocalBusinessType`** — classifies local intent within voice queries, routing them toward Geostore results rather than web results.

Featured snippet selection is a sub-pipeline within this system. The ML classifier evaluates candidates based on content structure (paragraph, list, table), source authority via `siteAuthority`, and recency via `freshnessEncodedSignals`.

## Confidence: High

The `KnowledgeAnswers` and `AssistantVerticalsCommon` model counts (1,685 combined) are explicitly documented in the leak. The named intent fields (`KnowledgeAnswersIntentModifiers`, `KnowledgeAnswersDialogReferentialResolution`) are documented structures. Featured snippet ranking behavior is widely confirmed through empirical observation and the antitrust proceedings.

## How to Measure on Your Site

- **Search Console → Performance → filter by question queries** (who, what, when, where, how, why). High-impression question queries are your voice search candidates.
- **Featured snippet tracking:** Ahrefs or SEMrush show which pages hold featured snippets. Track these positions monthly.
- **Rich Results Test:** Validates schema markup (FAQ, HowTo, Speakable) that feeds the `KnowledgeAnswers` extraction pipeline.
- **Conversational query appearance:** If your page ranks for "best [X]" but not "what is the best [X]," you are missing the intent modifier layer.

## What to Do

**Answer questions in 40–60 words.** The featured snippet extractor looks for concise, self-contained answers. Open each section with a direct answer paragraph before expanding into detail.

**Use structured formats.** `KnowledgeAnswers` extracts different answer types from different content structures. Steps should be `<ol>`, options should be `<ul>`, comparisons should be `<table>`. A numbered process written as a paragraph will not be classified as a list answer.

**Cover all intent modifiers.** For any topic, ensure the page addresses: *what* it is, *when* to use it, *how* to do it, *why* it matters. Each modifier maps to a `KnowledgeAnswersIntentModifiers` classification — missing one leaves a voice answer gap.

**Add Speakable schema.** The `speakable` property in schema.org marks which paragraphs are optimized for audio delivery by the Assistant. Apply it to the 2–3 most important answer paragraphs per page.

**Resolve referents clearly.** `KnowledgeAnswersDialogReferentialResolution` handles "it," "they," "there" in follow-up queries. Ambiguous pronouns in your content break entity linking in multi-turn conversations — use entity names on repeated mention.

**Optimize for local voice intent.** `NlpSemanticParsingLocalBusinessType` routes "near me" and location-qualified queries to Geostore. If you have local pages, include explicit entity names (city, neighborhood, service type) so the classifier routes correctly.

## Official Reference

[Featured snippets and your website](https://developers.google.com/search/docs/appearance/featured-snippets) — Google Search Central: Documents how Google selects featured snippets, including the importance of structured content and direct, concise answers.

## See Also

[[NLP - Semantics and Intent]] — The NLP layer that processes queries before Assistant ranking  
[[Entity - Knowledge Graph]] — Entities extracted by KnowledgeAnswers live in the Knowledge Graph  
[[Content - Query Coverage]] — Covering the full query including intent modifiers feeds this system  
[[Structured Data - Schema]] — Speakable and FAQ schema feed directly into KnowledgeAnswers extraction  
[[Authority - Site Authority]] — Source authority is a factor in featured snippet candidate selection
