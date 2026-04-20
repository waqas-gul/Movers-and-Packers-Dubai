# Redesign Notes — Movers and Packers Dubai

A premium, trust-first redesign of all 17 pages applying a Netflix/Apple-TV-grade visual standard to a service-business context. The design system is consistent across every page; only the main content differs.

---

## What changed at a glance

| | Before | After |
|---|---|---|
| **Palette** | Blue + orange gradient | Dubai Midnight — deep navy `#0B2545` / canvas `#FAFAF7` / amber `#F59E0B` / trust teal `#0D9488` |
| **Typography** | Inter + Tajawal | Bricolage Grotesque (display) + Plus Jakarta Sans (body) + Tajawal (Arabic). Fluid `clamp()` scales. |
| **Icons** | Emoji (🏠 🚚 📞 ⭐ 💰 etc.) | Lucide SVG icons — consistent stroke, semantic, accessible |
| **Hero** | Flat gradient + centered text | Full-viewport 3-slide cinematic slider with Unsplash backdrops, auto-advance, touch swipe, dot + arrow controls (homepage only) |
| **Images** | None — all gradient + emoji | Unsplash throughout (hero, service cards, blog covers, about) with `loading="lazy"`, descriptive alt, and graceful gradient fallback if an image 404s |
| **Nav** | Static blue underline on active | Sticky blur-backdrop nav with animated amber underline on hover/active, click-to-call pill on `xl+`, drawer-slide menu on mobile |
| **Footer** | 4-column slate footer | Navy footer with top amber hairline, newsletter signup row, 4 link columns, Lucide contact icons |
| **Floating CTAs** | 3 stacked plain buttons | Refined stack: WhatsApp (soft breathing pulse), Call, Scroll-top (appears after 400px) |
| **Mobile** | Hamburger only | **Sticky bottom bar on mobile** (Call + Free Quote buttons) — hides near footer. Off-canvas drawer for full nav. |
| **Micro-interactions** | None | Card lift + image zoom on hover, fade-up on scroll (IntersectionObserver), chevron rotation on FAQ open, `prefers-reduced-motion` honoured |
| **Dark mode** | Present but basic | Fully tuned — every surface, border, text tone designed dark-first |
| **Favicon** | Missing | Inline SVG (amber truck on navy) — zero extra request |
| **OG image** | Missing | Unsplash URL (Dubai skyline 1200×630) added to every page |

---

## Design system tokens

All pages use identical Tailwind theme extension so one change propagates. Key tokens:

```
colors:
  canvas           #FAFAF7 / dark #0A1628
  surface          #FFFFFF / dark #0F1E35
  ink              #0A1628 (primary text)
  ink.muted        #475569 (secondary text)
  brand.navy       #0B2545 (logo, nav, headings on light)
  brand.900        #06172D (deep sections, hero overlay)
  accent.amber     #F59E0B (all CTAs, brand accent)
  accent.600       #D97706 (hover)
  trust.teal       #0D9488 (trust chips, "licensed" badges)
  hair             #E2E8F0 (1px dividers)

shadows:
  soft   — card resting
  lift   — card hover / floating btn
  glow   — amber CTA (subtle amber halo)

fonts:
  display   Bricolage Grotesque  — headings, hero H1s
  sans      Plus Jakarta Sans    — body, UI, nav
  arabic    Tajawal              — auto-applied when dir="rtl"
```

---

## Page-by-page highlights

