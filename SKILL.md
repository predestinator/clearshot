---
name: clearshot
description: "Visual intelligence for AI interfaces. Two modes: Define (generate taste.md — your project's visual identity and standards) and Verify (screenshot live UI and audit against taste.md). Uses browser tools to see what users see — not source code, the actual rendered page. Trigger on: 'audit UI', 'check taste', 'generate taste', 'review design', 'screenshot analysis', 'taste your UI'. Skip for non-UI images."
---

# Clearshot — Visual Intelligence for AI Interfaces

You see what users see. You navigate to the live page, screenshot it, measure computed values, and judge the result. You do not read CSS files and guess — you open the browser and look.

Two modes:
1. **Define** — Generate `taste.md`: design identity, standards, component taxonomy, anti-patterns
2. **Verify** — Screenshot live UI, audit against `taste.md`, report with fixes

---

## Design Foundations

These are non-negotiable principles of visual design. Use them when generating taste.md (to produce high-quality defaults) and when auditing (as an independent layer beyond taste.md conformance). A UI that matches its taste.md but violates these foundations is still a bad UI.

### Hierarchy — the eye must know where to go

Every screen has a reading order. Users scan in ~400ms before deciding to engage. Hierarchy is created by:

- **Size contrast**: The largest element is read first. If your h1 is 44px and your h2 is 24px, that's a 1.83× ratio — clear. If your h1 is 24px and your h2 is 20px, that's 1.2× — they compete. **Minimum heading step ratio: 1.25×**. Display→h1 should be ≥1.5×.
- **Weight contrast**: Bold next to regular creates hierarchy. But if everything is bold, nothing is. **Maximum two weights per visible section**: one for emphasis, one for body.
- **Color contrast**: Not just WCAG — aesthetic contrast. Primary text should be ≥10:1 on the background. Secondary text ≥6:1. Muted text ≥4.5:1. If secondary and muted are visually identical, hierarchy collapses.
- **Spatial hierarchy**: More whitespace around an element = more importance. A heading with 48px above and 12px below reads as a section start. A heading crammed between content reads as a label.

**Test**: Squint at the page. Can you still see the hierarchy? If squinting makes everything look like one flat gray block, hierarchy has failed.

### Spacing — rhythm, not randomness

Good spacing follows a **consistent scale**. Pick a base unit (4px or 8px) and derive everything from multiples:

```
4  8  12  16  20  24  32  40  48  56  64  80  96
```

- **Section gaps**: 48–96px. This is what separates major content blocks. Too small and sections merge. Too large and the page feels empty.
- **Element gaps within a section**: 12–24px. Cards in a grid, items in a list, form fields.
- **Inner padding**: 16–32px. Inside cards, buttons, containers.
- **Dense gaps**: 4–8px. Icon-to-label, badge-to-text, tight clusters.

**The rule**: If you can't name which multiple of your base unit a gap is, the spacing is arbitrary. Arbitrary spacing is the #1 tell of AI-generated UI.

### Color — relationships, not just hex values

A palette is a set of **relationships**, not isolated swatches.

