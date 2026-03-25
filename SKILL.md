---
name: clearshot
description: "Visual intelligence for AI interfaces. Two modes: Define (generate taste.md — your project's visual identity and standards) and Verify (screenshot live UI and audit against taste.md). Uses browser tools to see what users see — not source code, the actual rendered page. Trigger on: 'audit UI', 'check taste', 'generate taste', 'review design', 'screenshot analysis', 'taste your UI'. Skip for non-UI images."
---

# Clearshot — Visual Intelligence for AI Interfaces

You see what users see. You navigate to the live page, screenshot it, measure computed values, and judge the result. You do not read CSS files and guess — you open the browser and look.

Two modes:
1. **Define** — Generate `taste.md`: design identity, standards, component taxonomy, anti-patterns
2. **Verify** — Screenshot live UI, audit against `taste.md`, report with fixes

## Entry point

When triggered, check if `taste.md` exists in the project root.

- **No taste.md**: Run Define mode. Ask the user for input or go autonomous (see below).
- **taste.md exists**: Run Verify mode. Screenshot and audit against it.
- **User says "full"**: Run Define then immediately Verify.

---

## Mode 1: Define — Generate taste.md

taste.md is not a token inventory. It is a **design projection** — a holistic understanding of what this product should look and feel like, derived from everything available.

### Sources of truth (use ALL of them)

1. **User intent** — What the user has said across the entire conversation. Their goals, frustrations, emotional language, aesthetic preferences, references they've shared. "Make it feel native" is a design decision. "I want clarity" is a constraint. "It's too light" is a measurement.
2. **Product context** — What the product does, who it serves, what outcome users seek. A contest platform for creative writers has a different taste than a billing dashboard. Read the copy, the page structure, the feature set.
3. **Existing visual decisions** — CSS/Tailwind config, font imports, color palette, spacing patterns, component structures. These are decisions already made — respect them or challenge them, but know them.
4. **Audience expectations** — What do the users of THIS product expect? What are they used to? What would feel wrong to them? A teen social app and an enterprise SaaS have different cognitive baselines.
5. **What hasn't been said** — Infer from the product's positioning. If the copy is warm and personal, the UI shouldn't be cold and corporate. If the product is about creativity, the layout shouldn't be rigid.

### Two approaches

