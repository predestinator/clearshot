---
name: clearshot
description: "Structured screenshot intelligence for Cursor. Analyzes UI screenshots with a 5×5 spatial grid, full element inventory, and design system extraction — facts and taste together, every time. Escalates to full blueprint when building. Trigger on any UI screenshot or commands like 'analyze this screenshot,' 'audit this UI,' 'rebuild this,' 'match this design,' 'taste your UI.' Skip for non-UI images. Adapted from github.com/udayanwalvekar/clearshot for Cursor's browser MCP tools."
---

# Clearshot — Structured Screenshot Intelligence for Cursor

## How to use

Use the `cursor-ide-browser` MCP tools to capture and analyze UI:

1. **Navigate**: `browser_navigate` to the target URL with `take_screenshot_afterwards: true`
2. **Lock**: `browser_lock` to prevent interference during analysis
3. **Capture**: `browser_take_screenshot` (viewport or `fullPage: true` for entire page)
4. **Scroll + capture**: `browser_scroll` down, then `browser_take_screenshot` again for below-fold content
5. **Resize + capture**: `browser_resize` to test responsive breakpoints (mobile: 375×812, tablet: 768×1024, desktop: 1440×900)
6. **Analyze**: Apply the analysis framework below to every screenshot
7. **Report**: Write findings to `~/.clearshot/reports/{date}-{page-slug}.md`
8. **Unlock**: `browser_unlock` when done

## Gate check

Not every image needs this skill.

1. Is this a digital interface? (websites, apps, dashboards, mockups, wireframes, Figma exports count. Photos, memes, charts do not.)
2. Is the conversation about building, debugging, designing, or evaluating UI?

**Three outcomes:**
- Neither true: exit skill, respond normally.
- Image is not UI but conversation IS about building UI: describe mood/texture/weight as inspiration. No structured analysis.
- Image IS a UI and conversation is about building/evaluating: proceed with analysis levels.

## Analysis levels

Every analysis combines facts AND taste. Every observation is grounded in specifics (hex values, pixel measurements) AND includes how it feels (hierarchy, weight, cohesion).

### Level 1: Map (always runs)

Divide the screenshot into a **5×5 grid**. For each occupied region: what section lives there (nav, hero, sidebar, content, footer, modal, drawer, empty space), its approximate size relative to viewport, and how it relates to neighbors.

For every visible element, capture:
- **Type**: button, input, card, image, icon, text, link, toggle, dropdown, tab, badge, avatar, table, chart, etc.
- **Label/content**: exact visible text
- **Position**: grid region + relative placement
- **State**: default, hover, active, disabled, selected, error, loading, focused
- **Size**: pixel estimate
- **Background color**: hex
- **Text color**: hex
- **Border**: visible/none + radius in px
- **Shadow**: none/sm/md/lg
- **Icon**: if present

Group by section. Also note: where the eye goes first, whether the layout breathes or feels cramped, whether hierarchy is clear or competing, what feels intentional vs accidental.

### Level 2: System (always runs)

Extract the design system behind what's visible:

**Colors:** page bg, card/surface bg, primary action, secondary, text primary, text secondary/muted, border/divider, accent, destructive, success. All hex values. Note whether the palette feels cohesive or patchwork.

**Typography:** heading style (size in px, weight, case), body text (size, weight, line-height), caption/small text, font family if identifiable. Note whether the type scale feels intentional.

**Spacing and shape:** spacing pattern (tight 4-8px / comfortable 12-16px / spacious 24-32px+), border radius pattern (sharp 0-2px / subtle 4-6px / rounded 8-12px / pill), overall density (compact / comfortable / spacious). Note consistency.

### Level 3: Blueprint (escalates when building)

Runs when the user needs to implement, rebuild, or clone the UI.

**Layout architecture:** page layout pattern, content layout per section, container width, responsive context, scroll clues, z-index layers.

**Interaction map:** primary CTA, secondary actions, navigation pattern, form elements, data display patterns, visible states. Note where a user would hesitate or feel friction.

## Output format

**Critique/audit:** Lead with what's wrong. Ground each observation in specifics (the exact hex, spacing, or element) and how it affects the experience. Don't catalog everything — focus on what matters.

**Comparison (before/after):** What changed, what improved, what regressed, what still needs work.

**Full audit report:** Write to `~/.clearshot/reports/{date}-{slug}.md`:

```markdown
# {Page name} — Clearshot Audit
**URL:** {url}
**Date:** {YYYY-MM-DD}
**Viewport:** {width}×{height}

## Level 1: Map
{5×5 grid analysis, element inventory grouped by section}

## Level 2: System
{Color palette, typography scale, spacing patterns}

## Issues
{Prioritized list: severity, element, problem, fix}

## Taste
{Overall feel, what works, what doesn't, what's missing}
```

## Core principles

- **Be specific.** "A dashboard with some cards" is never acceptable. "3-column grid, ~280px cards, #FFFFFF bg, 12px radius, border rgba(0,0,0,0.06) + shadow 0 2px 8px — cards feel solid but competing with each other" is.
- **Hex over color names, pixels over vague sizes.** Say #3B82F6 not "blue." Say ~16px not "some."
- **Group by section, not by element type.**
- **Call out the non-obvious.** Custom illustrations, unusual patterns, implied animations, dynamic vs static data.
- **Match the user's pace.** Rapid iteration = concise output. Detailed audit = exhaustive.

## Self-rating (internal, silent)

After analysis, rate 0-10: spatial accuracy, specificity, taste, actionability. Never show the rating to the user.
