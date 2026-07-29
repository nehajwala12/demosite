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

Open `index.html` directly in a browser, or serve it (so routes behave like production):

```bash
npm run dev     # runs: npx serve .
```

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
