# deebug.io — site

Single static page. No build step, no dependencies, no external requests. All CSS is
inline, the favicon is a data URI, and the CSP is `default-src 'none'` — the page loads
nothing from anywhere.

## Files

```
index.html                  the page
pgp.txt                     PLACEHOLDER — replace with the real armored public key
robots.txt  sitemap.xml
_headers                    Cloudflare Pages security headers (A+ on securityheaders.com)
.well-known/security.txt    RFC 9116 disclosure policy
```

## Deploy (Cloudflare Pages)

Wait for the zone to show **Active** in Cloudflare first — the delegation has to flip
before a custom domain can attach.

**Direct upload** — fastest, no repo needed:

1. Cloudflare dashboard → Workers & Pages → Create → Pages → Upload assets
2. Project name `deebug`, drag this `site/` directory in
3. Custom domains → add `deebug.io` and `www.deebug.io`

**Or via CLI:**

```sh
npx wrangler pages deploy site --project-name=deebug
```

Then delete the NameCheap parking A record (`192.64.119.91`) — Pages replaces it.

## Before it goes live

- [ ] Generate the PGP key, replace `pgp.txt`, publish the fingerprint
- [x] Mail on Google Workspace (domain alias of emoment.jp). MX `smtp.google.com`,
      SPF, DKIM (`google._domainkey`) and DMARC are live in Cloudflare.
      Addresses: `research@` (outbound), `security@` (disclosure), `support@` (reserved).
      Do NOT enable Cloudflare Email Routing — it would seize the MX records.
- [ ] Fill in profile links in `index.html` as handles are claimed — each is marked
      `<span class="pending">` with a comment above the list
- [ ] Bump `Expires` in `security.txt` annually — an expired one is worse than none
- [ ] Verify at securityheaders.com and hardenize.com

## Deliberately absent

No analytics, no fonts, no CDN, no JS. Every external request is a tracking surface and
a CSP exception, and this audience notices. Keep it that way.
