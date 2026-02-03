# Phase 3: Performance & Polish - Research

**Researched:** 2026-02-03
**Domain:** Mobile performance optimization, Core Web Vitals, accessibility tap targets
**Confidence:** HIGH

## Summary

This phase focuses on optimizing an existing static HTML landing page for mobile performance and accessibility. The page currently uses Tailwind CSS CDN, Google Fonts, and Font Awesome CDN. The success criteria are specific and measurable: Lighthouse 90+ on mobile 3G, LCP under 2.5 seconds, 44x44px tap targets, and no horizontal scroll on 320-768px viewports.

The current implementation has several performance bottlenecks that prevent hitting these targets: CDN-loaded Tailwind (no tree-shaking, ~300KB+ CSS), Font Awesome CDN (entire icon library ~400KB), and multiple external font requests. The optimization approach must address these blockers while keeping the static HTML architecture intact (no build system migration in this phase).

**Primary recommendation:** Focus on resource optimization through self-hosting critical assets, reducing external requests, and implementing CSS/image optimization. The current CDN-heavy approach is the main blocker for Lighthouse 90+ on mobile 3G.

## Standard Stack

### Core (No New Dependencies)

This phase uses existing web platform features and manual optimization techniques.

| Tool | Version | Purpose | Why Standard |
|------|---------|---------|--------------|
| Chrome DevTools Lighthouse | Built-in | Performance auditing | Official Google tool, measures exact success criteria |
| Inline SVG icons | N/A | Replace Font Awesome | Eliminates 400KB+ external request |
| System font stack fallback | N/A | Font loading strategy | Prevents FOIT/FOUT |
| Native CSS | N/A | Responsive fixes | No build system needed |

### Optional Tools (Quality Verification)

| Tool | Purpose | When to Use |
|------|---------|-------------|
| PageSpeed Insights | Real-world CrUX data | Verify against field data |
| WebPageTest | Detailed waterfall analysis | Debug specific bottlenecks |
| Responsively | Multi-viewport testing | Check 320px-768px range |

### Alternatives Considered

| Instead of | Could Use | Tradeoff |
|------------|-----------|----------|
| Inline SVG | Keep Font Awesome CDN | +400KB, fails Lighthouse target |
| Self-host fonts | Keep Google Fonts | 200-300ms slower, external dependency |
| Manual CSS fixes | Migrate to Tailwind v4 build | Larger scope, separate phase |

## Architecture Patterns

### Current Architecture (Constraints)

```
index.html
  CDN: tailwindcss (script)
  CDN: Google Fonts (2 requests)
  CDN: Font Awesome (stylesheet)
  Inline: <style> custom CSS
  Inline: <script> form/nav JS
```

### Optimization Strategy (In-Place)

Since this phase does not include build system migration, optimizations must work within the static HTML constraint:

```
index.html (optimized)
  CDN: tailwindcss (unchanged - can't purge without build)
  Self-host OR optimize: Fonts (subset, preconnect)
  Replace: Font Awesome CDN with inline SVG
  Optimize: Image compression, defer non-critical
  Fix: CSS overflow issues, tap target sizing
```

### Pattern 1: Critical Resource Loading Order

**What:** Ensure LCP resource loads before non-critical assets
**When to use:** Always for performance-critical pages

```html
<head>
  <!-- Preconnect to required origins first -->
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>

  <!-- Critical CSS inline (if small) or first external -->
  <style>/* Critical above-fold CSS */</style>

  <!-- Fonts with display:swap -->
  <link href="...&display=swap" rel="stylesheet">

  <!-- Defer non-critical scripts -->
  <script src="..." defer></script>
</head>
```

### Pattern 2: Mobile-First Responsive Fixes

**What:** Ensure no horizontal overflow on narrow viewports
**When to use:** Fixing existing layouts for 320px minimum width

```css
/* Defensive global styles */
html, body {
  overflow-x: hidden;
  width: 100%;
}

*, *::before, *::after {
  box-sizing: border-box;
}

/* Avoid fixed pixel widths */
.container {
  width: 100%;
  max-width: 1280px; /* Use max-width, not width */
}

/* Images must not overflow */
img {
  max-width: 100%;
  height: auto;
}
```

### Pattern 3: Tap Target Sizing

**What:** Ensure all interactive elements meet 44x44px minimum
**When to use:** All buttons, links, form controls

```css
/* Minimum tap target size */
.btn, a, button, input, select {
  min-height: 44px;
  min-width: 44px;
  /* OR use padding to achieve size */
  padding: 12px 16px; /* Results in ~44px+ with text */
}

/* For icon-only buttons */
.icon-btn {
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
}
```

### Anti-Patterns to Avoid