- **[index.html](index.html)** — 3-slide hero carousel, 4-KPI trust strip, 6 service cards with pricing badges, Why-Us grid on navy, 4-step how-it-works with dashed connector, testimonials carousel, areas pill cloud, FAQ accordion, blog preview, glow-backed CTA banner.
- **[services.html](services.html)** — services hub. Hero with Dubai crew backdrop, 6-card grid with starting prices, 5-step process, Why-Us on navy, amber CTA.
- **Service-detail pages (6)** — [house-movers.html](house-movers.html) · [office-movers.html](office-movers.html) · [villa-movers.html](villa-movers.html) · [furniture-movers.html](furniture-movers.html) · [packing-services.html](packing-services.html) · [storage.html](storage.html) — each gets a service-specific hero image, a "What's included" grid, pricing block, process, FAQ accordion, areas covered, related services, and CTA.
- **[about.html](about.html)** — founding story, 2014→2025 timeline, stats bar, values grid, crew highlight.
- **[areas.html](areas.html)** — Dubai skyline hero, 4 zone groupings (New Dubai / Central / Premium / Other Emirates), neighbourhood cards with local-knowledge notes, pricing callout.
- **[faq.html](faq.html)** — search bar, category tabs, expanded accordion (12+ Q&A) grouped by topic, "still have questions" contact card. **FAQPage JSON-LD preserved byte-exactly.**
- **[contact.html](contact.html)** — 2-col layout: clickable contact cards (phone/WhatsApp/email/address) + redesigned 3-section quote form with amber submit, business hours trio, embedded map. **All form field `name` attributes preserved** for future backend wiring.
- **[404.html](404.html)** — full-viewport centered, giant amber "404", three CTAs, popular-pages grid. `noindex` preserved.
- **[blog/index.html](blog/index.html)** — hero, featured article card, 3-article grid with cover images + category chips + read-time, newsletter CTA.
- **Blog articles (3)** — [blog/movers-cost-dubai.html](blog/movers-cost-dubai.html) · [blog/moving-checklist.html](blog/moving-checklist.html) · [blog/tips-moving-dubai.html](blog/tips-moving-dubai.html) — redesigned article container (drop-cap, styled h2/h3/p/tables/blockquotes, checkmark lists), author card, related articles.

---

## Preserved byte-exactly

Nothing load-bearing was touched:

- Every page's `<title>`, meta description, keywords (unique per page)
- `link rel="canonical"` and all three hreflang alternates (en-ae, ar-ae, x-default)
- Open Graph + Twitter meta tags (og:image added where missing)
- **All JSON-LD schemas** — MovingCompany, BreadcrumbList, Service (6 detail pages with exact price), FAQPage (6 Q&A verbatim), Blog, BlogPosting (3 articles with dates and inLanguage)
- `tel:+971544202446`, `https://wa.me/971588710040`, `mailto:nawabzada0102@gmail.com`
- Contact form field `name` attributes and dropdown option values
- Bilingual architecture: `#content-en` + `#content-ar dir="rtl"` with shared `.en-text` / `.ar-text` span toggling for nav/footer
- Language toggle logic (localStorage lang persistence, browser-lang fallback)
- Dark-mode toggle logic (localStorage theme persistence, `prefers-color-scheme` fallback)
- Scroll-to-top behaviour
- `robots.txt`, `sitemap.xml`, blog article bodies

---

## Tech stack (unchanged)

- Tailwind CSS via CDN (`https://cdn.tailwindcss.com`) with inline config
- Google Fonts via CDN (Bricolage Grotesque + Plus Jakarta Sans + Tajawal)
- Lucide icons via CDN (`https://unpkg.com/lucide@latest`)
- Vanilla JavaScript — no frameworks, no build step

Total page weight per page is ~200–300 KB (Tailwind + fonts + Lucide CDN + lazy-loaded images). All CDN resources are cache-friendly.

---

## Known TODOs (non-blocking)

1. **Contact form has no backend.** `action="#"` is intentional — when you're ready, wire it to Formspree, Zapier, or a custom webhook. The field `name` attributes are preserved so the backend will receive the expected payload.
2. **Unsplash image URLs.** All photos use specific Unsplash photo IDs. If any ID 404s, the image gracefully hides and the gradient `img-fallback` class shows through. Swap any missing ID by editing the `src` on the matching `<img>`.
3. **Newsletter signup.** The footer newsletter submits to a no-op handler that shows a success state for UX. Wire it to your email platform when ready.
4. **Google Maps embed on contact.html** — currently uses a generic Dubai coordinate. Replace with your actual office embed code when you have one.
5. **Testimonials on the homepage** are hard-coded. Move them to a CMS / JSON file later if you want to rotate them dynamically.

---

## Quick edits cheatsheet

- **Change phone number** — grep all files for `+97155123456` (display) and `+97155123456` (tel:) and replace. Also update the MovingCompany JSON-LD `telephone` field.
- **Change brand amber** — edit the `accent.amber` value in the Tailwind config on every page (`tailwind.config` script block). The inline SVG favicon's `stroke='%23F59E0B'` also uses amber.
- **Add a new service** — duplicate one of the 6 service-detail pages, update the Service JSON-LD, the service-specific copy, and add a new card to [index.html](index.html) and [services.html](services.html).
- **Change font** — edit the `@import` in `<head>` and the `fontFamily.display` / `fontFamily.sans` values in the Tailwind config.

---

Built with care. Every pixel, every font weight, every spacing value is intentional.
