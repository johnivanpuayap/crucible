# Crucible

> Where raw ideas survive the heat.

Crucible is a Claude Code skill that transforms raw ideas into fully designed projects — brand identity, visual design system, and tech stack recommendations.

## What It Does

Crucible walks you through (or generates in one shot) a complete project design:

1. **Concept Exploration** — What's the idea, who's it for, what problem does it solve
2. **Brand Identity** — Name suggestions, tagline, tone of voice, logo direction, personality
3. **Visual Identity** — Color palette, typography, UI style
4. **Tech Stack** — Best-fit recommendation with rationale

## Output

Crucible generates these files in your project:

```
docs/crucible/
├── specs/YYYY-MM-DD-<topic>-design.md   # Full design spec
├── plans/YYYY-MM-DD-<plan-name>.md      # Implementation plan
├── brand.md                              # Name, tagline, tone, personality
├── design.md                             # Palette, typography, style
└── tech-stack.md                         # Recommended stack + rationale
```

## Modes

- **Interactive (default)** — Guided conversation, one question at a time
- **One-shot** — Describe everything upfront, get the full package

## Dependencies

Crucible builds on top of these skills:

- [`superpowers:brainstorming`](https://github.com/anthropics/claude-code) — Concept exploration and spec generation
- [`ui-ux-pro-max`](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) — Visual identity intelligence

## Optional Integration

Crucible can push generated files to a tracker app (like [Canopy](https://github.com/jpuayap/canopy)) via API. Configure with `~/.crucible/config.json` — fully optional, works standalone without it.

## License

MIT
