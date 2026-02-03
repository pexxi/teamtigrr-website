# Phase 2: Content Sections - Research

**Researched:** 2026-02-03
**Domain:** Landing Page Content Sections (FAQ, Social Proof, How It Works)
**Confidence:** HIGH

## Summary

This phase adds three missing content sections to the TeamTigrr landing page: FAQ, Social Proof, and "How It Works". Research focuses on proven patterns for static HTML/Tailwind CSS implementation, specifically leveraging native HTML elements (`<details>/<summary>`) to avoid JavaScript dependencies.

The page is a static HTML file using Tailwind CSS via CDN. All new sections must match the existing design system (dark theme, orange accents, Teko/Inter fonts) and work without JavaScript frameworks. The research identifies proven patterns from 2026 landing page best practices.

**Primary recommendation:** Add lightweight social proof after hero, 3-step "How It Works" between problem and features, and accordion-style FAQ before the final CTA section.

## Standard Stack

This phase is HTML/CSS only using existing setup.

### Core (Already in Use)
| Tool | Version | Purpose | Why Standard |
|------|---------|---------|--------------|
| Tailwind CSS | CDN (v3.x) | Utility-first CSS | Already loaded, no build required |
| Font Awesome | 6.4.0 CDN | Icons | Already loaded, provides needed icons |
| Native HTML | `<details>` | Accordion behavior | Zero JavaScript, native accessibility |

### No New Dependencies
This phase explicitly uses only what's already in `index.html`. No new libraries, scripts, or build tools.

### Alternatives Considered
| Instead of | Could Use | Tradeoff |
|------------|-----------|----------|
| `<details>` accordion | JavaScript accordion | JS adds complexity; native HTML handles FAQ perfectly |
| Font Awesome icons | Lucide (tree-shakeable) | Deferred to v2, FA already loaded |
| Static numbers | Live counters | No backend yet; static sufficient for beta |

## Architecture Patterns

### Recommended Section Order

Based on ARCHITECTURE.md and 2026 landing page research:

```
Current                        After Phase 2
--------                       -------------
1. Hero                   ->   1. Hero
                          ->   2. Social Proof (NEW - lightweight bar)
2. Problem                ->   3. Problem
                          ->   4. How It Works (NEW - 3 steps)
3. Privacy                ->   5. Privacy
4. Features               ->   6. Features
5. Sports                 ->   7. Sports
                          ->   8. FAQ (NEW - accordion)
6. CTA                    ->   9. CTA
7. Footer                 ->   10. Footer
```

**Rationale:**
- Social proof immediately after hero builds trust before asking visitors to read
- "How It Works" between problem and features makes the solution tangible
- FAQ before CTA removes final objections right before conversion point

### Pattern 1: Lightweight Social Proof Bar

**What:** A simple trust indicator immediately after the hero section
**When to use:** Early stage products without extensive testimonials
**Position:** Between hero and problem section

**Design:**
- Dark background (matches site theme)
- Single line: tagline + subtle visual indicator
- No testimonial quotes (waiting for beta feedback)
- "Built by sports parents" messaging per requirements

**Example structure:**
```html
<div class="bg-tigrr-charcoal border-y border-gray-800 py-4">
  <div class="max-w-7xl mx-auto px-4 text-center">
    <p class="text-gray-400">
      <i class="fas fa-heart text-tigrr-orange mr-2"></i>
      <span class="text-white font-medium">Built by sports parents</span>
      for sports parents
    </p>
  </div>
</div>
```

### Pattern 2: 3-Step "How It Works"

**What:** Visual 3-step process showing simplicity of the product
**When to use:** SaaS products where complexity is an objection
**Position:** After problem section, before features

**Design principles:**
- 3 steps only (3-5 is ideal per research, 3 is perfect for simplicity messaging)
- Numbered circles with icons
- Short headline (2-4 words) + brief description
- Horizontal on desktop, stacked on mobile
- Optional: connecting line between steps (decorative)

**TeamTigrr-specific steps:**
1. **Add Your Games** - Import your schedule or add games manually
2. **Assign Duties** - AI suggests fair assignments, you approve
3. **Relax** - Parents get notified, swaps happen automatically

**Layout:**
```
[1. Add Games] -----> [2. Assign] -----> [3. Relax]
```

### Pattern 3: Accordion FAQ (No JavaScript)

