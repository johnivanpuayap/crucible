# Crucible

> Where raw ideas survive the heat.

Crucible is a Claude Code skill that transforms raw ideas into fully designed projects — brand identity, visual design system, logo system, and tech stack recommendations.

You describe an idea in the terminal. Crucible asks one question at a time, and every choice you make opens as a page in your browser, so you decide by seeing, not by reading a list. At the end you have a complete design package in `docs/crucible/`.

## What It Does

Crucible walks you through (or generates in one shot) a complete project design:

1. **Concept Exploration** — What's the idea, who's it for, what problem does it solve
2. **Brand Identity** — Name, tagline, tone of voice, personality
3. **Visual Identity** — Color palette, typography, UI style
4. **Logo System** — SVG logo, app icon, wordmark, favicon, with usage guidelines
5. **Tech Stack** — Best-fit recommendation with rationale
6. **Output** — Markdown docs, decision pages, logos, and a visual brand preview

## A Full Run, In Pictures

The pictures below follow one project through every phase: **Sunod**, a badminton open-play queue app for organizers. Everything shown here is what Crucible writes to `docs/crucible/` during an interactive run.

### Start

Invoke `/crucible` with your idea. Crucible explains the phases and starts asking questions.

![Starting Crucible in the terminal](docs/images/terminal-start.png)

### Phase 1 — Concept Exploration

Crucible hands the idea to the `brainstorming` skill. Each clarifying question with options opens as a decision page with trade-offs side by side, and the recommended option is marked. The answers become the design spec in `specs/`.

![Phase 1 decision page: form factor](docs/images/phase1-form-factor.png)

### Phase 2 — Brand Identity

**2a. Name.** Candidates are shown where they will live: the home screen icon, the app header, and the splash screen.

![Phase 2a decision page: names](docs/images/phase2a-names.png)

**2b. Tagline.** Each tagline is placed on the splash screen and as the app-store subtitle.

![Phase 2b decision page: taglines](docs/images/phase2b-taglines.png)

**2c/2d. Tone of voice and personality.** The same screen three times, with only the copy changing. The chosen option sets the voice for every label and error message, and is written to `brand.md` together with the personality attributes.

![Phase 2c decision page: tone of voice](docs/images/phase2c-tone.png)

### Phase 3 — Visual Identity

**3a. Color palette.** Three color directions applied to a mock of the product's main screen, with a light/dark toggle on the page. If `ui-ux-pro-max` is installed, its suggestion is one of the options.

![Phase 3a decision page: color directions](docs/images/phase3a-color-directions.png)

The same page in dark mode:

![Phase 3a decision page in dark mode](docs/images/phase3a-color-directions-dark.png)

**3b. Typography.** Font pairings from Google Fonts rendered on the real screen, in the chosen palette.

![Phase 3b decision page: typography](docs/images/phase3b-typography.png)

**3c. UI style.** Surfaces, radius, shadows, and motion, compared on the same screen. Palette, fonts, and style land in `design.md`.

![Phase 3c decision page: UI style](docs/images/phase3c-ui-style.png)

### Phase 4 — Logo System

**4a. Logo type and style.** Wordmark, lettermark, pictorial mark, and the rest, each previewed with the brand's own name and colors, followed by the visual style.

![Phase 4a decision page: logo type](docs/images/phase4a-logo-type.png)

![Phase 4a decision page: logo style](docs/images/phase4a-logo-style.png)

**4b. Concepts.** Three logo concepts as real SVG, each with its design rationale, shown in light and dark, in monochrome, in the app header, and as an icon from 160px down to a 16px browser tab.

![Phase 4b decision page: logo concepts](docs/images/phase4b-logo-concepts.png)

**4c. Full logo system.** From the chosen concept, Crucible generates the primary logo, wordmark, app icon, and favicon, each in full color, monochrome dark, and monochrome light, plus `USAGE.md`. The review page shows the actual files from `logos/`.

![Phase 4c page: generated logo system](docs/images/phase4c-logo-system.png)

### Phase 5 — Tech Stack

Realistic stack options scored against what the project actually needs, with an architecture diagram for the recommendation. The choice and its rationale go to `tech-stack.md`.

![Phase 5 decision page: tech stack](docs/images/phase5-tech-stack.png)

### Phase 6 — Output

Crucible writes every artifact to `docs/crucible/`, commits them, and offers a visual preview.

![Finishing Crucible in the terminal](docs/images/terminal-finish.png)

The preview is a single `preview.html` that pulls the whole brand together: logo system, light and dark palettes, typography, sample screens, UI components, voice, and tech stack.

![Brand preview page](docs/images/phase6-preview-top.png)

[See the full preview page](docs/images/phase6-preview.png).

### Phase 7 — Push to Tracker (optional)

If `~/.crucible/config.json` exists, the generated files are uploaded to your tracker. If it doesn't, nothing happens and the run is complete.

## Output

```
docs/crucible/
├── specs/YYYY-MM-DD-<topic>-design.md   # Full design spec
├── plans/YYYY-MM-DD-<plan-name>.md      # Implementation plan
├── brand.md                              # Name, tagline, tone, personality, logo notes
├── design.md                             # Palette (light + dark), typography, UI style
├── tech-stack.md                         # Recommended stack + rationale
├── decisions/                            # HTML decision pages, one per choice point
│   └── NN-<phase>-<topic>.html           #   chosen option marked on each page
├── logos/                                # SVG logo system + USAGE.md
└── preview.html                          # Visual brand preview
```

## Modes

- **Interactive (default)** — Guided conversation, one question at a time, every decision shown in the browser
- **One-shot** — Describe everything upfront, get the full package (decision pages are skipped; `preview.html` covers the visual review)

## Dependencies

Crucible builds on top of these skills:

- [`superpowers:brainstorming`](https://github.com/anthropics/claude-code) — Concept exploration and spec generation
- [`ui-ux-pro-max`](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill) — Visual identity intelligence

## Optional Integration

Crucible can push generated files to a tracker app (like [Canopy](https://github.com/jpuayap/canopy)) via API. Configure with `~/.crucible/config.json` — fully optional, works standalone without it.

## License

MIT
