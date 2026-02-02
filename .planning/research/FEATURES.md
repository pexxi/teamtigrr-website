# Feature Landscape: SaaS Landing Pages

**Domain:** SaaS Landing Pages for Junior Sports Duty Management
**Researched:** 2026-02-02
**Overall Confidence:** HIGH (based on multiple authoritative sources)

## Table Stakes

Features users expect. Missing = visitors bounce immediately.

| Feature | Why Expected | Complexity | Dependencies | Notes |
|---------|--------------|------------|--------------|-------|
| **Clear Value Proposition in Hero** | Nielsen Norman: users leave in 10-20 seconds without compelling value prop. 57% of page-viewing time is above the fold. | Low | None | Current page has this. Use "What-Why-How" formula. |
| **Single, Prominent CTA** | Adding second conversion goal drops conversions by up to 266%. Decision fatigue kills conversions. | Low | Value prop must be clear first | Current page: "Get Early Access" - good. |
| **Mobile-First Responsive Design** | 83% of landing page visits are mobile (Unbounce). Google mobile-first indexing is standard. | Medium | None | Not negotiable in 2026. |
| **Fast Page Load (<2.5s LCP)** | Google: LCP >2.5s increases bounce by 32%; at 4s it exceeds 90%. | Medium | Hosting, image optimization | Current CDN-loaded Tailwind may need review. |
| **Social Proof** | 88% of buyers trust reviews as much as personal recommendations. 97% say reviews impact purchasing decisions. | Low | Requires real testimonials/logos | **Current gap**: Page lacks testimonials, logos, or reviews. |
| **Benefits Over Features** | Visitors care about outcomes, not capabilities. Feature-focused copy underperforms outcome-driven messaging. | Low | None | Current page does this well - focuses on pain points. |
| **Contact/Signup Form** | Core conversion mechanism. Median SaaS conversion is 3.8%, top performers hit 10-15%. | Low | Backend integration | Current page has this - minimal fields (email, sport, role). |
| **HTTPS/Security Indicators** | 61% of buyers don't purchase when trust seals are missing. | Low | SSL certificate | Standard hosting handles this. |
| **Privacy Policy Link** | Legal requirement in most jurisdictions. Trust signal. | Low | Privacy policy page | Current page has footer link. |

## Differentiators

Features that set product apart. Not expected, but valued when present.

| Feature | Value Proposition | Complexity | Dependencies | Notes |
|---------|-------------------|------------|--------------|-------|
| **Interactive Product Demo** | "Interactive demos convert 2x better than static screenshots; leads close 20-25% faster." | High | Working demo component | Current page has a static mock-up. Consider animated walkthrough. |
| **Video Demo/Explainer** | Visual demonstration builds trust faster than text. Users want to see how it works before signing up. | Medium | Video production, hosting | Could be simple screen recording. |
| **Real Customer Testimonials with Photos** | Video testimonials add authenticity and relatability. Named quotes beat anonymous ones. | Medium | Beta user relationships | **High priority for post-beta launch.** |
| **Before/After Comparison** | Shows transformation clearly. Current "Excel chaos" visual does this well. | Low | Design work | **Current strength** - the spreadsheet vs. app comparison is effective. |
| **Benefit-Focused Micro-Animations** | Story-driven heroes with motion outperform static pages (2026 trend). | Medium | Animation implementation | Current page has subtle hover states only. |
| **Live G2/Capterra Review Widgets** | Verifiable third-party proof. 2026 buyers hunt for unbiased evidence. | Medium | Actual reviews on platforms | Future consideration once reviews exist. |
| **Case Study Snippets** | Real-world proof with numbers (e.g., "Tigers U12 saved 3 hours/week"). | Low | Beta user data | Can add after beta testing. |
| **ROI Calculator** | Lets visitors quantify value themselves. Particularly effective for decision-makers. | High | Interactive component | Future consideration for team leaders evaluating adoption. |
| **FAQ Section** | Reduces objections and support load. Addresses "but what about..." questions. | Low | Content creation | **Missing from current page** - would help with common objections. |
| **"How It Works" Section** | 3-step visual process builds understanding. | Low | Design work | Could enhance current features section. |
| **Pricing/Free Tier Clarity** | Hidden pricing erodes trust. "Free beta" is clear but long-term pricing should be addressed. | Low | Pricing strategy decision | Current "free beta" messaging is appropriate for this stage. |

## Anti-Features

Features to explicitly NOT build. Common mistakes in this domain.

