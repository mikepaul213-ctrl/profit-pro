# Profit Pro — Claude Code Brief

## What this is
A single-page web tool for digital product sellers to calculate profit margins and find listing prices. No backend, no framework, no build step required. Pure HTML/CSS/JS.

## Project structure
```
profit-pro/
├── src/
│   └── index.html      ← The entire application (single file)
├── CLAUDE.md           ← This file
└── README.md           ← Public-facing docs
```

---

## Deployment target: Netlify (recommended)

### Option A — Drag & drop (fastest, no CLI needed)
1. Go to netlify.com → Log in or create free account
2. From the dashboard: **"Add new site" → "Deploy manually"**
3. Drag the `src/` folder onto the upload zone
4. Done — live URL in ~30 seconds

### Option B — Netlify CLI
```bash
npm install -g netlify-cli
netlify login
netlify deploy --dir=src --prod
```

### Option C — GitHub + Netlify (recommended for ongoing updates)
1. Push this repo to GitHub
2. Netlify → "Add new site" → "Import from Git"
3. Set **publish directory** to `src`
4. Every push to `main` auto-deploys

---

## Alternative deploy targets

### Vercel
```bash
npm install -g vercel
vercel --public
# Set output directory to: src
```

### GitHub Pages
1. Push repo to GitHub
2. Settings → Pages → Source: Deploy from branch `main` → folder `/src`
3. Live at `https://yourusername.github.io/profit-pro`

### Cloudflare Pages
1. Connect GitHub repo in Cloudflare dashboard
2. Build settings: no build command, publish directory = `src`

---

## Custom domain (optional)
All platforms above support custom domains on free tier.
1. Buy domain (Namecheap, Cloudflare Registrar, etc.)
2. Add domain in Netlify/Vercel dashboard
3. Point DNS CNAME to the platform's provided URL
4. SSL is automatic

---

## Monthly maintenance (IMPORTANT)
**The only ongoing task.** Takes ~10 minutes.

Open `src/index.html` and find this at the top of the `<script>` block:

```js
const LAST_VERIFIED = 'May 2026'; // ← UPDATE THIS EACH MONTH
```

### Monthly checklist
Visit each link, confirm fee values match what's in the file, update the date:

| Platform | Fee in file | Check URL |
|---|---|---|
| Stripe | 2.9% + $0.30 | https://stripe.com/pricing |
| Gumroad | 10% | https://help.gumroad.com/article/66-gumroads-fees |
| Etsy Transaction | 6.5% | https://www.etsy.com/help/article/138 |
| Etsy Payments | 3% + $0.25 | https://www.etsy.com/help/article/138 |
| LemonSqueezy | 5% + $0.50 | https://www.lemonsqueezy.com/pricing |
| PayPal | 3.49% + $0.49 | https://www.paypal.com/webapps/mpp/merchant-fees |

If a fee changes:
1. Update the value in `PRESETS` (used by the fee layer chips)
2. Update the value in `PLATFORMS` (used by the compare panel)
3. Update `LAST_VERIFIED` date
4. Save and redeploy

---

## Features summary

| Feature | Description |
|---|---|
| Calculate Profit | Enter sale price → see net profit after all fees + COGS |
| Find List Price | Enter desired take-home → get required listing price |
| Fee stacking | Add multiple fee layers (e.g. Etsy transaction + Etsy Payments) |
| Quick-add chips | One-click preset fee layers for all supported platforms |
| Platform comparison | Enter one price, see profit across all 6 platforms ranked |
| Margin health indicator | Green / amber / red pill (≥50% / ≥20% / <20%) |
| Last verified date | Sourced from single `LAST_VERIFIED` variable — one edit updates everywhere |
| Copy result | Clipboard copy with inline feedback |
| Responsive | Works on mobile |

---

## What NOT to change
- No build tooling needed — do not add webpack, vite, or npm unless adding new features
- Do not split into multiple files unless the project grows significantly
- Google Fonts CDN links are intentional — no need to self-host for this use case
- The iterative solver in `reversePrice()` is intentional — stacked % fees cannot be cleanly inverted analytically

---

## If adding features later

**Email capture (Mailchimp/ConvertKit)**
Add a simple form at the bottom of the page. Both services provide embeddable HTML snippets — paste directly into `index.html` before `</body>`.

**Analytics (Plausible / Fathom — privacy-friendly)**
Add their one-line script tag before `</body>`. No GDPR issues for a free tool.

**New platform**
1. Add to `PRESETS` object (for fee layer chips)
2. Add to `PLATFORMS` array (for compare panel)
3. Add chip button in the `.fee-preset-row` div
4. Update monthly checklist above

---

## Tech stack
- HTML5 / CSS3 / Vanilla JS — zero dependencies
- Google Fonts: Instrument Serif, Outfit, DM Mono
- Tailwind: NOT used (pure CSS with CSS variables)
- No framework, no build step, no node_modules
