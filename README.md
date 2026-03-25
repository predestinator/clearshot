# Clearshot

Visual intelligence for AI interfaces. Two modes: **Define** (generate `taste.md` — your project's visual identity and standards) and **Verify** (screenshot live UI and audit against it). Uses browser tools to see what users see — not source code, the actual rendered page.

## Install

Copy `SKILL.md` into your project or user skills directory:

```bash
# Project-level (shared with team)
mkdir -p .cursor/skills/clearshot
cp SKILL.md .cursor/skills/clearshot/SKILL.md

# User-level (personal, all projects)
mkdir -p ~/.cursor/skills-cursor/clearshot
cp SKILL.md ~/.cursor/skills-cursor/clearshot/SKILL.md
```

Your AI agent picks it up automatically. Trigger with:
- "generate taste" — creates `taste.md` for your project
- "audit this UI" / "taste your UI" — screenshots and audits the live page
- "full clearshot" — generates taste.md then audits against it

## What it does that others don't

Every other UI skill reads your code. Clearshot opens the browser.

| | Clearshot | Code-based skills |
|---|---|---|
| **Sees** | Rendered pixels, computed styles | Source CSS, HTML templates |
| **Measures** | Actual contrast ratios, real font sizes | Token values that may not apply |
| **Catches** | Font rendering issues, image loading failures, layout overlap, animation timing | Token inconsistencies, missing dark mode vars |
| **Generates** | `taste.md` — project-specific visual identity | Generic design rules |
| **Checks** | Live UI against `taste.md` standards | Code against linting rules |

## How it works

### 1. Define mode — taste.md

Analyzes your codebase (design tokens, components, copy tone) to generate `taste.md`: a living specification of your project's visual identity. Covers palette, typography, spacing, shape, depth, component taxonomy (static containers vs interactive surfaces vs action buttons), project-specific anti-patterns, and universal AI slop indicators.

Can ask you questions first or go fully autonomous.

### 2. Verify mode — audit

Navigates to your live URL, takes screenshots at multiple scroll positions and breakpoints (375, 768, 1440), extracts computed styles via browser console, then runs five analysis layers:

1. **Spatial Grid** — 5x5 cell-by-cell element inventory with hex colors, pixel sizes, states
2. **Taste Check** — every observation compared against `taste.md`
3. **Cognitive Load** — Clarity / Action / Delight grading (A through F)
4. **Accessibility** — WCAG AA contrast, touch targets, focus indicators, heading hierarchy
5. **Responsive** — layout reflow, text readability, target sizes at each breakpoint

Issues are prioritized P0 (blocker) through P3 (polish), each with the specific CSS/HTML fix.

## The taste.md spec

The generated `taste.md` includes:

- **Identity** — one sentence: what this is and who it's for
- **Principles** — 3-5 design decisions (not platitudes)
- **Palette** — every color role with hex values
- **Typography** — full scale with family, size, weight, case, tracking
- **Spacing** — base unit and derived values
- **Shape** — radius values per element type
- **Depth** — shadow hierarchy (flat → raised → elevated → button)
- **Component taxonomy** — visual rules for static containers, interactive surfaces, primary buttons, secondary buttons, form inputs, text links
- **Anti-patterns** — project-specific things to never do
- **AI slop indicators** — universal generated-UI tells to flag

## License

MIT