| Anti-Feature | Why Avoid | What to Do Instead |
|--------------|-----------|-------------------|
| **Navigation Menu on Landing Page** | UX studies: dedicated landing pages convert 40% better than homepages. Navigation creates exit points. | Keep minimal nav or remove entirely for campaign pages. Current nav is acceptable for a homepage-style landing page. |
| **Multiple Competing CTAs** | Each additional goal drops conversions significantly. Decision fatigue. | One primary CTA ("Get Early Access") repeated strategically. Secondary links should be clearly subordinate. |
| **Long Form Fields** | Shopify asks for one thing: email. Every field costs conversions. | Current 3 fields (email, sport, role) is reasonable for qualification. Don't add more. |
| **Feature Lists Above the Fold** | Jargon and features don't convert. Outcomes do. | Lead with pain point and promise, not capabilities. |
| **Full Website Navigation/Footer Links** | Every link is an exit point. | Keep footer minimal. Remove any links that don't support conversion. |
| **Stock Photos** | "Cheesy stock photos can make or break your entire website... they can end up looking amateur, low-budget, and even suspicious." | Use product screenshots, illustrations, or real photos. Current page uses illustrations effectively. |
| **Vague "Welcome" Headlines** | "Welcome to Our Website" provides zero value. | Specific, benefit-driven headlines. Current "Every Game Covered" is strong. |
| **AI-Generated Generic Copy** | "Visitors can easily pick up on generic phrasing and canned lines, and when they do, trust can take a real blow." | Write authentic, specific copy. Use real team/parent language. |
| **Autoplay Video with Sound** | Disrupts user experience, causes immediate bounce. | If video, make it muted by default with clear play controls. |
| **Popup on Page Load** | Interrupts before value is communicated. | If needed, use exit-intent or scroll-trigger instead. |
| **Excessive Social Media Icons** | Each icon is an exit point. | Keep social links in footer only, not prominent. |
| **Keyword-Stuffed Copy** | Destroys readability for marginal SEO benefit. | Write for humans first. Natural keyword usage. |
| **Pricing Page Link (Pre-Product)** | For beta/pre-launch, pricing links to empty pages break trust. | "Free beta" or "pricing coming soon" is appropriate. |
| **Blog/Resource Links** | Exit points that distract from conversion. | Save for main website, not landing page. |

## Feature Dependencies

```
Value Prop (Hero)
    └── CTA Button (requires clear value to be effective)
         └── Signup Form (CTA leads here)
              └── Backend Integration (form needs somewhere to submit)

Social Proof
    └── Beta Users (requires actual users for testimonials)
         └── G2/Capterra Reviews (requires enough users)

Interactive Demo
    └── Working Product (can't demo what doesn't exist)
         └── Demo Environment (sandbox version of product)

Video Demo
    └── Product Visuals (needs something to show)
         └── Video Hosting (Vimeo, YouTube, or self-hosted)
```

## Current Page Assessment

**What the Current Page Has (Table Stakes Covered):**
- Clear value proposition ("Every Game Covered. Every Duty Handled.")
- Single primary CTA ("Get Early Access")
- Mobile-responsive design
- Benefits-focused copy
- Pain point visualization (spreadsheet chaos)
- Minimal signup form
- Privacy/Terms links in footer

**Critical Gaps to Address:**

1. **Social Proof** (High Priority)
   - No testimonials
   - No client logos
   - No user count or credibility indicators
   - Recommendation: Add beta user testimonials or "Trusted by X teams" once available

2. **FAQ Section** (Medium Priority)
   - Common objections not addressed
   - Recommendation: Add 4-6 FAQs addressing: cost, setup time, sports supported, privacy, switching from current system

3. **How It Works** (Low Priority)
   - Features section exists but could be clearer step-by-step
   - Recommendation: Optional enhancement with 3-step visual process

**What's Working Well:**
- Before/after comparison (spreadsheet vs. app) is a strong differentiator
- Sporty, energetic design matches brand
- Beta badge creates urgency
- Product mock-up shows interface concept

## MVP Landing Page Recommendation

For initial launch, prioritize:

1. **Social Proof Placeholder** - Add "Trusted by [X] teams in beta" once beta teams exist. For now, could add "Built by sports parents" or team leader credibility.
2. **FAQ Section** - 4-6 questions addressing common objections
3. **Speed Optimization** - Verify LCP is under 2.5s

Defer to post-MVP:
- Interactive demo: Requires working product
- Video demo: Can wait until product is stable
- G2/Capterra widgets: Requires enough users
- ROI calculator: Advanced feature for later

## Sources

- [Unbounce: SaaS Landing Page Best Practices](https://unbounce.com/conversion-rate-optimization/the-state-of-saas-landing-pages/) - MEDIUM confidence
- [SaaSFrame: 2026 Landing Page Trends](https://www.saasframe.io/blog/10-saas-landing-page-trends-for-2026-with-real-examples) - MEDIUM confidence
- [Webstacks: SaaS Website Conversions 2026](https://www.webstacks.com/blog/website-conversions-for-saas-businesses) - MEDIUM confidence
- [Fibr.ai: SaaS Landing Pages Best Practices](https://fibr.ai/landing-page/saas-landing-pages) - MEDIUM confidence
- [Heyflow: SaaS Landing Page Best Practices](https://heyflow.com/blog/saas-landing-page-best-practices/) - MEDIUM confidence
- [SwipePages: Social Proof Types](https://swipepages.com/blog/7-proven-social-proof-types-to-build-trust-on-your-landing-page/) - MEDIUM confidence
- [Klientboost: Landing Page Testimonials](https://www.klientboost.com/landing-pages/landing-page-testimonials/) - MEDIUM confidence
- [Moosend: Landing Page Mistakes 2026](https://moosend.com/blog/landing-page-mistakes/) - MEDIUM confidence
- [Abmatic: SaaS Landing Page Mistakes](https://abmatic.ai/blog/top-saas-landing-page-mistakes-to-avoid) - MEDIUM confidence
- Nielsen Norman Group studies on above-the-fold attention - HIGH confidence (widely cited, authoritative)
- BrightLocal Consumer Review Survey data - HIGH confidence (industry standard source)
