---
tags: [meta, leak, context, google]
category: Meta
last_updated: 2026-04-23
---
# About the Google API Content Warehouse Leak

## What Happened

On March 13, 2024, an automated bot called `yoshi-code-bot` made a routine commit to a public GitHub repository and accidentally published thousands of pages of Google's internal API documentation. The file was available for weeks without attracting attention.

On May 5, a former Google employee named Erfan Azimi sent the documents to Rand Fishkin, co-founder of SparkToro. Fishkin spent weeks verifying the authenticity of the material with former Google engineers before publishing his analysis on May 27. He also reached out to Mike King, CEO of iPullRank, for an independent technical review.

Both reached the same conclusion: the documents were authentic.

"In the last 25 years, no leak of this magnitude or detail has been reported from Google's search division," Fishkin wrote at the time.

## What the File Contains

The file documents **2,596 modules** with **14,014 attributes** describing Google's internal ranking systems — data structures, fields, types, and technical comments never intended for public consumption.

It is not the algorithm itself. It is the documentation of the data models that feed the algorithm. The distinction matters: you don't see the weights, you don't see the combination formulas. But you do see which signals exist, which fields are stored, and in many cases what each one represents.

## Why to Believe It

The authenticity of the leak was reinforced in three independent ways.

First, former Google engineers recognized the internal structure of the documents — naming conventions, proto patterns, comments. Not the kind of thing someone fabricates from the outside.

Second, the U.S. antitrust case against Google (U.S. vs. Google) had, in February 2025, testimony that explicitly confirmed the use of Navboost as one of the main ranking signals — exactly as described in the leak.

Third, the internal consistency of the file is too high to be fabricated. Fields appearing in one module were correctly referenced in others, with consistent data types across hundreds of modules.

## What Was Revealed

Some findings confirmed what the SEO community had suspected for years but Google publicly denied. Others were genuinely new.

**Navboost** is the system that aggregates click signals into ranking. It distinguishes `goodClicks` (the user stayed on the page) from `badClicks` (returned to the SERP in seconds) and `lastLongestClicks` (longest dwell time). These signals are collected via Chrome and aggregated at multiple levels — by page, host, domain, and geographic area. The antitrust process confirmed that Navboost is "one of the most important signals" in Google's ranking.

**SiteAuthority** is an authority metric calculated per site, something Google representatives publicly denied for years. The field explicitly appears in the leak as part of `CompressedQualitySignals` — the central quality signals used in the scoring system.

**Chrome data** is more central than Google admitted. The leak details how browsing history, logged-in sessions, and click patterns in Chrome form the backbone of Navboost. The distinction between "squashed" clicks (discarded as spam-like) and "unsquashed" (valid) suggests a sophisticated signal filtering system.

**New sites face a probationary period.** The leak contains fields indicating differentiated treatment for new domains — something Google also publicly denied and that now has technical backing.

## What the Leak Does Not Show

The relative weights between signals are not documented. That Navboost exists is fact. Whether it accounts for 10% or 40% of the final ranking, no one knows.

The combination formulas also do not appear. The file describes the ingredients, not the full recipe.

What you get from the leak is understanding which signals exist and what each represents — measuring your own site still depends on Search Console, Analytics, and testing.

## Recommended Reading

- [[Confidence Methodology]] — how we assess the solidity of each signal in this base
- [[Glossary]] — technical terms from the leak explained
- [[Engagement - Navboost and Clicks]] — the most discussed signal from the leak
