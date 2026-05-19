# Reedhaus

The agency's own site. Single-page static HTML — Tailwind via CDN, Three.js for the scroll-driven video, custom modals for checkout / booking / quote intake.

**Live (soon):** [reedhaus.studio](https://reedhaus.studio)

---

## Stack

- **HTML** — single file, no build step
- **Tailwind CSS** via CDN (production: bundle locally before launch for perf)
- **Three.js** for the scroll-scrubbed hero video
- **Variable fonts** — Fraunces (display) + Geist (sans + mono) via Google Fonts

No framework, no `node_modules`. Open `index.html` and it works.

---

## Local dev

Open the file:

```bash
open index.html
```

Or run a local HTTP server (recommended — video + asset paths behave the same as production):

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

---

## Deploy to Vercel

The Vercel project should be named **`reedhaus`** so it shows cleanly in the dashboard and the default URL becomes `reedhaus.vercel.app`.

### Option A — Vercel CLI (fastest)

```bash
npm i -g vercel
vercel --name reedhaus
```

Follow the prompts. Vercel auto-detects this as a static site.

### Option B — Vercel Dashboard

1. Push this repo to GitHub (see below)
2. Go to <https://vercel.com/new>
3. Import the GitHub repo
4. **Project Name:** `reedhaus`
5. **Framework Preset:** Other / Static
6. **Root Directory:** leave default
7. Click **Deploy**

### Hook up the domain

1. In the Vercel project → **Settings → Domains** → add `reedhaus.studio` and `www.reedhaus.studio`
2. Vercel will show DNS records (`A` + `CNAME`)
3. At your domain registrar, point those records at Vercel
4. SSL is automatic — done in ~1 min once DNS propagates

---

## Push to GitHub

```bash
git init
git add .
git commit -m "Initial Reedhaus site"

# with GitHub CLI:
gh repo create reedhaus-site --private --source=. --remote=origin --push

# OR manually — create the repo on github.com first, then:
git remote add origin git@github.com:YOUR_USERNAME/reedhaus-site.git
git branch -M main
git push -u origin main
```

---

## File structure

```
reedhaus-site/
├── index.html          ← the whole site
├── README.md
├── .gitignore
├── vercel.json
└── assets/
    ├── favicon.png
    ├── logo-square.png
    ├── og-image.png
    └── hero-scrub.mp4   (re-encoded all-I-frame, 6 MB — for smooth scrubbing)
```

---

## Pre-launch TODO

The site is design-complete. Before driving traffic:

1. **DNS** — point `reedhaus.studio` at the Vercel project
2. **Email** — set up `hi@reedhaus.studio` (Gmail-on-domain via Google Workspace, or Fastmail / Migadu)
3. **Stripe** — create a Payment Link for `$649 initial + $149/mo recurring`, wire it into the Starter checkout modal in `index.html`
4. **Cal.com / Calendly** — set up a 30-min "Discovery call" page, embed in or link from the Pro calendar modal
5. **Supabase** — `leads` table for quote-intake submissions; wire the Signature form's `fakeQuote()` handler to an actual insert
6. **Telegram bot** — pushed alert for every new lead / signup (matches your existing automation stack)
7. **Terms of Service + Privacy Policy** — required by Stripe (Termly or a one-pager)
8. **Analytics** — GA4 or Plausible
9. **og:image** — current is portrait 896×1200; generate a proper landscape **1200×630** for clean social cards
10. **Convert to Next.js** when you need a client dashboard, per-client subdomains, or per-industry landing pages

---

## Credits

Built by Gabriel Reed · 2026
