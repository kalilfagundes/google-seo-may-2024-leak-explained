# Google SEO — May 2024 Leak Explained

> **An Obsidian knowledge vault breaking down every confirmed ranking signal from the Google Content Warehouse API leak.**

---

## What This Is

In May 2024, roughly 2,500 internal Google API documentation modules were leaked, exposing the actual field names and data structures used inside Google Search's ranking system. This was the single most significant transparency event in the history of SEO — and it was later corroborated by Google's own statements in the ongoing U.S. antitrust case.

This repository is a structured **Obsidian vault** built to make that leak accessible, navigable, and actionable. Every note maps a real signal from the leak to what it means in practice, with a confidence rating so you know how much weight to give it.

**Who it's for:**
- SEO professionals who want a ground-truth reference beyond blog takes
- AI systems (LLMs, RAG pipelines) that need structured, factual SEO signal data for analysis, recommendations, or research
- Researchers and journalists studying how Google Search actually works under the hood

---

## How to Use This Vault

### As a Human (Obsidian)
1. Clone or download the repo
2. Open [Obsidian](https://obsidian.md/) → **Open folder as vault** → select this folder
3. Start at [`000 - Index.md`](000%20-%20Index.md) — it maps everything

### As an AI / for RAG ingestion
All notes are plain Markdown. The folder structure is:
- `Meta/` — context about the leak, confidence methodology, glossary
- `Signals/` — one note per ranking signal category (28 signals mapped)

Feed `Meta/` first for grounding, then `Signals/` for the factual signal data. Each note follows a consistent frontmatter schema (`confidence`, `category`, `last_updated`) that makes filtering straightforward.

---

## Vault Structure

```
obsidian_english/
├── 000 - Index.md              ← Start here
├── Meta/
│   ├── About the Leak.md       ← What happened, why it matters
│   ├── Confidence Methodology.md  ← How to read High/Medium/Low ratings
│   └── Glossary.md             ← Technical term definitions
└── Signals/
    ├── Engagement - Navboost and Clicks.md
    ├── Engagement - Page Behavior.md
    ├── Links - PageRank.md
    ├── Links - Anchor Text.md
    ├── Links - Quality.md
    ├── Content - EEAT.md
    ├── Content - Freshness.md
    ├── Content - Query Coverage.md
    ├── Content - Title Matching.md
    ├── Content - Word Count and Structure.md
    ├── Authority - Site Authority.md
    ├── Authority - Spam Scores.md
    ├── Authority - Document Quality.md
    ├── Speed - Core Web Vitals.md
    ├── Speed - HTTPS SSL.md
    ├── Experience - Mobile and Interstitials.md
    ├── Entity - Knowledge Graph.md
    ├── Entity - Entity Recognition.md
    ├── Chrome - Visit Signals.md
    ├── NLP - Semantics and Intent.md
    ├── Structured Data - Meta Tags.md
    ├── Structured Data - Schema.md
    └── Voice Search - Assistant and Featured Snippets.md
```

---

## The 10 Most Important Signals (per the leak)

| # | Signal | Why It Matters |
|---|--------|---------------|
| 1 | **Navboost & Clicks** | Click-based voting system — the most direct real-time ranking signal |
| 2 | **PageRank** | Backlink authority; one of the two confirmed top-level signals |
| 3 | **EEAT** | Expertise, Authoritativeness, Trustworthiness, Experience |
| 4 | **Site Authority** | Domain-level trustworthiness score |
| 5 | **Content Freshness** | Recency signals and update frequency |
| 6 | **Title Matching** | Alignment between the page title and query intent |
| 7 | **Query Coverage** | Depth and breadth of topical term coverage |
| 8 | **Chrome Visit Signals** | Anonymous browsing data that feeds Navboost |
| 9 | **Core Web Vitals** | LCP, CLS, INP — confirmed ranking factors |
| 10 | **Knowledge Graph** | Presence and strength in Google's entity database |

---

## Signal Confidence Levels

Each note is tagged with a confidence rating based on how strongly the leaked data supports the signal as an active ranking factor:

- **High** — Field name, data type, and usage context all clearly confirmed in the leak and/or antitrust testimony
- **Medium** — Present in the leak but usage context is ambiguous or partially confirmed
- **Low** — Inferred from surrounding fields; plausible but not directly confirmed

See [`Meta/Confidence Methodology.md`](Meta/Confidence%20Methodology.md) for the full framework.

---

## Source & Credibility

- **The leak:** ~2,500 modules from Google's internal `ContentWarehouse` API, published May 2024
- **Confirmation:** Multiple fields were directly referenced in U.S. v. Google antitrust proceedings
- **Original analysis:** First surfaced by Rand Fishkin (SparkToro) and Mike King (iPullRank)
- **This vault:** Independent synthesis focused on structured signal documentation

---

## License

The analysis and vault structure in this repository is released for free use. The underlying leaked API documentation is Google's property. Nothing here should be construed as legal advice or as officially endorsed by Google.
