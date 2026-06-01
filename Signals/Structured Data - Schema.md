---
tags: [signal, structured-data, schema.org, markup, high-confidence]
cargo: [developer]
confidence: high
category: Structured Data
last_updated: 2026-04-23
---
# Structured Data — Schema.org

Standard vocabulary for semantically annotating content. Schema is not a direct ranking factor — Google does not rank pages higher for having schema. But schema helps Google better understand what a page is, which enables better query matching, featured snippets, and rich results on the SERP that affect CTR.

Schema.org is a set of standardized terms (Article, Product, FAQPage, Event, etc.) that you add as JSON-LD or microdata in HTML. When Googlebot sees valid schema, it processes the structured data and stores it as document metadata. This allows Google to display rich snippets (star ratings, prices, etc.) that increase CTR compared to plain snippets.

## In the Leak

Schema does not appear as a named ranking field ("schemaScore" or similar). But it appears as part of content processing — Alexandria (semantic analysis) and Mustang (classification) use structured data to better understand the document. There are also "rich results eligibility" signals that determine whether a page is a candidate for a featured snippet or rich result.

Schema markup for **product reviews** is directly connected to the `productReviewP*` fields in `CompressedQualitySignals`. The structured data from `Product` and `Review` schema feeds into the evaluation that generates `productReviewPPromotePage`, `productReviewPDemoteSite`, and related signals. Sites with valid product review schema that also have high-quality review content are more likely to receive promotion signals; sites with schema but low-quality or non-expert reviews may still receive the demotion. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

**FAQPage** and **HowTo** schema feed directly into the **KnowledgeAnswers** system — the 1,685-model pipeline that powers featured snippets and Google Assistant responses. Valid FAQ schema gives Google a pre-structured question-answer pair it can extract directly for zero-click results. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: High

Processing documented, Google public confirmation that schema is not a direct ranking factor, but the indirect impact (via featured snippets and rich results) is real and observable.

## How It Works

Google processes schema to extract data structure. Example: Article schema with `author`, `datePublished`, `headline` lets Google know exactly who wrote it, when, and what the authorized title is (vs. having to parse HTML). This improves indexing reliability.

For featured snippets, schema (especially FAQPage) increases the probability of appearing — Google knows exactly what the questions and structured answers are, making display easier.

For rich results (Product with rating, Event with location), the visual snippet dramatically improves CTR.

## How to Measure on Your Site

There is no direct "schema score" metric. But there are proxies:

- **Rich results in SERP:** Search your keywords on Google. Do your pages appear with stars, prices, or just plain text? If competitors have rich results and you don't, schema may be the gap
- **Featured snippet eligibility:** Search "your_keyword" on Google. Is there a featured snippet box? If so and you are not in it, FAQPage schema may help
- **Search Console:** "Enhancements" > "Rich results" tab shows if Google detected valid schema on your site
- **Schema.org validator:** Look for errors in implementation — invalid schema is ignored

Indirect metric: featured snippet = ~30% more clicks than regular position 1. If you implement FAQ schema and gain a featured snippet, the boost is measurable.

## What to Do

**By page type:**

Blog article: `<script type="application/ld+json">` with Article schema including `headline`, `author`, `datePublished`, `dateModified`, `articleBody` (partial). Lets Google display byline, date, and consider for featured snippets.

FAQ page: FAQPage schema with an array of Question/Answer pairs. Increases chance of featured snippet or being used in Google Assistant/voice search.

Product page: Product schema with `name`, `price`, `priceCurrency`, `aggregateRating` (if it has reviews). Enables star rating on the SERP.

Event: Event schema with `name`, `startDate`, `location`. Enables rich result with date and place.

**Validation:** Use the [schema.org Validator](https://validator.schema.org) or Search Console "Rich Results" report to check for errors. Invalid schema is ignored.

**Priority:** Article + FAQPage cover 80% of cases. Product + Event if applicable. Implementing correct schema is 2-3 hours of work per page.

Common mistake: confusing "schema helps ranking" with "schema is a ranking factor." Schema does not put you in position 1 directly. But the featured snippet or rich result that schema enables increases CTR and engagement, which feeds Navboost.

## Official Reference

[Introduction to Structured Data](https://developers.google.com/search/docs/appearance/structured-data/intro-structured-data) — Google Search Central: Google explains the use of schema.org and structured data to help better understand content, enabling rich results and better SERP presentation.

## See Also

[[Content - Query Coverage]] — Schema helps Google better understand whether the page covers the topic  
[[Engagement - Navboost and Clicks]] — Featured snippets from schema increase CTR  
[[Voice Search - Assistant and Featured Snippets]] — Schema is critical for voice search
