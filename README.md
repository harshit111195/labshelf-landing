# LabShelf — landing page

Static single-file landing page for [LabShelf](https://labshelf.com). Deployed to Vercel from this repo; auto-deploys on every push to `main`.

## Stack

- Plain HTML + Tailwind CDN, no build step
- Lemon Squeezy overlay checkout embedded
- Deployed on Vercel (Hobby tier, free)

## Structure

```
index.html        — the whole page
README.md         — this file
.gitignore
.claude/          — local dev-server config (not needed on Vercel)
```

## Before going live — replace placeholders

Search `index.html` for these and swap in real values:

| Placeholder | Replace with |
|---|---|
| `PRODUCT-ID` (4×) | Lemon Squeezy product/variant ID |
| `labshelf.lemonsqueezy.com` (4×) | Your actual LS store subdomain |
| `LOOM-URL` | 3-minute setup Loom video URL |
| `DEMO-SHEET-URL` | Read-only live demo Sheet URL |
| `SUPPORT-EMAIL` (2×) | Your support email |
| `https://github.com/` | Public repo URL or source-preview link |
| `https://labshelf.com` in `<meta og:url>` | Your production domain |

Do a final `grep -n PLACEHOLDER index.html` before the first deploy.

## Local dev

If you have Claude Code's launch.json integration, a server is pre-configured on port 8766. Otherwise, any static server works:

```bash
python -m http.server 8766
# or
npx serve .
```

Open http://localhost:8766.

## Deploying to Vercel

1. Push this repo to GitHub (see below).
2. Go to vercel.com → **Add New → Project** → import the repo.
3. Framework preset: **Other**. Build command: leave blank. Output directory: leave blank (repo root).
4. Deploy. You'll get a `*.vercel.app` URL immediately.
5. Add your custom domain (`labshelf.com`) under Project Settings → Domains.

After that, every `git push` to `main` ships to production. Pushes to other branches create preview deployments with unique URLs.

## Production notes

- Tailwind CDN throws a console warning in dev. If traffic grows, swap to a one-time Tailwind CLI build (`npx tailwindcss -i in.css -o out.css --minify`) and replace the CDN script tag. Not urgent at launch volume.
- `<meta property="og:image">` intentionally missing. Add a 1200×630 screenshot of the hero once the real domain is live.
- No analytics, no cookie banner (no tracking). Add Plausible / Fathom later if needed for conversion numbers.

## Related

- Product code (private): `labshelf` repo
- Payment & distribution roadmap: internal planning doc
