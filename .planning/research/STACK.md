# Technology Stack

**Project:** TeamTigrr Landing Page
**Researched:** 2026-02-02
**Overall Confidence:** HIGH

## Executive Summary

For a SaaS landing page targeting team leaders and parents in junior sports, Astro + Tailwind CSS v4 is the optimal stack. This combination delivers superior performance (critical for mobile users at sports venues), excellent SEO, and maintains development simplicity. The current static HTML approach works but misses modern tooling benefits like component reusability, build-time optimization, and type safety.

---

## Recommended Stack

### Core Framework

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **Astro** | 5.x (5.10+) | Static site framework | 50-70% smaller JS bundles vs React-based frameworks. Zero JS by default with islands architecture. 5x faster builds for content-heavy sites. Built-in View Transitions for smooth page animations without extra libraries. Perfect for content-focused landing pages. | HIGH |

**Rationale:** Astro outperforms Next.js for static landing pages:
- First Contentful Paint: 0.5s (Astro) vs 1-1.5s (Next.js)
- Lighthouse scores stay above 95 on mobile 3G, while Next.js drops to ~75
- No mandatory JS payload (Next.js loads minimum 87KB even for blank pages)
- View Transitions API support with zero JavaScript (85%+ browser support in 2025)

**What NOT to use:**
- **Next.js** - Overkill for a landing page. Requires React runtime (~87KB minimum). Better for dynamic apps with user dashboards. TeamTigrr's landing page is static content; Next.js overhead isn't justified.
- **Plain HTML** (current) - Misses component reusability, build-time optimization, and developer tooling. Works but doesn't scale as page complexity grows.
- **Gatsby** - Effectively deprecated. Slower builds, heavier bundle, React dependency.

---

### Styling

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **Tailwind CSS** | 4.x (4.0+) | Utility-first CSS | Full builds 3.78x faster, incremental builds 182x faster via Rust-based Oxide engine. CSS-first configuration (no tailwind.config.js needed). Native CSS features: cascade layers, color-mix(), @property. First-party Vite plugin for Astro integration. | HIGH |

**Installation:**
```bash
npm i tailwindcss @tailwindcss/vite
```

**CSS-first configuration (replaces tailwind.config.js):**
```css
@import "tailwindcss";

@theme {
  --font-display: "Teko", sans-serif;
  --font-sans: "Inter", sans-serif;
  --color-tigrr-orange: oklch(0.65 0.24 30);
  --color-tigrr-dark: oklch(0.13 0 0);
  --color-tigrr-charcoal: oklch(0.18 0 0);
}
```

**What NOT to use:**
- **Tailwind CDN** (current) - No tree-shaking, no build optimization, no CSS-first config. Only suitable for prototypes.
- **Tailwind v3** - Missing Oxide engine performance, CSS-first config, and modern CSS features.
- **CSS-in-JS (styled-components, Emotion)** - Runtime overhead, hydration cost, worse performance for static sites.

---

### Icons

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **Lucide** | 0.562+ | Icon library | Tree-shakeable icons (import only what you use). Consistent, modern design. Official Astro package (@lucide/astro). Replaces Font Awesome which loads entire icon set. | HIGH |

**Installation:**
```bash
npm i @lucide/astro
```

**Usage:**
```astro
---
import { Timer, Users, Shield } from '@lucide/astro'
---
<Timer class="w-6 h-6" />
```

**What NOT to use:**
- **Font Awesome CDN** (current) - Loads entire icon library (~400KB). No tree-shaking. Network dependency.
- **Heroicons** - Good alternative but Lucide has broader icon selection for sports/team contexts.

---

### Fonts

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **@fontsource** | latest | Self-hosted fonts | Eliminates Google Fonts network request. Font files bundled at build time. Better privacy (no Google tracking). Faster loading (no external DNS lookup). | MEDIUM |

**Installation:**
```bash
npm i @fontsource-variable/inter @fontsource/teko
```

**Usage:**
```css
@import "@fontsource-variable/inter";
@import "@fontsource/teko/400.css";
@import "@fontsource/teko/700.css";
```

**Alternative:** Keep Google Fonts if self-hosting complexity is unwanted. Performance difference is marginal with proper preconnect hints.

---

### Animations

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **Astro View Transitions** | Built-in | Page transitions | Zero JavaScript required with @view-transition CSS rule. 85%+ browser support. Automatic reduced-motion support. Smooth app-like feel. | HIGH |
| **CSS animations** | Native | Micro-interactions | Hardware-accelerated, no library needed. Use for hover states, loading spinners. | HIGH |

**For complex animations (optional):**
| Technology | Version | Purpose | When to Use | Confidence |
|------------|---------|---------|-------------|------------|
| **Motion** | 12.x | Interactive animations | Only if you need scroll-triggered animations, gesture support, or springs. Consider later if conversion data suggests animation improvements help. | MEDIUM |

**What NOT to use:**
- **GSAP** - 23KB+ for timeline features you likely won't need. Overkill for landing page micro-interactions.
- **Framer Motion** - Requires React. Wrong fit for Astro.
- **Animate.css** - Dated approach. CSS native is cleaner.

---

### Analytics

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **Plausible Analytics** | Cloud or self-hosted | Privacy-first analytics | GDPR/CCPA compliant without consent banners. 75x smaller script than Google Analytics. Real-time dashboard. UTM tracking. EU-hosted. $9/month for 10k pageviews. | HIGH |

**Alternative - Free:** PostHog (self-hosted) if you need session recordings, funnels, A/B testing later. More complex setup.

**What NOT to use:**
- **Google Analytics** - Requires cookie consent banner. Privacy concerns for EU users. Overkill for landing page needs.
- **No analytics** - Can't optimize conversion without data.

---

