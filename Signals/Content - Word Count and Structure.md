---
tags: [signal, content, word-count, depth, structure, high-confidence]
cargo: [writer]
confidence: high
category: Content
subcategory: Volume
last_updated: 2026-04-23
---
# Content — Word Count and Structure

Word count alone is not a direct ranking factor. Google does not look for "2000+ words" as a criterion. But word count correlates with depth, and depth matters. A 500-word article that completely covers a topic ranks better than a 3,000-word article that is 60% filler. That said, in direct competition, longer content tends to rank better because it has more room to cover the topic in detail.

The leak exposes fields like `wordCount: integer()`, `nonAbstractWordCount: integer()`, and structure evaluation via header detection. Google also measures "content effort" — use of images, videos, tables, structured data — which together with volume contributes to perceived quality.

## In the Leak

The `wordCount: integer()` field records the total number of words. `nonAbstractWordCount: integer()` filters boilerplate words (navigation, footer, sidebars), counting only substantive content. There is also documented structure analysis in modules that detect the presence of H1, H2, lists, bold/italic — signals that content was formatted for readability.

The leak documents that **documents in the Mustang system are truncated at a maximum token count**. This means very long pages are not fully processed — content beyond the token limit may not be included in quality or relevance scoring. Practically, critical content should appear early in the document, not buried after thousands of words of body text. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

A **keyword stuffing score** is explicitly named in the leak as a distinct field, confirming that Google does not just penalize keyword stuffing as a pattern — it has a dedicated quantitative measure for it. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

**Weighted font size of terms and links** is tracked. This means that text displayed at a larger visual size (headings, bold) is given more weight than body text in relevance calculations — confirming that heading structure is not just a user experience concern but a direct content signal. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: High

Explicit fields, obvious empirical validation (superficial 300-word content loses to deep 2000-word content on competitive queries), and clear logic — more content allows for more complete topic coverage.

## How It Works

Google does not have a threshold ("articles shorter than 800 words are bad"). It analyzes: is it possible to adequately cover this topic in N words? The query "how to cook an egg" deserves 300-500 words. The query "complete history of machine learning" deserves 3,000+. Quality matters more than quantity, but the quantity that enables quality is necessary.

Structure matters as much as volume. A 2,000-word article with one long continuous paragraph and no headers is harder to scan, scoring lower than the same size well-formatted with clear headers, lists, bold key points.

Google measures "content effort" — presence of images, videos, tables, structured data, citations. A 1,500-word article with 5 images and a comparison table indicates more effort than 1,500 words with none.

## How to Measure on Your Site

No direct metric in GSC. But there is analysis:

- **Average article size:** Use a tool like Yoast or SEMrush to measure. Does your site average 800 words vs. competitors with 1,500? Significant gap?
- **Structure:** Search "your keyword intitle:your_title" in the top 10 and analyze how many headers each has. If all use 4-5 headers and you use 2, there's a gap
- **Effort signals:** Do your articles have images? Tables? Do you cite sources? Are competitors doing more of this?

Indirect metric: if a page is in position 5-7 but competitors in 1-3 have visibly longer and more structured content, expansion may help.

## What to Do

**Do not** rewrite an excellent 600-word article into 2,000 generic words. Only add content if there is more value to deliver.

**Do:** For each page in your top 10, compare size and structure with the page in position 1-2. If you are in position 5 with 800 words and position 1 has 1,500 with 4 headers, there is room for improvement. Add: more comparisons, specific use cases, uncovered FAQs, or technical details.

**Minimum structure:** Every article deserves an H1 (single main title), 2-3 H2s (main sections), possibly H3s (subtopics). No headers = hard to scan.

**Effort signals:** Add relevant images (not generic stock). Tables for comparisons. Cite original sources with links. Structured data (FAQ schema, Article schema). Embedded video (if relevant). All of this signals effort.

**Size by type:**

Technical blog post: 1,000-2,000 words is the sweet spot. Less and it seems superficial on complex topics. More and it can be verbose.

Tutorial/how-to: 800-1,500. Straight to the point without digression.

Deep analysis: 2,500+. Deserves detail.

News/breaking: 300-800. News doesn't need a saga.

Review: 1,000-2,000. Necessary to cover various angles.

There is no "perfect" — Google wants "as long as necessary to completely answer, no more."

## Official Reference

[Creating Helpful, Reliable, People-First Content](https://developers.google.com/search/docs/fundamentals/creating-helpful-content) — Google Search Central: Google emphasizes that quality content must be deep, well-structured, and create genuine value for users, rather than just filling word volume.

## See Also

[[Content - Query Coverage]] — Long content allows for more term coverage  
[[Engagement - Page Behavior]] — Clear structure affects time on page  
[[Content - EEAT]] — An expert writes with more depth