- **Loading all Font Awesome icons:** CDN loads entire library (~400KB). Replace with inline SVG for used icons only.
- **Using 100vw for widths:** Includes scrollbar width, causes horizontal overflow. Use `100%` instead.
- **Fixed pixel widths on mobile:** Elements like `width: 600px` overflow 320px viewport. Use `max-width` and percentages.
- **Small tap targets with no padding:** A 20px link looks fine but fails accessibility. Extend clickable area with padding.

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Performance measurement | Manual timing | Lighthouse DevTools | Standardized, weighted scoring |
| Icon optimization | Custom SVG sprites | Direct inline SVG | Simple, no build needed |
| Font subsetting | Manual font editing | Google Fonts URL params | Already optimized delivery |
| Image compression | Custom scripts | ImageOptim / Squoosh | One-time manual optimization |
| Viewport testing | Browser resize | Chrome DevTools Device Mode | Accurate device simulation |

**Key insight:** For a single static HTML page without a build system, manual optimizations are appropriate. Automated tooling becomes valuable when you have many pages or frequent updates.

## Common Pitfalls

### Pitfall 1: Tailwind CDN Cannot Be Purged

**What goes wrong:** Tailwind CDN delivers full framework (~300KB+), cannot tree-shake unused utilities
**Why it happens:** CDN version has no build step to analyze HTML for used classes
**How to avoid:** Accept this limitation for now OR migrate to Tailwind CLI/build (separate phase). Focus optimization on other resources.
**Warning signs:** CSS payload shows high KB in Lighthouse audit

### Pitfall 2: Font Awesome CDN Loads Everything

**What goes wrong:** Including Font Awesome CDN loads all icons (~400KB), even if using 5-10 icons
**Why it happens:** CDN cannot know which icons are used
**How to avoid:** Replace with inline SVG for each icon used. Extract from Font Awesome source or use icon site.
**Warning signs:** Large "fontawesome" resource in network waterfall

### Pitfall 3: Google Fonts Blocking Render

**What goes wrong:** Fonts block text rendering, causing FOIT (Flash of Invisible Text)
**Why it happens:** Default font-display behavior is "auto" which often blocks
**How to avoid:** Add `&display=swap` to Google Fonts URL. Already present in current implementation.
**Warning signs:** Blank text during load, "Ensure text remains visible during webfont load" in Lighthouse

### Pitfall 4: Hidden Horizontal Overflow

**What goes wrong:** Page scrolls horizontally on mobile despite looking fine in desktop browser
**Why it happens:** Elements with fixed widths or margins extend beyond viewport
**How to avoid:** Test at exactly 320px width. Use `overflow-x: hidden` as safety net. Audit all fixed widths.
**Warning signs:** Content cut off on one side, visible scrollbar at bottom on mobile

### Pitfall 5: Tap Targets Too Close Together

**What goes wrong:** Links in navigation or footer are too close, users tap wrong item
**Why it happens:** Designing for desktop click precision, not mobile finger taps
**How to avoid:** Minimum 8px spacing between 44px targets, or increase individual target size
**Warning signs:** Lighthouse "Tap targets are not sized appropriately" audit failure

### Pitfall 6: LCP Resource Not Prioritized

**What goes wrong:** LCP element (usually hero image or heading) loads late
**Why it happens:** Browser discovers critical resource after other requests start
**How to avoid:** Ensure LCP resource is in initial HTML (not JS-loaded), use `fetchpriority="high"` for images
**Warning signs:** LCP > 2.5s, waterfall shows LCP resource loading late

## Code Examples

### Replace Font Awesome with Inline SVG

Current (problematic):
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
...
<i class="fas fa-bars text-xl"></i>
```

Optimized:
```html
<!-- Remove Font Awesome CDN entirely -->
...
<svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"/>
</svg>
```

### Optimize Google Fonts Request

Current:
```html
<link href="https://fonts.googleapis.com/css2?family=Teko:wght@300;400;500;600;700&family=Inter:wght@300;400;600;700&display=swap" rel="stylesheet">
```

Optimized (subset weights actually used):
```html
<!-- Preconnect first -->
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<!-- Load only weights actually used -->
<link href="https://fonts.googleapis.com/css2?family=Teko:wght@400;700&family=Inter:wght@400;600;700&display=swap" rel="stylesheet">
```

### Fix Overflow for 320px Viewport

```html
<style>
  /* Global overflow protection */
  html, body {
    overflow-x: hidden;
    width: 100%;
    margin: 0;
    padding: 0;
  }

  *, *::before, *::after {
    box-sizing: border-box;
  }

  /* Ensure images don't overflow */
  img, video, iframe {
    max-width: 100%;
    height: auto;
  }

  /* Tables need wrapper for horizontal scroll */
  .table-wrapper {
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
  }
</style>
```

### Ensure 44px Tap Targets

```css
/* Navigation links */
nav a {
  display: inline-flex;
  align-items: center;
  min-height: 44px;
  padding: 10px 12px;
}