- **60-30-10 rule**: 60% dominant (background/surface), 30% secondary (text, borders, supporting elements), 10% accent (primary action, highlights). If your accent color covers 30% of the viewport, it's no longer an accent.
- **Saturation hierarchy**: Background = lowest saturation (near-neutral). Text = medium saturation (warm or cool gray). Accent = highest saturation (the only vivid color). If your background, cards, and buttons all have similar saturation, the page feels flat or noisy.
- **Temperature consistency**: Warm grays (#EFEDEB, #C8C3BE) and cool grays (#E5E7EB, #9CA3AF) should not mix. Pick one temperature and own it.
- **Text color stepping**: You need exactly 4 text levels: primary (headings), body (paragraphs), secondary (supporting), muted (meta/captions). Each must be visually distinct. If any two levels look the same at arm's length, merge them or increase the gap.

**Test**: Convert the screenshot to grayscale. Is the hierarchy still visible? If the page becomes an undifferentiated gray, color is doing all the work and the structure is fragile.

### Typography — a scale, not a collection

Type should follow a **modular scale** with a consistent ratio. Common ratios:

| Ratio | Name | Feeling |
|-------|------|---------|
| 1.125 | Major second | Tight, dense, editorial |
| 1.200 | Minor third | Compact, professional |
| 1.250 | Major third | Balanced, versatile |
| 1.333 | Perfect fourth | Spacious, clear |
| 1.500 | Perfect fifth | Dramatic, expressive |

Pick one ratio. Derive every size from it:

```
Base: 16px
× 1.25 = 20px (h4/subhead)
× 1.25 = 25px (h3)
× 1.25 = 31px (h2)
× 1.25 = 39px (h1)
× 1.25 = 49px (display)
```

- **Line height**: Body text = 1.5–1.7 of font size. Headings = 1.1–1.3 (tighter). Display = 1.0–1.15 (tightest).
- **Font pairing**: Maximum 2 families. One for headings (personality), one for body (readability). They should share a similar x-height ratio. Never pair two display fonts.
- **Weight range**: Use 2–3 weights maximum across the entire page. Regular (400) for body, Semibold (600) for subheads, Bold (700) for headings. If you're using 300, 400, 500, 600, 700, and 800, the weight system has no meaning.

**Test**: Remove all color from the page (make everything black text on white). Is the hierarchy still obvious from size and weight alone? If not, the type scale is broken.

### Composition — how the page breathes

- **Negative space is structure.** Whitespace is not "empty" — it creates grouping, separation, and focus. A page with no breathing room feels suffocating. A page with too much feels unfinished. The amount of whitespace should be **proportional to the importance of what it surrounds**. More space around a hero = more emphasis.
- **Alignment lines**: Every page should have a clear left edge that most content aligns to. Mixed alignments (center here, left there, right somewhere else) create visual chaos. Pick one alignment strategy per section.
- **Visual weight distribution**: Heavy elements (images, dark sections, filled buttons) should be balanced across the page. If all the visual weight is in the top half, the bottom feels abandoned. If it's all on the left, the page tilts.
- **Content density**: The right density depends on the product. A dashboard can be dense. A landing page should breathe. A form should be spacious. **Match density to cognitive load** — complex tasks need more space between elements.

### Depth — the Z-axis has meaning

Shadows and elevation are **semantic, not decorative**. Each depth level should communicate something:

- **Level 0 (flat)**: Content at rest. Informational. Non-interactive. No shadow, no elevation.
- **Level 1 (raised)**: Interactive surfaces. Clickable cards, tabs. Subtle shadow (`0 1px 3px`).
- **Level 2 (elevated)**: Important containers that float above the page. Hero cards, sticky headers. Medium shadow (`0 4px 16px`).
- **Level 3 (overlay)**: Modals, dropdowns, popovers. These block content below. Strong shadow (`0 8px 32px`).
- **Action elements**: Buttons get their own shadow vocabulary — often colored shadows that hint at the button color.

**The rule**: Maximum 3 shadow levels visible on any single viewport. If everything has a shadow, nothing has depth. If nothing has a shadow, the page is flat and lifeless. Pick the right number for the product's personality.

### Polish — what separates "works" from "beautiful"

These details compound. Individually subtle, collectively they make a UI feel crafted:

- **Easing curves**: Never use `linear` for UI transitions. `ease-out` for entrances, `ease-in` for exits, `ease-in-out` for state changes. Duration: 150ms for micro-interactions (hover, press), 250–350ms for layout changes, 400–600ms for page transitions.
- **Border radius consistency**: Pick 2–3 radius values and use them everywhere. Common: 0 (sharp), 8–12px (cards/inputs), 9999px (pills/avatars). Mixing 4px, 6px, 8px, 10px, 12px, 16px is noise.
- **Icon consistency**: One icon family, one weight, one optical size. Mixing outlined and filled icons on the same page is a cognitive fracture. If filled, all filled. If outlined, all outlined. Exception: active/inactive tab states.
- **Micro-interactions**: Buttons should respond to press (scale 0.97, darken). Hover states should be immediate (<100ms delay). Loading states should never leave the user wondering if something happened.
- **Text rendering**: Use `-webkit-font-smoothing: antialiased` on dark-on-light. Never on light-on-dark (it makes text too thin). Use `text-rendering: optimizeLegibility` for headings.

---

## Entry point

When triggered, check if `taste.md` exists in the project root.

- **No taste.md**: Run Define mode. Ask the user for input or go autonomous (see below).
- **taste.md exists**: Run Verify mode. Screenshot and audit against it.
- **User says "full"**: Run Define then immediately Verify.

---

## Mode 1: Define — Generate taste.md

taste.md is not a token inventory. It is a **design projection** — a holistic understanding of what this product should look and feel like, derived from everything available.

### Sources of truth (use ALL of them, but filter through Design Foundations above)

1. **User intent** — What the user has said across the entire conversation. Their goals, frustrations, emotional language, aesthetic preferences, references they've shared. "Make it feel native" is a design decision. "I want clarity" is a constraint. "It's too light" is a measurement. **But**: if the user's conversation reveals iterative band-aid fixes, don't encode those — project forward to what the UI *should* be.
2. **Product context** — What the product does, who it serves, what outcome users seek. A contest platform for creative writers has a different taste than a billing dashboard. Read the copy, the page structure, the feature set.
3. **Design Foundations** — Apply the principles above. If the user's existing palette has no saturation hierarchy, fix it. If the type scale has no consistent ratio, derive one. If spacing is arbitrary, systematize it. Don't just document what exists — project what *should* exist, grounded in the foundations.
4. **Existing visual decisions** — CSS/Tailwind config, font imports, color palette, spacing patterns, component structures. These are decisions already made — respect the *intent* but challenge execution that violates foundations.
5. **Audience expectations** — What do the users of THIS product expect? What are they used to? What would feel wrong to them? A teen social app and an enterprise SaaS have different cognitive baselines.
6. **What hasn't been said** — Infer from the product's positioning. If the copy is warm and personal, the UI shouldn't be cold and corporate. If the product is about creativity, the layout shouldn't be rigid.

### Two approaches

**Ask mode** — when nuance matters, prompt the user:
1. Who uses this and what do they expect?
2. What feeling should this evoke? (not "modern" — that's nothing. "Warm but authoritative" is something.)
3. Reference sites or screenshots?
4. What currently bothers you about the UI?

**Autonomous mode** — when speed matters or user says "go yolo":
1. Read every source above silently
2. Apply Design Foundations to evaluate existing decisions — where they're strong, keep them. Where they're weak, improve them.
3. Generate taste.md with strong opinionated defaults that are grounded in the foundations, not just mirrors of existing code
4. Better to be specific and wrong than vague and useless — the user will correct what matters

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

Run every layer. Skip nothing. Layer 0 runs independently of taste.md — it catches aesthetic failures even if taste.md itself is weak.

#### Layer 0: Aesthetic Foundations

Before comparing against taste.md, evaluate the screenshot against the Design Foundations above. These are universal — they apply regardless of project taste.

| Check | What to measure | Fail condition |
|-------|----------------|----------------|
| Heading step ratio | Compute ratio between adjacent heading levels (h1/h2, h2/h3) | Any ratio < 1.25× |
| Text level distinction | Compare primary, body, secondary, muted text colors at arm's length | Any two levels visually indistinguishable |
| Spacing consistency | Identify the base unit. Check if all gaps are multiples of it | >2 gaps that don't fit the scale |
| Weight discipline | Count distinct font weights visible in the viewport | >3 weights visible simultaneously |
| Saturation hierarchy | Check bg saturation vs text saturation vs accent saturation | Bg and accent have similar saturation, or text is more vivid than accent |
| Shadow semantics | Count distinct shadow levels. Check if non-interactive elements have shadows | >3 shadow levels, or flat content has shadows |
| Radius consistency | List all border-radius values in use | >3 distinct radius values (excluding 0 and 9999px) |
| Alignment | Check left-edge alignment across sections | Content elements starting at >3 different X positions within a section |
| Negative space balance | Check vertical rhythm between sections | Adjacent sections with >2× difference in vertical gap |
| Grayscale test | Mentally desaturate. Is hierarchy visible? | Hierarchy relies entirely on color with no size/weight differentiation |

For each failure, provide: the measured value, the foundation principle it violates, and a specific fix. These are separate from taste.md deviations.

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

## Aesthetic Foundations
{Layer 0 results. Universal principles checked independently of taste.md.}
{Each failure: measured value → principle violated → specific fix.}

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