**What:** Expandable FAQ section using native HTML `<details>` element
**When to use:** Any FAQ section - accessibility built-in, no JS needed
**Position:** Before final CTA section

**Implementation approach:**
- Use `<details>` and `<summary>` elements (native HTML5)
- Tailwind's `group-open:` classes for rotation/styling
- First question open by default (shows interaction affordance)
- 4-6 questions addressing key objections

**HTML pattern:**
```html
<details class="group" open>
  <summary class="flex items-center cursor-pointer ...">
    <svg class="transition group-open:rotate-90 ...">...</svg>
    <span>Question here?</span>
  </summary>
  <div class="px-4 pb-4">
    <p>Answer here.</p>
  </div>
</details>
```

### Anti-Patterns to Avoid

- **JavaScript accordions:** Native `<details>` works perfectly, is accessible, and requires zero JS
- **Carousel testimonials:** For social proof - static is better than carousel (users skip carousels)
- **Generic social proof:** "Trusted by thousands" without specifics feels like marketing speak
- **Too many FAQ questions:** 4-6 is ideal; more becomes overwhelming
- **Long FAQ answers:** Brief, scannable answers convert better

## Don't Hand-Roll

| Problem | Don't Build | Use Instead | Why |
|---------|-------------|-------------|-----|
| Accordion expand/collapse | JavaScript toggle | `<details>` + `<summary>` elements | Native HTML, accessible, works without JS |
| Arrow rotation animation | CSS keyframes | `group-open:rotate-90` Tailwind class | Built-in, one class |
| Step connector line | Custom SVG path | Simple border or flex with gap | Good enough; complex SVG adds maintenance |
| Social proof counter | Real-time API | Static number or "Built by parents" | No backend data yet |

**Key insight:** Native HTML5 elements (`<details>`, `<summary>`) provide accordion behavior for free. Custom JavaScript accordion components add complexity without benefit for FAQ sections.

## Common Pitfalls

### Pitfall 1: FAQ Too Generic
**What goes wrong:** Questions don't address actual visitor objections
**Why it happens:** Writing FAQ without considering buyer journey
**How to avoid:** Focus on objections from requirements: cost, setup time, privacy, switching
**Warning signs:** Questions feel like feature documentation, not objection handling

### Pitfall 2: "How It Works" Too Technical
**What goes wrong:** Steps describe system mechanics instead of user experience
**Why it happens:** Product knowledge bias
**How to avoid:** Each step should start with a user action verb, end with user benefit
**Warning signs:** Steps mention database, sync, backend, API

### Pitfall 3: Social Proof Too Ambitious
**What goes wrong:** Placeholder testimonials look fake
**Why it happens:** Wanting to look established before having real users
**How to avoid:** Use authentic placeholder: "Built by sports parents" is true and humble
**Warning signs:** Fake names, stock photos, made-up quotes

### Pitfall 4: Breaking Visual Flow
**What goes wrong:** New sections look bolted-on, not integrated
**Why it happens:** Not matching existing design patterns
**How to avoid:** Match section patterns: dark/light alternation, consistent spacing, same typography
**Warning signs:** Different padding, new colors, inconsistent fonts

### Pitfall 5: Non-Responsive Sections
**What goes wrong:** Content looks broken on mobile
**Why it happens:** Testing only on desktop
**How to avoid:** Use Tailwind responsive prefixes (`md:`, `lg:`), mobile-first approach
**Warning signs:** Horizontal overflow, tiny text, cramped spacing on mobile

## Code Examples

Verified patterns adapted for TeamTigrr's design system.

### Social Proof Bar
```html
<!-- Position: After hero section closing div, before problem section -->
<div class="bg-tigrr-charcoal border-y border-gray-800 py-6">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 text-center">
        <p class="text-gray-400 text-lg">
            <i class="fas fa-heart text-tigrr-orange mr-2"></i>
            <span class="text-white font-semibold">Built by sports parents</span>
            who were tired of the spreadsheet shuffle
        </p>
    </div>
</div>
```