/* Mobile menu button */
.mobile-menu-btn {
  width: 44px;
  height: 44px;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* CTA buttons - already large, but verify */
.cta-btn {
  min-height: 44px;
  padding: 12px 24px;
}

/* Footer links - often too small */
footer a {
  display: inline-block;
  min-height: 44px;
  line-height: 44px;
  padding: 0 8px;
}
```

## State of the Art

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| Font Awesome CDN | Inline SVG / tree-shakeable icon libs | 2023+ | 400KB+ savings |
| Google Fonts external | Self-hosted fonts or optimized CDN | 2022+ | 200-300ms faster |
| Full Tailwind CDN | Tailwind CLI with purge | Always for production | 90%+ CSS reduction |
| FOIT (font blocking) | font-display: swap/optional | 2019+ | Better perceived performance |
| FID (First Input Delay) | INP (Interaction to Next Paint) | March 2024 | More comprehensive interactivity measure |

**Deprecated/outdated:**
- **FID metric:** Replaced by INP in Core Web Vitals (March 2024). INP measures all interactions, not just first.
- **Large icon fonts:** Tree-shakeable alternatives (Lucide, Heroicons) are preferred over monolithic icon fonts.

## Lighthouse Scoring Details

### Current Weights (Lighthouse 10)

| Metric | Weight | Target for 90+ |
|--------|--------|----------------|
| First Contentful Paint (FCP) | 10% | < 1.8s |
| Speed Index | 10% | < 3.4s |
| Largest Contentful Paint (LCP) | 25% | < 2.5s |
| Total Blocking Time (TBT) | 30% | < 200ms |
| Cumulative Layout Shift (CLS) | 25% | < 0.1 |

### Mobile 3G Throttling

Lighthouse mobile audit simulates:
- CPU: 4x slowdown
- Network: Slow 3G (~400kbps, 400ms latency)

This makes achieving 90+ challenging. Key strategies:
1. Minimize total payload (remove unused resources)
2. Prioritize LCP resource loading
3. Avoid long main thread tasks (TBT)
4. Prevent layout shifts (CLS)

## Verification Steps

### Pre-Optimization Baseline

1. Run Lighthouse on current page (mobile, simulated throttling)
2. Record scores: Performance, LCP, TBT, CLS
3. Test viewport at exactly 320px and 768px
4. Audit tap targets with Lighthouse accessibility audit

### Post-Optimization Verification

1. Run Lighthouse again, compare scores
2. Verify LCP < 2.5s
3. Verify no horizontal scroll at 320px
4. Verify all tap targets pass 44x44px audit
5. Test on real mobile device if possible

## Open Questions

1. **Tailwind CDN trade-off**
   - What we know: CDN cannot be purged, adds ~300KB
   - What's unclear: Acceptable to keep CDN in this phase, or must migrate?
   - Recommendation: Keep CDN for now. Migration to build-time Tailwind is separate scope. Focus on Font Awesome and fonts which have clearer wins.

2. **Self-host fonts vs optimize Google Fonts**
   - What we know: Self-hosting is 200-300ms faster but adds complexity
   - What's unclear: Whether Google Fonts with preconnect + swap achieves target
   - Recommendation: Start with optimized Google Fonts. Self-host only if LCP target not met.

## Sources

### Primary (HIGH confidence)
- [web.dev - Optimize Largest Contentful Paint](https://web.dev/articles/optimize-lcp) - LCP optimization strategies
- [Chrome DevTools - Lighthouse Performance Scoring](https://developer.chrome.com/docs/lighthouse/performance/performance-scoring) - Metric weights and thresholds
- [Tailwind CSS v3 - Optimizing for Production](https://v3.tailwindcss.com/docs/optimizing-for-production) - Build optimization guidance
- [WCAG 2.2 - Target Size (Minimum)](https://www.w3.org/WAI/WCAG22/Understanding/target-size-enhanced.html) - 44x44px requirement

### Secondary (MEDIUM confidence)
- [web.dev - Core Web Vitals](https://web.dev/articles/vitals) - LCP/CLS/INP thresholds
- [Smashing Magazine - Accessible Target Sizes](https://www.smashingmagazine.com/2023/04/accessible-tap-target-sizes-rage-taps-clicks/) - Tap target implementation
- [Tailwind CSS - Responsive Design](https://tailwindcss.com/docs/responsive-design) - Breakpoint system

### Tertiary (LOW confidence)
- Various web performance blog posts on Google Fonts vs self-hosted
- Font Awesome documentation on SVG alternatives

## Metadata

**Confidence breakdown:**
- Performance metrics & targets: HIGH - Official Google documentation
- Tap target requirements: HIGH - WCAG specification
- CDN optimization strategies: MEDIUM - Verified with multiple sources
- Lighthouse scoring weights: HIGH - Official Chrome documentation

**Research date:** 2026-02-03
**Valid until:** 2026-03-03 (Lighthouse scoring stable, 30-day validity)
