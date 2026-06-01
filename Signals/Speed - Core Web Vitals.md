---
tags: [signal, speed, web-vitals, performance, high-confidence]
cargo: [developer, seo-specialist]
confidence: high
category: Speed
subcategory: Core Web Vitals
last_updated: 2026-04-23
---
# Speed — Core Web Vitals

Core Web Vitals are three user experience metrics that Google uses as a ranking factor. The leak exposes explicit fields in the `IndexingVoltCoreWebVitals` module: `lcp`, `cls`, `inp`. In March 2024, Google replaced FID (First Input Delay) with INP (Interaction to Next Paint), reflecting a shift in priority from only the first interaction to all page interactions. Google collects this data in real time via the Chrome User Experience Report (CrUX) — Chrome users who visit your site automatically send metrics to Google, and this data is aggregated.

Since 2021, Google has confirmed that Core Web Vitals affect ranking. It is not an isolated factor — excellent content can still outrank a faster competitor — but for technically and content-wise equivalent pages, Core Web Vitals is a tiebreaker.

## In the Leak

The leak confirms that Google stores:

```
IndexingVoltCoreWebVitals:
  lcp: [value in ms]
  cls: [value between 0 and 1]
  inp: [value in ms]
```

These fields are populated with CrUX data. Google does not use synthetic data (Lighthouse) as a ranking factor — it uses real data from real Chrome users. This is critical to understand: your page may have a perfect Lighthouse score, but if real Chrome users have poor Core Web Vitals (or insufficient data in CrUX), Google penalizes it.

The **Htmlrender** pipeline documented in the leak (part of the document quality system) overlaps with Core Web Vitals data collection. Htmlrender pre-renders pages at indexing time to assess DOM structure, rendering completeness, and visual stability — the same properties measured by CLS and LCP. A page that renders inconsistently in Htmlrender is likely to have poor CrUX CLS scores as well. *(Source: [iPullRank](https://ipullrank.com/google-algo-leak))*

## Confidence: High

Google officially disclosed Core Web Vitals in 2021 and confirmed multiple times that it is a ranking factor. The leak explicitly documents the fields used. The evidence is direct and publicly verifiable.

## How to Measure on Your Site

Use PageSpeed Insights (https://pagespeed.web.dev/), which combines CrUX data with Lighthouse analysis. Enter your domain. The result shows:

- **LCP (Largest Contentful Paint):** Time until the largest element (text, image) loads and becomes visible. Measured in seconds
  - Good: < 2.5s
  - Needs improvement: 2.5-4s
  - Poor: > 4s

- **CLS (Cumulative Layout Shift):** Amount of unexpected visual changes during loading. Measured from 0 to infinity, the lower the better
  - Good: < 0.1
  - Needs improvement: 0.1-0.25
  - Poor: > 0.25

- **INP (Interaction to Next Paint):** Time from user interaction (click, tap) until the page visually responds. Measured in milliseconds
  - Good: < 200ms
  - Needs improvement: 200-500ms
  - Poor: > 500ms

All three need to be in the green to pass. Google evaluates at the 75th percentile — not the maximum nor the average, but where 75% of traffic has a good experience.

Use Google Search Console to see the aggregate status of your site (Search Console > Page Experience > Core Web Vitals). If there is insufficient data in CrUX (< 100 clicks/day), the metric stays pending — in that case, optimize anyway, since the more traffic, the more data.

## What to Do

**For LCP (fast loading):**
- Compress images aggressively (use WebP, tools like TinyPNG)
- Implement lazy loading for below-the-fold images
- Minimize or split render-blocking CSS/JavaScript
- Use CDN to serve assets globally (Cloudflare, AWS CloudFront)
- Optimize server — respond to requests in < 600ms (TTFB)

**For CLS (avoid visual shifts):**
- Fix container heights before content loads (CSS `aspect-ratio` or explicit `height`)
- Avoid inserting ads, pop-ups, or dynamic content above the fold after initial loading
- For animations, use `transform` or `opacity` instead of `margin`/`top`/`left` (which cause reflow)
- For custom fonts, use `font-display: swap` to avoid shift when font loads

**For INP (respond quickly):**
- Minimize blocking JavaScript — split into smaller chunks
- Optimize event handlers (clicks, scroll)
- For long operations, use `setTimeout` to break into tasks
- Use requestAnimationFrame for interaction animations

Test regularly. PageSpeed Insights is quick and shows priorities. Chrome DevTools (Performance tab) allows deep analysis. WebPageTest enables testing on real connections and devices.

## See Also

[[Speed - HTTPS SSL]]  
[[Authority - Document Quality]] — Rendering quality from Htmlrender overlaps with Core Web Vitals data
