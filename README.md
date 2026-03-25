# Clearshot

```bash
mkdir -p .cursor/skills/clearshot && curl -sL https://raw.githubusercontent.com/predestinator/clearshot/main/SKILL.md -o .cursor/skills/clearshot/SKILL.md
```

Run this in your project root. Your AI picks it up instantly. Say **"generate taste"** to create your design spec, **"audit this UI"** to screenshot and grade the live page, or **"full clearshot"** for both.

---

## What this is

Every other UI skill reads your source code. Clearshot opens the browser and looks at the rendered page — the same pixels your users see.

It runs in two modes:

**Define** — Generates `taste.md` in your project root. Not a token dump. It reads your codebase, your conversation history, your stated goals, and your audience to build a holistic design brief: visual identity, typography scale, spacing system, component taxonomy, and the specific anti-patterns that would violate YOUR project's taste. Can ask you questions first, or go fully autonomous.

**Verify** — Navigates to your live URL, screenshots at multiple scroll positions and responsive breakpoints, extracts computed styles via browser console, then runs five analysis layers against `taste.md`:

1. **Spatial Grid** — 5x5 element inventory with hex colors, pixel sizes, states
2. **Taste Check** — every observation vs your `taste.md` spec
3. **Cognitive Load** — Clarity / Action / Delight, graded A–F
4. **Accessibility** — WCAG AA contrast, touch targets, focus indicators
5. **Responsive** — layout, readability, and target sizes at 375, 768, 1440

Every issue gets a severity (P0–P3) and a specific CSS/HTML fix.

## What makes taste.md different

taste.md is not a list of design tokens. It's a **projection** — built from everything available:

- What the user has said across the conversation (goals, feelings, frustrations)
- The product's purpose and who it serves
- The emotional tone of existing copy and content
- The visual decisions already made in the codebase
- Competitive and cultural context
- What the user hasn't said but the product implies

The result is a living design brief that the AI checks against every time it touches UI. It captures intent, not just values.

## Links

- [SKILL.md](https://github.com/predestinator/clearshot/blob/main/SKILL.md) — the full skill file
- [Raw SKILL.md](https://raw.githubusercontent.com/predestinator/clearshot/main/SKILL.md) — direct download

## License

MIT
