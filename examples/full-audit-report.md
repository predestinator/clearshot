# MAYA Creators Program — Full UI Audit
**URL:** https://creators.entermaya.com
**Date:** 2026-03-25
**Viewport:** ~980×660 (browser tool viewport)

---

## Level 1: Spatial Map

### Dashboard `/dashboard`
- **A1-A5 (row 1)**: Topbar — sticky, bg-background/80 blur. "Program" left, "ENTERMAYA.COM" right. Thin border-bottom (~1px #C8C3BE/60). Feels like a native app bar. ✓
- **B1-B5 (row 2)**: Hero card — full-width within max-w-1100, card-elevated with gradient bg (#FFF8F6→#FFF→#F8F7F5). Left half: red accent bar + "MAYA NARRATIVE UNIVERSE" label + h1 heading + body + CTAs. Right half: book mockup image.
- **C1-C5 (row 3)**: "How it works" — 3-column card grid. Each card-soft with red numbered circle, heading, body text.
- **D1-D5 (row 4)**: "Choose your format" — 2-column card-interactive. Icon-left, text-right layout. "Review Essay" and "Review Video."
- **E1-E3 (row 5, left)**: Prize section — Grand Prize card with image, badge, title. card-elevated with red top gradient bar.
- **E3-E5 (row 5, right)**: Secondary prizes — stacked card-soft items (Divyas, Physical Copy, Published).
- **F1-F5 (row 6)**: Rewards callout — full-width card-elevated with pink gradient bg, blur orbs, CTA.
- **G1-G5 (row 7)**: Quick nav — 4-column card grid (Resources, Rules, Leaderboard, Sign in).
- **H1-H5 (row 8)**: Footer — centered MAYA wordmark (very faint), text links.

### Winners `/winners`
- Header: eyebrow text + "LEADERBOARD" display heading + red bar + subtitle
- Board: Solari split-flap board — white bg, gray header row, 5 ghost rows with scrambling flap cells, footer with "LIVE" pip

### Resources `/resources`
- Header: eyebrow + "Resources" heading + subtitle
- Book card: card-elevated with book cover image, title, author, download CTA
- Below fold: theme cards, prompt cards, video tips

### Rules `/rules`
- Header: "Rules" heading + subtitle
- Basics: 2×2 grid of info cards with red check icons
- Categories: accordion panels
- Judging: info box
- Prizes: stacked prize cards
- CTAs: bottom action links

### Login `/login`
- Split layout: hero image left (dark overlay), form panel right
- Form: Google sign-in, email/password fields, CTA buttons

---

## Level 2: Design System

### Colors (measured)
| Token | Hex | Usage | Verdict |
|-------|-----|-------|---------|
| background | #EFEDEB | Page bg | ✓ Good — warm, cards contrast |
| surface | #FFFFFF | Cards | ✓ Visible lift from bg |
| surface-container-low | #F7F6F4 | Sidebar bg | ⚠️ Too close to cards on sidebar |
| primary | #DE0137 | CTAs, accents | ✓ Strong, consistent |
| text-primary | #1A1816 | Headings | ✓ Dark, readable |
| text-body | #3D3A37 | Body text | ✓ Good contrast |
| text-secondary | #5C5752 | Secondary | ✓ Readable |
| text-tertiary | #8A8683 | Meta/footer | ⚠️ Borderline on #EFEDEB bg |
| outline-variant | #C8C3BE | Borders | ✓ Visible |

### Typography
| Role | Size | Weight | Font | Verdict |
|------|------|--------|------|---------|
| Display (h1) | clamp(2rem-3.25rem) | 900 (black) | Space Grotesk | ✓ Strong |
| Section heading (h2) | 1.25rem (20px) | 600 | Space Grotesk | ⚠️ Could be bigger |
| Card heading (h3) | 0.875rem (14px) | 600 | Space Grotesk | ✓ Compact but clear |
| Body | 15px | 400 | Inter | ✓ |
| Secondary | 13px | 400 | Inter | ✓ |
| Caption | 10-11px | 500-700 | Space Grotesk / Inter | ✓ |

### Spacing
- Section gaps: 56-64px (mb-14 md:mb-16) — **spacious, good breathing room**
- Card padding: 24px (p-6) — **comfortable**
- Card gaps: 16-20px (gap-4 to gap-5) — **consistent**
- Border radius: 12px (0.75rem) — **consistent across all cards**

---

## Issues (Priority Order)

### P0 — Critical
1. **Login page: left hero panel not rendering at narrow viewport** — The split layout collapses to form-only. The hero image with dark gradient overlay doesn't show. This means first-time visitors see a plain white form with no brand context.

### P1 — High
2. **Dashboard hero gradient too subtle** — `#FFF8F6→#FFF→#F8F7F5` against `#EFEDEB` page bg barely registers. The hero card needs a visibly different background to anchor the page. Suggestion: use `#F8F1EE` (warmer, pinker) as start color.
3. **Leaderboard ghost state: "AWAITING" text nearly invisible** — `#C8C3BE` on `#F7F6F4` header bg is ~1.3:1 contrast. Needs `#8A8683` minimum.
4. **Ghost flap cells too faint** — `#DBD8D5` text on `#F0EEEC` flap bg is ~1.2:1. Needs `#A8A4A0` minimum.
5. **Section headings (h2) too small at 20px** — "How it works", "Choose your format", "What you can win" feel like card headings, not section headers. Should be 24px minimum.
6. **Sidebar bg (#F7F6F4) too close to card white (#FFFFFF)** — At a glance, sidebar and cards merge. Sidebar needs `#F0EEEC` or a subtle left-side shadow.

### P2 — Medium
7. **Text-tertiary (#8A8683) fails WCAG AA on #EFEDEB** — 3.1:1 contrast (needs 4.5:1 for small text). Footer and meta text are technically below accessibility threshold.
8. **"MAYA NARRATIVE UNIVERSE" eyebrow at 10px is too small** — Gets lost in the hero. Should be 11-12px.
9. **Accent bar (2px × 32px) is nearly invisible** — The red separator bars before section headings are too thin. Should be 3px height minimum.
10. **Quick nav card labels use font-semibold but say "Resources" in 12px** — Below comfortable tap-target for text recognition on mobile.

### P3 — Polish
11. **Book mockup drop shadow blends with hero gradient** — The `drop-shadow-xl` is warm-toned against a warm bg. Consider a cooler shadow or vignette.
12. **Cookie banner persists over all content** — Blocks ~60px of bottom. Standard but annoying.
13. **Footer MAYA wordmark extremely faint** — opacity-40 on the light bg makes it nearly invisible. Bump to opacity-60.
14. **Prizes "1 winner" / "5 winners" meta text uses text-tertiary** — Hard to read. Use text-secondary.

---

## Taste

**What works:** The overall layout is clean and well-structured. Section spacing is generous and gives each block room to breathe. The red accent color (#DE0137) is used sparingly and effectively — CTAs, badges, icons, accent bars all feel intentional. Card system (soft/interactive/elevated) creates clear hierarchy. The Solari board concept for the leaderboard is distinctive and memorable.

**What doesn't:** The page feels monochromatic. Everything is warm gray + white + red. There's no secondary accent, no illustrative element beyond the book cover, no texture or visual rhythm to break the flatness. The hero — the first thing a visitor sees — reads as "slightly warm white box on warm white page." It should be the strongest visual on the page and instead it's the most neutral.

**What's missing:** Visual anchors. The page needs at least one section with a contrasting background (not just a barely-perceptible gradient). A dark section, a colored section, anything to break the warm-gray monotony. The Solari board used to be that anchor (dark on light) — now that it's white too, there's no visual relief on any page.