### Form Handling & Email

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **Resend** | latest | Transactional email | Simple API. Free tier (100 emails/day). Easy integration. Confirmation emails for waitlist signups. | MEDIUM |
| **Astro Server Endpoints** | Built-in | Form backend | Handle form submissions server-side. No external service for simple use cases. | HIGH |

**Current approach (Google Apps Script):** Works but fragile. No email confirmation, limited error handling, no rate limiting.

**Alternative - No-code:** Keep Google Sheets integration if it works. Add rate limiting via Cloudflare.

---

### Hosting

| Technology | Version | Purpose | Why | Confidence |
|------------|---------|---------|-----|------------|
| **Cloudflare Pages** | - | Static hosting | Unlimited bandwidth (free). 300+ global edge locations. Best performance. Free SSL. Easy GitHub integration. | HIGH |

**Alternative - Good:** Netlify or Vercel. Both have 100GB bandwidth free tier. Vercel is overkill for static Astro site.

**Current (GitHub Pages):** Works fine but Cloudflare offers better global performance and unlimited bandwidth.

---

## Alternatives Considered

| Category | Recommended | Alternative | Why Not Alternative |
|----------|-------------|-------------|---------------------|
| Framework | Astro | Next.js | React runtime overhead. Overkill for static landing page. |
| Framework | Astro | Eleventy (11ty) | Less modern DX. No built-in View Transitions. Smaller ecosystem. |
| Styling | Tailwind v4 | Vanilla CSS | Slower development. No design system consistency. |
| Styling | Tailwind v4 | UnoCSS | Smaller ecosystem. Tailwind v4 closed the performance gap. |
| Icons | Lucide | Heroicons | Lucide has broader sports-relevant icons. |
| Hosting | Cloudflare Pages | Vercel | Vercel's strengths (Next.js optimization) aren't relevant here. |
| Analytics | Plausible | Fathom | Plausible is open-source, EU-hosted, slightly cheaper. |

---

## Installation

### Create new Astro project
```bash
npm create astro@latest teamtigrr-website
cd teamtigrr-website
```

### Core dependencies
```bash
npm install tailwindcss @tailwindcss/vite
npm install @lucide/astro
npm install @fontsource-variable/inter @fontsource/teko
```

### Dev dependencies
```bash
npm install -D typescript @astrojs/check
```

### Optional (add later if needed)
```bash
npm install motion  # Complex animations
npm install resend  # Email
```

---

## Migration Path from Current Setup

1. **Phase 1: Framework** - Create Astro project, convert index.html to Astro components
2. **Phase 2: Styling** - Replace CDN Tailwind with build-time Tailwind v4
3. **Phase 3: Icons** - Replace Font Awesome with Lucide
4. **Phase 4: Fonts** - Optional: Self-host fonts via @fontsource
5. **Phase 5: Hosting** - Deploy to Cloudflare Pages (keep GitHub Pages as backup)
6. **Phase 6: Analytics** - Add Plausible after launch

Each phase can be deployed independently. No big-bang migration required.

---

## File Structure (Recommended)

```
teamtigrr-website/
├── src/
│   ├── components/
│   │   ├── Header.astro
│   │   ├── Hero.astro
│   │   ├── Features.astro
│   │   ├── SignupForm.astro
│   │   └── Footer.astro
│   ├── layouts/
│   │   └── Base.astro
│   ├── pages/
│   │   └── index.astro
│   └── styles/
│       └── global.css
├── public/
│   └── favicon.svg
├── astro.config.mjs
└── package.json
```

---

## Performance Targets

| Metric | Target | Why |
|--------|--------|-----|
| Lighthouse Performance | 95+ | Mobile users at sports venues may have poor connectivity |
| First Contentful Paint | < 1s | Above-fold content must load fast |
| Total Blocking Time | < 200ms | No JS blocking main thread |
| Cumulative Layout Shift | < 0.1 | No jarring layout shifts |
| Bundle size (JS) | < 10KB | Astro default is near-zero |

---

## Sources

### Framework Research
- [Next.js vs Astro 2025 Comparison - Makers' Den](https://makersden.io/blog/nextjs-vs-astro-in-2025-which-framework-best-for-your-marketing-website)
- [Astro vs Next.js Technical Comparison - BetterLink](https://eastondev.com/blog/en/posts/dev/20251202-astro-vs-nextjs-comparison/)
- [Astro 5.0 Release - Astro Blog](https://astro.build/blog/astro-5/)

### Tailwind Research
- [Tailwind CSS v4.0 Official Release](https://tailwindcss.com/blog/tailwindcss-v4)
- [Tailwind v4 Deep Dive - DEV Community](https://dev.to/dataformathub/tailwind-css-v4-deep-dive-why-the-oxide-engine-changes-everything-in-2025-3dhd)

### Animation Research
- [GSAP vs Motion Comparison - Motion](https://motion.dev/docs/gsap-vs-motion)
- [Astro View Transitions - Astro Docs](https://docs.astro.build/en/guides/view-transitions/)
- [Zero-JS View Transitions - Astro Blog](https://astro.build/blog/future-of-astro-zero-js-view-transitions/)

### Analytics Research
- [PostHog vs Plausible - Vemetric](https://vemetric.com/blog/posthog-vs-plausible)
- [Plausible Analytics](https://plausible.io/)

### Hosting Research
- [Vercel vs Netlify vs Cloudflare 2025 - Digital Applied](https://www.digitalapplied.com/blog/vercel-vs-netlify-vs-cloudflare-pages-comparison)

### Conversion Optimization
- [SaaS Landing Page Best Practices 2025 - Magic UI](https://magicui.design/blog/saas-landing-page-best-practices)
- [SaaS Landing Pages - Unbounce](https://unbounce.com/conversion-rate-optimization/the-state-of-saas-landing-pages/)
