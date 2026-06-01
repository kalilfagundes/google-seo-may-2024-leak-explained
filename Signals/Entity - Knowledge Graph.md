---
tags: [signal, entity, knowledge-graph, brand, medium-confidence]
cargo: [seo-specialist, marketing-director]
confidence: medium
category: Entity
subcategory: Knowledge Graph
last_updated: 2026-04-23
---
# Entity — Knowledge Graph

Google's database of entities and relationships. When you search "Steve Jobs," Google displays a Knowledge Panel with photo, bio, dates, and links to related articles. All of this comes from the Knowledge Graph. Presence in the Knowledge Graph is not a direct ranking factor, but it is a recognition signal that benefits brand and CTR.

A page about an entity recognized in KG ranks better because: (1) Google knows exactly what the page is about, (2) the page can appear in the Knowledge Panel, (3) CTR improves due to visual presence. The leak shows fields like `knowledgeGraphAnnotations` and `entityScore` that capture entity strength.

## In the Leak

Fields related to `knowledgeGraphAnnotations`, `entityScore`, and connections to the Knowledge Graph. The system stores entity strength and relationship validation.

The `entityScore` field quantifies how strongly a page is associated with a specific Knowledge Graph entity. A higher score means Google is more confident about what entity the page represents. Pages with a strong entity score are more likely to be surfaced in Knowledge Panels and direct-answer results. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

The KnowledgeAnswers system documented in the leak — which powers featured snippets and Assistant responses — resolves entity-based queries by pulling from the Knowledge Graph first. This means pages that are **the canonical source for a KG entity** have a structural advantage for zero-click and voice search results. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: Medium

Processing documented, public confirmation about Knowledge Graph, but exact weight in ranking is not stated in the leak.

## How It Works

When a page is about an entity (person, company, place, brand), Google attempts to link it to the Knowledge Graph. If it finds a match, it pulls KG data (photo, bio, dates) for use in the Knowledge Panel. If it doesn't find one, it creates a vacant KG entry awaiting data.

Pages that best describe an entity (complete biography, certifications, publications) gain a boost because Google uses them to validate KG data.

The **KnowledgeAnswers** pipeline (1,685 models documented in the leak) uses entity resolution from the Knowledge Graph as its first step when answering direct queries. Entities that are well-represented in the KG with high `entityScore` are matched faster and with greater confidence — giving the pages that feed them an advantage in featured snippets and voice answers. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## What to Do

**For person/expert:** Complete Wikipedia (if applicable), create a Knowledge Panel profile, add author schema structured data.

**For company/brand:** Keep Google My Business updated (address, hours, photos, reviews). Add Organization schema with logo, location, contact.

**For content about an entity:** Linking to the Knowledge Panel or the entity's Wikipedia improves entity linking. Use `rel="author"` or `rel="organization"` when relevant.

## Official Reference

[Introduction to Structured Data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) — Google Search Central: Google describes how structured data helps feed the Knowledge Graph, enabling better understanding of entities and their presence in enriched search results.

## See Also

[[Entity - Entity Recognition]] — Identification of entities in text  
[[Content - EEAT]] — EEAT benefits from KG presence  
[[Links - Quality]] — Links from KG pages validate authority  
[[Voice Search - Assistant and Featured Snippets]] — KnowledgeAnswers resolves entities from this graph for direct answers