### How It Works Section
```html
<!-- Position: After problem section, before privacy section -->
<div id="how-it-works" class="bg-tigrr-dark py-20 border-t border-gray-800">
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-16">
            <h2 class="text-tigrr-orange font-semibold tracking-wide uppercase text-sm">Simple Setup</h2>
            <h2 class="text-3xl md:text-5xl font-display font-bold text-white mt-2">How It Works</h2>
        </div>

        <div class="grid md:grid-cols-3 gap-8 md:gap-12 max-w-4xl mx-auto">
            <!-- Step 1 -->
            <div class="text-center">
                <div class="flex items-center justify-center w-16 h-16 mx-auto bg-tigrr-orange rounded-full mb-6">
                    <span class="text-2xl font-display font-bold text-white">1</span>
                </div>
                <h3 class="text-xl font-bold text-white mb-3">Add Your Games</h3>
                <p class="text-gray-400">Import your season schedule or add games one by one. Takes about 5 minutes.</p>
            </div>

            <!-- Step 2 -->
            <div class="text-center">
                <div class="flex items-center justify-center w-16 h-16 mx-auto bg-tigrr-orange rounded-full mb-6">
                    <span class="text-2xl font-display font-bold text-white">2</span>
                </div>
                <h3 class="text-xl font-bold text-white mb-3">Assign Duties</h3>
                <p class="text-gray-400">Our smart assistant suggests fair assignments. You review and approve with one click.</p>
            </div>

            <!-- Step 3 -->
            <div class="text-center">
                <div class="flex items-center justify-center w-16 h-16 mx-auto bg-tigrr-orange rounded-full mb-6">
                    <span class="text-2xl font-display font-bold text-white">3</span>
                </div>
                <h3 class="text-xl font-bold text-white mb-3">Relax</h3>
                <p class="text-gray-400">Parents get notified automatically. Swaps happen without your involvement.</p>
            </div>
        </div>
    </div>
</div>
```

### FAQ Section with Accordion
```html
<!-- Position: After sports section, before CTA section -->
<div id="faq" class="bg-tigrr-charcoal py-20 border-t border-gray-800">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
        <div class="text-center mb-12">
            <h2 class="text-3xl md:text-4xl font-display font-bold text-white">Frequently Asked Questions</h2>
        </div>

        <div class="divide-y divide-gray-700">
            <!-- Question 1 - Open by default -->
            <details class="group py-4" open>
                <summary class="flex items-center justify-between cursor-pointer list-none">
                    <span class="text-lg font-semibold text-white">Is TeamTigrr free?</span>
                    <svg class="w-5 h-5 text-gray-400 transition-transform group-open:rotate-180" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                    </svg>
                </summary>
                <p class="mt-4 text-gray-400">Yes! During our beta period, TeamTigrr is completely free. We're looking for teams to help us refine the experience before our official launch.</p>
            </details>

            <!-- Question 2 -->
            <details class="group py-4">
                <summary class="flex items-center justify-between cursor-pointer list-none">
                    <span class="text-lg font-semibold text-white">How long does setup take?</span>
                    <svg class="w-5 h-5 text-gray-400 transition-transform group-open:rotate-180" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                    </svg>
                </summary>
                <p class="mt-4 text-gray-400">Most team leaders are up and running in under 10 minutes. Add your games, invite parents via a link, and you're ready to go.</p>
            </details>

            <!-- Question 3 -->
            <details class="group py-4">
                <summary class="flex items-center justify-between cursor-pointer list-none">
                    <span class="text-lg font-semibold text-white">What about privacy? Where does our data go?</span>
                    <svg class="w-5 h-5 text-gray-400 transition-transform group-open:rotate-180" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                    </svg>
                </summary>
                <p class="mt-4 text-gray-400">Your data stays yours. Contact details are only visible to team leaders and assigned duty partners. We never sell data or show public volunteer lists.</p>
            </details>

            <!-- Question 4 -->
            <details class="group py-4">
                <summary class="flex items-center justify-between cursor-pointer list-none">
                    <span class="text-lg font-semibold text-white">Can we switch from our current system?</span>
                    <svg class="w-5 h-5 text-gray-400 transition-transform group-open:rotate-180" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                    </svg>
                </summary>
                <p class="mt-4 text-gray-400">Absolutely. Whether you're using spreadsheets, WhatsApp, or another app, TeamTigrr works alongside your existing tools. Start small - try it for one team first.</p>
            </details>

            <!-- Question 5 -->
            <details class="group py-4">
                <summary class="flex items-center justify-between cursor-pointer list-none">
                    <span class="text-lg font-semibold text-white">What sports does TeamTigrr support?</span>
                    <svg class="w-5 h-5 text-gray-400 transition-transform group-open:rotate-180" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
                    </svg>
                </summary>
                <p class="mt-4 text-gray-400">Currently basketball, football (soccer), and ice hockey. We're adding more sports based on user requests - just let us know what you need!</p>
            </details>
        </div>
    </div>
</div>
```