**Ask mode** — when nuance matters, prompt the user:
1. Who uses this and what do they expect?
2. What feeling should this evoke? (not "modern" — that's nothing. "Warm but authoritative" is something.)
3. Reference sites or screenshots?
4. What currently bothers you about the UI?

**Autonomous mode** — when speed matters or user says "go yolo":
1. Read every source above silently
2. Generate taste.md with strong opinionated defaults
3. Better to be specific and wrong than vague and useless — the user will correct what matters

### taste.md specification

Generate `taste.md` in the project root:

```markdown
# Taste — {Project Name}

## Identity
{One sentence. What this is and who it's for.}

## Principles
{3-5 ordered design principles.}
{Each principle is a decision, not a platitude. "Clarity over decoration" > "Good design."}

## Visual Language

### Palette
| Role | Hex | Notes |
|------|-----|-------|
| Page background | #___ | |
| Surface (cards) | #___ | |
| Primary action | #___ | CTAs, links, accents |
| Text primary | #___ | Headings |
| Text body | #___ | Paragraphs |
| Text secondary | #___ | Supporting |
| Text muted | #___ | Captions, meta |
| Border | #___ | Card edges, dividers |
| Error | #___ | Validation |
| Success | #___ | Confirmations |

### Typography
| Role | Family | Size | Weight | Case | Tracking |
|------|--------|------|--------|------|----------|
| Display | ___ | ___px | ___ | ___ | ___ |
| Heading | ___ | ___px | ___ | ___ | ___ |
| Subheading | ___ | ___px | ___ | ___ | ___ |
| Body | ___ | ___px / ___lh | ___ | ___ | ___ |
| Label | ___ | ___px | ___ | ___ | ___ |
| Caption | ___ | ___px | ___ | ___ | ___ |

### Spacing
Base unit: ___px
Section gap: ___px
Card padding: ___px
Element gap: ___px
Dense gap: ___px

### Shape
Card radius: ___px
Button radius: ___px (or pill)
Input radius: ___px
Avatar radius: ___px (or circle)

### Depth (shadow values)
| Level | Shadow | Usage |
|-------|--------|-------|
| Flat | none | Non-interactive containers |
| Raised | ___ | Interactive surfaces |
| Elevated | ___ | Modals, dropdowns, popovers |
| Button | ___ | Action elements (may include colored shadow) |

## Component Taxonomy

Every visible element falls into one of these categories. Each has a distinct visual signature. Users should identify the category in under one second.

### Static containers
{Appearance: flat, no shadow, faint border or none, white/surface bg}
{Signal: "I hold content. Don't click me."}
{Cursor: default}
{Hover: none}

### Interactive surfaces
{Appearance: raised with shadow, visible border, white/surface bg}
{Signal: "I'm a doorway. Click to go somewhere."}
{Cursor: pointer}
{Hover: border tints toward primary, faint primary bg wash, shadow deepens}

### Action buttons — primary
{Appearance: filled primary color, pill shape, 2px border, colored shadow}
{Signal: "I trigger an action. Click to do something."}
{Cursor: pointer}
{Hover: darkens, shadow intensifies}
{Active: scale down (0.97)}

### Action buttons — secondary
{Appearance: outlined, pill shape, 2px border (thicker than card borders), tinted or white bg}
{Signal: "I'm an alternative action."}
{Cursor: pointer}
{Hover: border darkens, bg tints}
{Active: scale down (0.97)}

### Form inputs
{Appearance: white bg, visible border, rounded (not pill), focus ring on interaction}
{Cursor: text/pointer depending on type}
{Focus: primary-colored ring or border}

### Text links
{Appearance: colored text (primary), optional underline}
{Cursor: pointer}
{Hover: underline or color shift}

## Anti-patterns — project-specific
{5-10 specific things that would violate this project's taste.}
{e.g., "No drop shadows heavier than 0 4px 20px", "Never use opacity below 0.4 for text"}

## AI Slop Indicators — universal
These patterns indicate the UI was generated carelessly. If you see them, flag immediately:
- Generic purple-blue-on-white SaaS palette with no brand connection
- Gradient text headings
- Glassmorphism / frosted glass cards with no functional purpose
- Dashboard hero with exactly 4 metric stat cards in a row
- Card grids where every card is forced to identical height
- Bounce/elastic easing on every animation
- Generic stock-illustration style (isometric people, abstract blobs)
- Placeholder copy that shipped ("Lorem ipsum", "Acme Corp", "John Doe")
- Shadows on everything — no depth hierarchy, just uniform depth
- Components that look identical but serve different purposes (buttons = cards = inputs)
```

### Validation

After generating taste.md, verify it against the existing codebase:
1. Do the specified colors match what's in the CSS/Tailwind config?
2. Do the font families match what's imported?
3. Are the anti-patterns grounded in reality for this project?
4. Does the component taxonomy match the actual CSS classes?

Fix any discrepancies before saving.

---

## Mode 2: Verify — Audit the live UI

### Capture protocol

Use `cursor-ide-browser` MCP tools in this order:

1. **Navigate**: `browser_navigate` to target URL with `take_screenshot_afterwards: true`
2. **Lock**: `browser_lock` to prevent interference
3. **Screenshot**: `browser_take_screenshot` for above-fold
4. **Scroll and capture**: `browser_scroll` down, `browser_take_screenshot` — repeat until page bottom
5. **Extract computed styles**: `browser_console` to get real values:
   ```js
   (function(){
     var body = getComputedStyle(document.body);
     var h1 = document.querySelector('h1,h2');
     var card = document.querySelector('[class*=card]');
     var btn = document.querySelector('button,.btn');
     return JSON.stringify({
       bodyBg: body.backgroundColor,
       bodyFont: body.fontFamily,
       bodyColor: body.color,
       h1Size: h1 ? getComputedStyle(h1).fontSize : null,
       h1Weight: h1 ? getComputedStyle(h1).fontWeight : null,
       cardBg: card ? getComputedStyle(card).backgroundColor : null,
       cardShadow: card ? getComputedStyle(card).boxShadow : null,
       cardBorder: card ? getComputedStyle(card).border : null,
       btnBg: btn ? getComputedStyle(btn).backgroundColor : null,
       btnBorder: btn ? getComputedStyle(btn).border : null,
       btnRadius: btn ? getComputedStyle(btn).borderRadius : null,
     }, null, 2);
   })()
   ```
6. **Responsive test**: `browser_resize` to each breakpoint, screenshot each:
   - **Mobile**: 375×812
   - **Tablet**: 768×1024
   - **Desktop wide**: 1440×900
7. **Unlock**: `browser_unlock` when all captures are done

### Analysis

Run every layer. Skip nothing.

#### Layer 1: Spatial Grid

Divide the screenshot into a **5×5 grid**. For each occupied cell:
- What section lives there (nav, hero, sidebar, content, footer, modal, empty space)
- Approximate size relative to viewport
- Relationship to neighbors

For every visible element, capture:
- **Type**: button, input, card, image, icon, text, link, toggle, tab, badge, avatar, table, chart
- **Label**: exact visible text
- **Position**: grid cell + relative placement
- **State**: default, hover, active, disabled, selected, error, loading
- **Size**: pixel estimate
- **Background**: hex
- **Text color**: hex
- **Border**: visible/none, width, radius in px
- **Shadow**: none / sm / md / lg / colored
- **Icon**: if present, which one

Group by section. Note: where the eye lands first, whether hierarchy is clear or competing, whether the layout breathes or suffocates, what feels intentional vs accidental.

#### Layer 2: Taste Check

Load the project's `taste.md`. Check every observation against it:

| Check | Method |
|-------|--------|
| Palette match | Compare screenshot colors to taste.md hex values |
| Typography scale | Compare rendered sizes/weights to taste.md spec |
| Spacing consistency | Measure gaps between sections, cards, elements |
| Component taxonomy | Is each element visually categorized per the taxonomy? |
| Anti-pattern scan | Are any project-specific anti-patterns present? |
| AI slop scan | Are any universal slop indicators visible? |

For each deviation: state what should be (per taste.md), what is (measured), severity, and the specific CSS/HTML fix.

#### Layer 3: Cognitive Load

Three dimensions. Grade each A through F.

**Clarity** — Can a user identify every element's purpose in <1 second?
- Can you tell buttons from cards from inputs instantly?
- Is the hierarchy (primary → secondary → tertiary) obvious without reading?
- Are non-interactive elements obviously non-interactive?
- Are interactive elements obviously interactive?
- Could a first-time user navigate without instructions?

**Action** — Can a user find the primary action in <2 seconds?
- Is there one clear CTA per viewport?
- Do secondary actions visually recede?
- Are destructive actions gated (confirmation, different color)?
- Does the eye path lead naturally toward the action?

**Delight** — Does any element spark interest or reward attention?
- Is there purposeful motion (not decoration)?
- Are there visual details that reward a second look?
- Does the interface feel crafted or generated?
- Would a user screenshot this to share?

#### Layer 4: Accessibility

Measure on the live rendered page:

| Check | Standard | Method |
|-------|----------|--------|
| Text contrast | WCAG AA: 4.5:1 (normal), 3:1 (large) | Computed bg + fg colors → calculate ratio |
| Touch targets | ≥44×44px | Measure interactive element dimensions |
| Focus indicators | Visible focus ring on tab | Tab through page, screenshot |
| Heading hierarchy | h1 → h2 → h3, no skips | Inspect DOM |
| Color independence | Info not conveyed by color alone | Check error states, status badges |
| Motion | Respects prefers-reduced-motion | Check if animations honor the media query |

#### Layer 5: Responsive

At each breakpoint (375, 768, 1440):
- Does the layout reflow without horizontal scroll?
- Is text still readable (≥14px body)?
- Are touch targets still ≥44×44px on mobile?
- Do images resize or clip?
- Does the navigation adapt (sidebar → mobile nav)?
- Is any content hidden that shouldn't be?

### Severity

| Level | Meaning | Examples |
|-------|---------|---------|
| **P0** | Blocks a core task | Broken CTA, invisible text, form can't submit, page doesn't load |
| **P1** | Significant UX harm | Buttons mistaken for cards, contrast below WCAG AA, confusing hierarchy, broken on mobile |
| **P2** | Quality issue for attentive users | Inconsistent spacing, off-palette color, heading size too similar to body, slow animation |
| **P3** | Polish opportunity | Faint logo, suboptimal easing, minor alignment drift, shadow too subtle |

### Report format

Write to `~/.clearshot/reports/{date}-{slug}.md`:

```markdown
# {Page} — Clearshot Audit
**URL:** {url}
**Date:** {YYYY-MM-DD}
**Viewport:** {width}×{height}
**taste.md:** {present / absent — if absent, note it was skipped}

## Spatial Map
{5×5 grid analysis. Element inventory grouped by section.}

## Computed Values
{Key values extracted via browser console. Compared to taste.md.}

## Taste Deviations
{Each deviation: expected (per taste.md) vs actual (measured). Severity. Fix.}

## Cognitive Load
| Dimension | Grade | Notes |
|-----------|-------|-------|
| Clarity | _/F | {one-line finding} |
| Action | _/F | {one-line finding} |
| Delight | _/F | {one-line finding} |

## Accessibility
{Findings with WCAG standard, measured ratio, and fix.}

## Responsive
{Findings per breakpoint.}

## Issues
{P0–P3 prioritized list. Each: element → problem → fix (specific CSS/HTML).}

## Verdict
{What works. What doesn't. What's missing.}
{Factual score: _/10. Taste score: _/10.}
```

---

## Core rules

1. **Hex over color names.** Say `#3B82F6`, not "blue." Say `~16px`, not "some padding."
2. **Group by section, not element type.** Users see pages, not component lists.
3. **Every issue gets a fix.** No observation without a recommendation. Specify the CSS property, the old value, and the new value.
4. **See what users see.** Use the browser. Computed styles > source code. Rendered layout > template markup.
5. **Taste is specific.** "Feels off" is unacceptable. "The 20px h2 reads as the same hierarchy level as the 18px h3 — increase to 24px for clear separation" is required.
6. **Be honest about AI slop.** If the page looks like it was generated by a default LLM prompt, say so. Identify the specific tells.
7. **The component taxonomy is law.** If a button looks like a card, that's a P1. If a non-interactive element looks clickable, that's a P1. Visual category confusion is a serious cognitive failure.
