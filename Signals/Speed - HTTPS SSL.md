---
tags: [signal, speed, https, ssl, security, high-confidence]
cargo: [developer]
confidence: high
category: Speed
subcategory: Security
last_updated: 2026-04-23
---
# Speed — HTTPS SSL

HTTPS has been a confirmed ranking factor since August 2014. The leak exposes simple boolean fields: `displayUrlIsHttps` and `IndexingBadSSLCertificate`, showing that Google explicitly stores whether a page is served via valid HTTPS or not. However, Google is clear that HTTPS is a "very lightweight signal" — it affects less than 1% of global queries. When other ranking factors are equal, HTTPS can be the tiebreaker, but it will never make a poor page rank above an excellent one just for having an SSL certificate.

Google encourages HTTPS for user security reasons — encrypted communication reduces the risk of man-in-the-middle attacks. Since 2016, Chrome marks HTTP sites as "Not secure" in the address bar, creating market pressure beyond the ranking factor itself.

## In the Leak

The specific fields are:

- `displayUrlIsHttps` (boolean): Is the page served via HTTPS?
- `desktopDisplayUrlIsHttps` (boolean): Is the desktop version HTTPS?
- `IndexingBadSSLCertificate` (flag): Is the SSL certificate invalid?

These fields are simple booleans — there is no gradual score. Either the page has valid HTTPS, or it doesn't. Google validates the certificate chain (whether the certificate was issued by a recognized authority) and checks expiration. Invalid certificates (self-signed, expired, domain mismatch) are explicitly flagged.

## Confidence: High

Google officially announced HTTPS as a ranking factor. The leak confirms with explicit fields. The evidence is direct and publicly verifiable — inspect any site with HTTPS and see the valid certificate in the browser bar.

## How to Measure on Your Site

Check whether your site is HTTPS:

- **In the browser address bar:** Look for the padlock icon and "https://" in the URL
- **SSL Labs (https://www.ssllabs.com/ssltest/):** Detailed analysis of certificate quality. Enter your domain and get an A-F score
- **Chrome DevTools (F12 > Security):** See the certificate and validate the certification chain
- **Search Console:** Check for certificate warnings in the Security tab

Check for "mixed content" (HTTPS page loading HTTP assets):

- **Chrome DevTools (F12 > Console):** Look for "mixed content blocked" messages
- **PageSpeed Insights:** Flags mixed content
- **Manually:** Inspect all images, scripts, stylesheets — all need to be HTTPS

## What to Do

If your site is still not HTTPS, migrate immediately. Let's Encrypt offers free SSL certificates — no legitimate reason to be without HTTPS in 2026.

Migration steps:

1. Acquire an SSL certificate (Let's Encrypt is free; Comodo and DigiCert are paid but with more features)
2. Install on your hosting/web server (hosting support can do this)
3. Configure HTTP → HTTPS redirect via .htaccess (Apache) or nginx.conf (Nginx)
4. Update internal references: links between pages, redirects, canonical tags — all must use HTTPS
5. Update in Google Search Console: add the HTTPS property as a separate property
6. Submit new sitemap with HTTPS URLs

If your site is already HTTPS, eliminate mixed content:

- Replace all `http://` with `https://` in assets
- For CDN and third-party services, check if they offer HTTPS (most do)
- If a third-party resource doesn't offer HTTPS, consider an alternative or proxy it through your HTTPS server

Keep certificate updated. Set up automatic renewal (Let's Encrypt renews automatically every 90 days). Expired certificates are flagged by Google as `IndexingBadSSLCertificate`.

## See Also

[[Speed - Core Web Vitals]]  
[[Document Quality - Rendering]]
