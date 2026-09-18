# Response headers

`_headers` is **Cloudflare Pages** syntax. GitHub Pages ignores it — it does not
support custom response headers at all.

While this site is served from GitHub Pages, the CSP / HSTS / frame-options
headers in `_headers` are NOT applied. To get them back, either:

1. Move hosting to Cloudflare Pages (the file then works as written), or
2. Proxy the domain through Cloudflare (orange cloud) and recreate the headers
   as a Transform Rule → Modify Response Header ruleset on the zone.

Until one of those is done, assume the site ships with GitHub's default headers.
