# Movers and Packers Dubai

Bilingual (English + Arabic) static website for a Dubai moving-services company. 17 pages, fully responsive, dark-mode aware, SEO-optimised with structured data.

**Live contact:**
`+971 54 420 2446` · WhatsApp `+971 58 871 0040` · `nawabzada0102@gmail.com`

---

## Tech stack

- **HTML5** — 17 static pages, no build step
- **Tailwind CSS** via CDN (`cdn.tailwindcss.com`) with inline config
- **Google Fonts** — Bricolage Grotesque (display) + Plus Jakarta Sans (body) + Tajawal (Arabic)
- **Lucide Icons** via CDN (`unpkg.com/lucide@latest`)
- **Vanilla JS** — language toggle, dark mode, hero slider, mobile drawer, scroll animations

No frameworks, no npm, no bundler. Just open an HTML file.

---

## Run locally

```bash
cd website
python -m http.server 8000
```

Open [http://localhost:8000](http://localhost:8000).

Or just double-click `index.html` to open directly in a browser (language toggle and theme toggle will work; only a few features need a real server).

---

## Project structure

```
website/
├── index.html                  # Homepage with hero slider
├── services.html               # Services hub
├── about.html                  # Company story
├── areas.html                  # Coverage areas
├── contact.html                # Contact + quote form
├── faq.html                    # FAQ with schema
├── 404.html                    # Error page (noindex)
├── house-movers.html           # Service: AED 300 start
├── office-movers.html          # Service: AED 800 start
├── villa-movers.html           # Service: AED 1,800 start
├── furniture-movers.html       # Service: AED 150/item
├── packing-services.html       # Service: AED 200 start
├── storage.html                # Service: AED 100/month
├── blog/
│   ├── index.html              # Blog hub
│   ├── movers-cost-dubai.html  # Pricing guide
│   ├── moving-checklist.html   # 8-week checklist
│   └── tips-moving-dubai.html  # 10 expert tips
├── sitemap.xml
├── robots.txt
├── README.md                   # This file
└── REDESIGN-NOTES.md           # What changed in the redesign
```

---

## Deploy

### Netlify (recommended)
Drag the `website/` folder onto [app.netlify.com](https://app.netlify.com) → done.
See `REDESIGN-NOTES.md` for CLI + Git-based alternatives.

### Any static host
Upload the folder to any static host — Vercel, Cloudflare Pages, GitHub Pages, S3, or traditional shared hosting. No server-side dependencies.

---

## Common edits

**Change phone / WhatsApp / email** (find-and-replace across all files):
- Phone display: `+971 54 420 2446`
- Phone `tel:` link: `+971544202446`
- Phone schema (JSON-LD): `+971-54-420-2446`
- WhatsApp URL: `https://wa.me/971588710040`
- Email: `nawabzada0102@gmail.com`

**Change brand colour:**
Edit the `accent.amber` (`#F59E0B`) value in each file's `<script>tailwind.config = ...` block. The favicon SVG `stroke='%23F59E0B'` also uses this colour.

**Wire up the quote form:**
`contact.html` has a form with `action="#"`. Replace with your Formspree / Zapier / custom endpoint. Field `name` attributes are already set — they map to: `name`, `phone`, `email`, `from`, `to`, `date`, `type`, `size`, `message`.

**Add a new service:**
Duplicate one of the service-detail pages (e.g. `house-movers.html`), update the Service JSON-LD schema, the copy, and add a card to `index.html` + `services.html`.

---

## Key features

- **Bilingual** — one click swaps between English and Arabic; `dir="rtl"` toggles for Arabic with Tajawal font.
- **Dark mode** — class-based, persisted in `localStorage`, respects system preference on first visit.
- **SEO** — unique title/description/keywords per page, canonical URLs, three `hreflang` alternates (en-ae, ar-ae, x-default), Open Graph + Twitter cards, structured data on every page.
- **Structured data** — `MovingCompany`, `BreadcrumbList`, `Service` (on each service-detail page with price), `FAQPage` (on FAQ), `BlogPosting` (on articles).
- **Mobile-first** — sticky bottom bar (Call + Free Quote) on phones, off-canvas drawer for nav, touch-swipe hero slider.
- **Conversion-optimised** — click-to-call in header, WhatsApp floating button with breathing pulse, Get-Free-Quote CTAs everywhere.
- **Accessibility** — semantic HTML, `aria-label`s, focus states, 44px tap targets, `prefers-reduced-motion` honoured.

---

## Notes

- Contact form is not wired to a backend yet (`action="#"`).
- Newsletter signup in the footer is visual-only.
- Google Maps embed on `contact.html` uses a generic Dubai coordinate — replace with your actual office embed when ready.
- All images come from Unsplash (`images.unsplash.com`). If any URL 404s, a gradient fallback shows.

Licensed, insured, and trusted across the UAE since 2014.