### CSS for Details/Summary (add to style block)
```css
/* Hide default details marker in all browsers */
details summary::-webkit-details-marker {
    display: none;
}
details summary::marker {
    display: none;
}
```

## State of the Art

| Old Approach | Current Approach | When Changed | Impact |
|--------------|------------------|--------------|--------|
| JavaScript accordions | Native `<details>` element | 2023+ | Zero JS, better accessibility |
| Carousel testimonials | Static social proof bars | 2024+ | Higher engagement (users skip carousels) |
| Long "how it works" | 3 steps max | 2024+ | Reduced cognitive load |
| Generic FAQ pages | Embedded FAQ sections | 2025+ | Keeps visitors in conversion flow |
| "Trusted by thousands" | Specific, authentic proof | 2025+ | Higher trust scores |

**2026 Trends:**
- Minimalist layouts with generous whitespace
- Real interface visuals over abstract illustrations
- Social proof placed near CTAs for "moment of decision" trust
- FAQ with schema markup for SEO/AEO (Answer Engine Optimization)

**Deprecated/outdated:**
- Testimonial carousels: Users skip them, static is better
- JavaScript accordions for FAQ: Native HTML works perfectly
- Separate FAQ pages: Embedded FAQ keeps conversion flow intact

## Open Questions

1. **FAQ Schema Markup**
   - What we know: Adding FAQ schema helps SEO and may show in "People Also Ask"
   - What's unclear: Whether to add schema now or defer to SEO phase
   - Recommendation: Add JSON-LD schema in Phase 2 (low effort, good SEO benefit)

2. **How It Works - Connector Line**
   - What we know: Many designs use decorative connector lines between steps
   - What's unclear: Whether to add complexity for visual enhancement
   - Recommendation: Skip connector line initially; cleaner without, add later if needed

3. **Social Proof - Future Testimonials**
   - What we know: Current "Built by sports parents" is placeholder for real testimonials
   - What's unclear: Structure for future testimonial section
   - Recommendation: Keep placeholder simple; testimonial structure is v2 requirement (CONT-05)

## Sources

### Primary (HIGH confidence)
- [Tailwind Flex - Accordion FAQ](https://tailwindflex.com/@sophia-baker/accordion-faq) - Native HTML accordion pattern
- [Tailwind Flex - Steps Section](https://tailwindflex.com/@anonymous/steps-section-for-explaining-process) - 3-step process layout
- [MDN - Details Element](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/details) - Native HTML accordion

### Secondary (MEDIUM confidence)
- [Landingi - FAQ Landing Page Guide](https://landingi.com/landing-page/faq/) - FAQ best practices
- [SaaSFrame - Landing Page Trends 2026](https://www.saasframe.io/blog/10-saas-landing-page-trends-for-2026-with-real-examples) - How It Works patterns
- [Nudgify - Social Proof Landing Pages 2026](https://www.nudgify.com/social-proof-landing-pages/) - Social proof placement
- [SaaS Hero - B2B Landing Page Trends 2026](https://www.saashero.net/content/top-landing-page-design-trends/) - Design patterns
- [MailerLite - Social Proof Examples](https://www.mailerlite.com/blog/social-proof-examples-for-landing-pages) - Social proof types
- [Fibr AI - SaaS Landing Pages 2026](https://fibr.ai/landing-page/saas-landing-pages) - How It Works best practices

### Tertiary (LOW confidence)
- General Tailwind patterns from training data - verified against 2026 sources above

## Metadata

**Confidence breakdown:**
- Social Proof pattern: HIGH - Multiple sources confirm placement and format
- How It Works structure: HIGH - Consistent 3-step pattern across sources
- FAQ accordion: HIGH - Native HTML `<details>` is standard practice
- Section ordering: MEDIUM - Based on ARCHITECTURE.md and conversion research
- Visual design: HIGH - Matches existing page patterns exactly

**Research date:** 2026-02-03
**Valid until:** 2026-03-03 (HTML patterns stable, 30-day validity)

---

*Phase: 02-content-sections*
*Research complete: 2026-02-03*
