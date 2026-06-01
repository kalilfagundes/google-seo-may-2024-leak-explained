---
tags: [signal, entity, entity-recognition, nlp, medium-confidence]
cargo: [seo-specialist, writer]
confidence: medium
category: Entity
subcategory: Recognition
last_updated: 2026-04-23
---
# Entity — Entity Recognition

Automatic identification of entities (people, places, companies, concepts) in content using NLP. Google uses machine learning models to extract and classify entities in each document. A page about "Albert Einstein" mentions the entity person (Albert Einstein), countries (Germany, USA), concepts (Relativity). Google identifies all of them.

The leak exposes the Webref system that Google uses for entity linking — connecting entity mentions in a document to the Knowledge Graph. There is no field named "entityRecognitionScore," but there is a structure for entity analysis that feeds entity strength and topical relevance.

## In the Leak

Fields related to `webrefEntity`, `knowledgeGraphAnnotations`, `entityAliases`. The Webref system links entity mentions in text to the Knowledge Graph. Importance: it allows Google to understand not just textual keywords, but the semantic concepts behind them.

**Authorship is tracked as an entity relationship.** The leak confirms Google explicitly stores the **authors associated with a document as text**, and also checks whether an entity mentioned on the page is the same as the author of the page. This creates an entity graph where content, author, and topic are linked. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

This is supported by a broader system of **entity mapping and vector embeddings** documented in the leak. Google vectorizes both pages and authors, enabling it to evaluate whether an author has a consistent pattern of publishing on a specific topic — a direct algorithmic expression of Expertise in E-E-A-T.

## Confidence: Medium

System implicitly documented in entity processing fields, but exact use in ranking is not explicit. Impact is more indirect (improves semantic understanding) than direct.

## How It Works

When Google processes a document, NLP extracts: "This article mentions person 'Steve Jobs,' company 'Apple,' concept 'technological innovation,' place 'California'." Each mention is linked to the Knowledge Graph. A page that mentions many related concepts is seen as topically deeper.

Difference from keyword matching: query "who invented the iPhone" → you need to mention "Steve Jobs" textually. With entity recognition, mentioning "the creator of the iPhone" or "co-founder of Apple" is sufficient — Google understands they are the same entity.

**Author-entity detection** adds a second layer: Google checks whether the author of the page (from byline, structured data, or internal entity graph) is the same entity as a recognized expert in the topic. A cardiologist writing about heart disease triggers a stronger expertise signal than an anonymous author writing on the same topic. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## What to Do

**Clear entity mention:** When mentioning an important person/company/place, use the full name on first mention. Example: "Steve Jobs (co-founder of Apple)" instead of just "he."

**Disambiguation:** If "Apple" can mean the fruit or the company, provide context. "The company Apple" is clearer than just "Apple."

**Breadth vs. depth:** A page about "history of technology" that mentions 50 different entities has breadth. A page about "Steve Jobs's evolution" that explores details of 5-10 entities has depth. Both are valuable.

**Linking:** Links to relevant Knowledge Graph resources help. Linking "Steve Jobs" to their Wikipedia or Knowledge Panel improves entity linking.

**Establish author entity markup.** Since Google stores authors as text and checks entity-author relationships, implement `schema.org/author` on every article. Use a consistent author name that matches the person's Knowledge Panel or Wikipedia page if one exists. For niche topics without a KG presence, maintain a consistent author profile page on your own site with clear topical focus. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

**Build topical authority for your author entity.** The entity recognition system tracks whether an author consistently publishes within the same topic cluster. An author who writes about cardiology, then recipes, then finance is semantically inconsistent. An author who publishes consistently on cardiology builds a stronger entity-expertise signal over time.

## Official Reference

[Introduction to Structured Data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) — Google Search Central: Google explains how structured data helps identify and classify entities, improving semantic understanding of content for better ranking and presentation.

## See Also

[[Entity - Knowledge Graph]] — Entities live in the Knowledge Graph  
[[Content - Query Coverage]] — Entities are part of semantic coverage  
[[Content - EEAT]] — Author entity recognition feeds the Expertise signal in E-E-A-T  
[[NLP - Semantics and Intent]] — Entity recognition is one layer of the NLP pipeline  
[[Structured Data - Schema]] — `schema.org/author` and `schema.org/Person` markup feeds the author-entity detection system
