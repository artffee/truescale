# Deploying TrueScale

Static site — no build step. Upload the repo to any static host (Netlify, Cloudflare Pages, GitHub Pages, S3+CloudFront). Before going live, do these two find-and-replace passes.

## 1. Your domain

Replace `https://ruleler.vercel.app/` with your real URL (keep the trailing slash) in:

| File | Where |
|------|-------|
| `index.html` | `<link rel="canonical">` and `<meta property="og:url">` |
| `sitemap.xml` | `<loc>` |
| `robots.txt` | `Sitemap:` line |

## 2. Google AdSense

After your AdSense account is approved, replace these placeholders in `index.html`:

| Placeholder | Occurrences | Replace with |
|-------------|-------------|--------------|
| `ca-pub-XXXXXXXXXXXXXXXX` | 3 (loader script + 2 `<ins>`) | Your publisher ID |
| `data-ad-slot="0000000001"` | 1 (leaderboard) | Real slot ID for a 728×90 unit |
| `data-ad-slot="0000000002"` | 1 (anchor) | Real slot ID for a 320×50 unit |

Notes:
- The loader script is `async` and the tool runs independently, so a blocked or slow ad never delays interactivity (spec §10, test T-6).
- Ad slots have **reserved fixed dimensions** (728×90, 320×50) to keep CLS at 0. If you switch to responsive units, give them a fixed `min-height` so layout doesn't shift.
- The dashed "Advertisement" box is just a placeholder; the real ad renders on top of it once filled.

## 3. Local testing only

`serve.js` is a throwaway dev server (`node serve.js` → http://localhost:8080) used to test the service worker / offline behavior locally. **Do not deploy it** — your host serves static files and sets MIME types itself.

## 4. Post-deploy checklist
- [ ] Submit `sitemap.xml` to Google Search Console **and** Bing Webmaster Tools (spec §09 — Bing matters here).
- [ ] Run Lighthouse: Performance & SEO ≥ 95, no CLS from ads (test T-8).
- [ ] Verify the service worker registers (DevTools → Application) and the page loads offline.
- [ ] Calibrate with a real card, then measure it → reads 8.5–8.6 cm (test T-1).
