---
phase: 01-messaging-copy
plan: 01
subsystem: ui
tags: [landing-page, copywriting, messaging, benefit-focused]

# Dependency graph
requires: []
provides:
  - Benefit-focused hero section with category naming
  - Positive-framed problem section without negative visual elements
  - Two benefit-first feature cards (Quick Setup, Swaps)
affects: [01-02, 01-03] # subsequent messaging plans will build on this tone

# Tech tracking
tech-stack:
  added: []
  patterns:
    - Benefit-first headlines (outcome before feature name)
    - Problem-acknowledge-pivot (brief pain, quick solution)
    - Casual tone with contractions

key-files:
  created: []
  modified:
    - index.html

key-decisions:
  - "Hero headline 'Duties Handled, Effortlessly' (3 words) - prioritized brevity and benefit"
  - "Subtext explicitly names category: 'Duty scheduling for sports teams'"
  - "Problem section header 'From Spreadsheets to Simplicity' - positive outcome framing"
  - "Removed ban icon and 'The Old Chaos' label - replaced with neutral 'Before'"
  - "Privacy card removed from features - will be dedicated section in Plan 02"

patterns-established:
  - "Benefit-first headlines: lead with what users get, not feature names"
  - "Casual tone: contractions OK, active verbs, excitement energy"
  - "Problem framing: one sentence acknowledgment, pivot to solution"

# Metrics
duration: 2min
completed: 2026-02-02
---

# Phase 01 Plan 01: Hero, Problem & Features Copy Summary

**Benefit-focused landing page copy with 3-word hero headline, category naming, and casual tone across hero, problem, and features sections**

## Performance

- **Duration:** 2 min
- **Started:** 2026-02-02T09:29:35Z
- **Completed:** 2026-02-02T09:31:18Z
- **Tasks:** 3
- **Files modified:** 1

## Accomplishments
- Hero headline reduced to 3 words with effortless coordination benefit
- Hero subtext explicitly names "duty scheduling for sports teams"
- Problem section reframed from negative chaos language to positive outcome focus
- Removed ban icon and "Old Chaos" visual elements
- Feature cards use benefit-first headings: "Ready in Minutes", "Swaps Made Simple"
- Privacy card removed (dedicated section planned for Plan 02)

## Task Commits

Each task was committed atomically:

1. **Task 1: Rewrite hero section with benefit-focused messaging** - `ee4ba89` (feat)
2. **Task 2: Reframe problem section to positive messaging** - `5bdbd75` (feat)
3. **Task 3: Rewrite 2 feature cards to benefit-first** - `76d64cd` (feat)

## Files Created/Modified
- `index.html` - Hero, problem section, and features section copy updates

## Decisions Made
- Used "Duties Handled, Effortlessly" (3 words) instead of alternatives - brevity while maintaining benefit focus
- Changed "The Old Chaos" red label to neutral "Before" gray label - less negative while still showing contrast
- Kept the Excel/WhatsApp mockup as "before" visual but reduced opacity and removed ban icon
- Selected "Ready in Minutes" and "Swaps Made Simple" as benefit-first feature headings
- Documented privacy card content for Plan 02: "No more volunteer lists published on club website. Contact details stay private, visible only to those who need them."

## Deviations from Plan
None - plan executed exactly as written.

## Issues Encountered
None

## User Setup Required
None - no external service configuration required.

## Next Phase Readiness
- Hero, problem, and 2 feature cards ready with benefit-focused messaging
- Casual tone with contractions established as pattern
- Privacy section content documented and ready for dedicated section in Plan 02
- CTA section and final polish planned for subsequent plans

---
*Phase: 01-messaging-copy*
*Completed: 2026-02-02*
