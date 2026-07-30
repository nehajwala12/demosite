# CreditSwan.AI — Credit Diligence Demo Suite

Five sample credit-committee dashboards, one per sector. Static HTML, no build step, no dependencies —
deploys to Vercel as-is.

> **Everything in this repo is fictional.** All company names, sponsor names, codenames, financial figures,
> ratios, charts, and findings are invented for demonstration purposes and describe no real company,
> transaction, or security. Nothing here is investment advice.

## Routes

| Route | Sector | Engagement | Depth |
|---|---|---|---|
| `/` | Suite landing page (all five, previewable inline) | — | — |
| `/cpg-snacking` | Consumer Packaged Goods — Better-for-you Snacking | Project Summit — Northwind Provisions Co. | 15 tabs · 40 charts |
| `/functional-beverage` | Consumer — Functional Beverage / Hydration | Project Current — Volt Hydration Co. | 15 tabs · 40 charts |
| `/pet-supplements` | Consumer Health — Pet Supplements | Project Thrive — VitaPaw Nutrition | 15 tabs · 40 charts |
| `/fitness-franchising` | Consumer — Boutique Fitness Franchising | Project Ignite — PulseForge Studios | 15 tabs · 41 charts |
| `/pet-insurance` | InsurTech — Pet Insurance | Project Companion — Paws Assurance | 15 tabs · 41 charts |

Each sector is a standalone page, so you can send a prospect a direct link to just the relevant one —
e.g. `https://your-project.vercel.app/pet-insurance`.

## Deploy to Vercel

**Option A — GitHub (recommended)**

1. Create a new GitHub repo and push these files:
   ```bash
   git init
   git add .
   git commit -m "CreditSwan demo suite"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
2. Go to [vercel.com/new](https://vercel.com/new), import the repo.
3. Framework preset: **Other**. Build command: *(leave empty)*. Output directory: *(leave empty / root)*.
4. Deploy.

**Option B — Vercel CLI**

```bash
npm i -g vercel
vercel          # preview deployment
vercel --prod   # production deployment
```

**Option C — drag and drop**

Zip the folder contents and drop them on [vercel.com/new](https://vercel.com/new).

## Local preview

Open `index.html` directly in a browser, or serve it so routes behave like production:

```bash
npx serve .
```

## Troubleshooting — "it deployed but nothing shows"

**1. 404: NOT_FOUND — the most common cause.** `index.html` must be at the *repository root*,
not inside a subfolder. If your repo looks like `your-repo/creditswan-demo-suite/index.html`,
Vercel is serving `your-repo/` and finding nothing.

Fix either way:

```bash
# move the files up one level
mv creditswan-demo-suite/* creditswan-demo-suite/.gitignore .
rmdir creditswan-demo-suite
git add -A && git commit -m "Move site to repo root" && git push
```

...or in Vercel: **Project → Settings → Build and Deployment → Root Directory** →
set it to `creditswan-demo-suite` → Save → Redeploy.

Verify with: `git ls-files | head` — you should see `index.html` on its own, with no folder prefix.

**2. "No Output Directory named 'public' found."** This means Vercel treated the project as a
build project. This repo intentionally contains **no `package.json`** to avoid that. If you see
this error, check Settings → Build and Deployment:

- Framework Preset: **Other**
- Build Command: **empty** (toggle the override off)
- Output Directory: **empty**, or `.`

**3. A login / SSO wall instead of the site.** That is Vercel Deployment Protection, which is on
by default for preview deployments on many plans. Go to **Settings → Deployment Protection** and
set Vercel Authentication to *Disabled* (or *Only Preview Deployments* if you want the production
URL public). Also confirm you are opening the **Production** URL, not a preview URL.

**4. Blank white page.** Open the browser console. The dashboards load Chart.js from
`cdnjs.cloudflare.com`; if a corporate network blocks it, charts will not render. Everything else
on the page is inline and offline-safe.

## Adding a passphrase gate

The demos are public by default. If you want the same passphrase protection used on your other
deployments, the simplest options are:

- **Vercel Password Protection** — Project → Settings → Deployment Protection (no code changes).
- **Client-side gate** — wrap each page's body in an AES-GCM encrypted payload unlocked by a passphrase.

## Customizing

Each dashboard is a single self-contained HTML file: inline CSS, inline JS, Chart.js from CDN.

- **Change numbers** — chart data lives in the `renderCharts()` function near the bottom of each file.
- **Change copy** — the narrative text sits in the `<section class="panel">` blocks.
- **Change a sector name** — rename the `.html` file and update the matching entry in `index.html`.
- **Palette** — the design tokens are in the `:root` CSS block at the top of each file.

## Notes

- `vercel.json` sets `cleanUrls` (so `/pet-insurance` works), sensible security headers, and
  `X-Robots-Tag: noindex` so demo content stays out of search results.
- No analytics or tracking is included.
