---
name: crucible
description: "Transforms raw ideas into fully designed projects — brand identity, visual design system, and tech stack recommendations. Use when starting a new project from scratch or when you have a raw idea that needs to be fleshed out into a complete design."
---

# Crucible

Transform raw ideas into fully designed projects through collaborative dialogue.

Crucible takes you from "I have an idea" to a complete project design: brand identity, visual design system, and tech stack — all in one session.

<HARD-GATE>
Do NOT skip any phase. Every idea goes through all phases in order. The design can be lightweight for simple projects, but every phase must be addressed.
</HARD-GATE>

## When to Use

- Starting a new project from scratch
- You have a raw idea and want to turn it into a full design
- You want brand identity, visual design, and tech stack recommendations for a project
- You want to capture an idea with enough detail to build it later

## Modes

### Interactive (default)

Guided conversation. One question at a time, multiple choice when possible. Builds the full project design incrementally with validation at each phase.

Use interactive mode unless the user explicitly requests one-shot.

**How to be a great guide:**
- Start each phase with a brief explanation of what you're about to do and why it matters
- When presenting choices, lead with your recommendation and explain why
- If the user seems unsure, offer examples from real products they might know
- Summarize decisions at the end of each phase before moving to the next
- If the user changes their mind on a previous phase, go back and update — don't fight it
- Keep the energy up — this should feel exciting, not like filling out a form

### One-shot

User describes everything upfront. Crucible generates the full package in one pass. Activate when the user says something like "just generate it" or provides a detailed brief.

**One-shot mode differences:**
- Skip phase transitions (no recap/preview between phases)
- Phase 1: Write the design spec directly instead of invoking brainstorming interactively
- Phase 4: Generate a logo brief by default (not SVG generation)
- Skip TaskCreate tracking — just generate everything sequentially
- If `ui-ux-pro-max` is available, use its data but don't invoke it interactively

## Phase Transitions (Interactive Mode Only)

Between each phase, provide a brief recap and preview:

> "Great — [phase name] is locked in. Here's what we decided: [1-2 line summary]. Next up: [next phase name] — [what it involves and why it matters]. Ready?"

This keeps the user oriented and gives them a chance to revisit anything before moving forward.

## Re-running Crucible

If Crucible output already exists in `docs/crucible/`, ask the user: "I see existing Crucible files. Want me to start fresh (overwrite) or update specific parts?"

- **Start fresh:** Overwrite all files
- **Update:** Let the user pick which phases to re-run (e.g., "just redo the brand")

## Checklist

Follow this checklist in order, using TaskCreate to track each item:

1. **Concept exploration** — understand the idea, who it's for, what problem it solves
2. **Brand identity** — name, tagline, tone of voice, personality
3. **Visual identity** — color palette, typography, UI style
4. **Logo** — generate full logo system (4 variants x 3 color modes + usage guide) or write a brief
5. **Tech stack** — best-fit recommendation with rationale
6. **Generate output files** — write all artifacts to `docs/crucible/`
7. **Visual preview** — optionally generate and open an HTML brand preview in browser
8. **Push to tracker (if configured)** — upload files via API if `~/.crucible/config.json` exists

## Phase 1: Concept Exploration

**Interactive mode:** Invoke the `superpowers:brainstorming` skill to explore the idea. Follow its process fully — it handles concept questions, approach proposals, and design spec generation.

**One-shot mode:** Write the design spec directly based on the user's brief. Cover these essentials:
- Problem statement and target users
- Core features (prioritized)
- Constraints and scope boundaries
- Recommended approach with rationale

Once the design spec is written and approved (interactive) or generated (one-shot), continue to Phase 2.

**Output:** `docs/crucible/specs/YYYY-MM-DD-<topic>-design.md`

## Phase 2: Brand Identity

After the concept is solid, develop the brand. Ask the user one question at a time:

### 2a. Name

Generate 5-7 name candidates. For each, provide:
- The name
- A one-line tagline
- Why it works (one sentence)

Present them in a table. Ask the user to pick one or request another round.

**Naming guidelines:**
- 1-2 words, memorable, easy to type
- Should work as a folder name, CLI command, and app name
- Avoid generic startup clichés (dropping vowels, adding -ly/-ify)
- Check that the name doesn't clash with well-known existing products

### 2b. Tagline

Once the name is chosen, propose 3-5 taglines. Short, evocative, not a feature description.

### 2c. Tone of Voice

Ask the user to pick where the brand sits on these spectrums (or propose based on context):
- Formal ←→ Casual
- Playful ←→ Serious
- Technical ←→ Approachable
- Minimal ←→ Expressive

### 2d. Brand Personality

Summarize in 3-4 attributes (e.g., "Calm, organized, encouraging").

**Output:** `docs/crucible/brand.md`

## Phase 3: Visual Identity

Use the `ui-ux-pro-max` skill as a design intelligence reference. If the user has ui-ux-pro-max installed, invoke it via the Skill tool to get design system recommendations. Otherwise, generate recommendations manually using these guidelines:

- Match UI style to the product type
- Choose a color palette that reflects the brand personality from Phase 2
- Pick a typography pairing that matches the tone of voice
- Consider both light and dark mode from the start

Present the following to the user for approval:

### 3a. Color Palette

Present a full semantic color palette:
- Primary, On Primary
- Secondary
- Accent/CTA
- Background, Foreground
- Muted, Border
- Destructive
- Ring (focus)

Include hex values and usage descriptions. Consider both light and dark mode.

### 3b. Typography

Recommend a font pairing (heading + body) from Google Fonts. Provide:
- Font names and weights
- Mood/style keywords
- Google Fonts URL
- CSS import snippet
- Tailwind config snippet

### 3c. UI Style

Recommend a UI style (flat, glassmorphism, minimal, motion-driven, etc.) with:
- Keywords describing the style
- Key effects and transitions
- What to avoid
- Performance and accessibility notes

**Output:** `docs/crucible/design.md`

## Phase 4: Logo System

Now that the brand identity (Phase 2) and color palette/typography (Phase 3) are locked in, create the full logo system.

Ask the user: "Want me to generate a full logo system using your brand colors? I'll create SVG logos you can use right away — primary logo, app icon, favicon, and wordmark — or we can skip this and just write a logo brief for later."

**If the user wants logos generated:**

### 4a. Requirements

Ask about preferences (one question at a time):

- **Logo type:**
  - **Wordmark** — text-based logo (Google, Coca-Cola style)
  - **Lettermark** — initials/abbreviation (IBM, HBO style)
  - **Pictorial mark** — icon/symbol (Apple, Twitter style)
  - **Abstract mark** — abstract geometric form (Pepsi, Adidas style)
  - **Combination mark** — icon + text (Burger King, Lacoste style)
  - **Emblem** — text inside symbol (Starbucks, Harley-Davidson style)
- **Visual style:** Minimalist, geometric, organic/flowing, bold/strong, elegant/refined, playful/friendly, tech/modern, vintage/retro?
- **Any inspiration?** Existing logos they admire?

Use **color psychology** from the brand personality to guide design choices:
- Blue → trust, professionalism (finance, tech, healthcare)
- Green → growth, health (environment, wellness)
- Red → energy, passion (food, entertainment, retail)
- Purple → creativity, luxury (beauty, tech, creative)
- Orange → friendly, energetic (retail, food)
- Black/Gray → sophisticated, modern (luxury, fashion, tech)

### 4b. Design Concept Development

Generate **3 logo concepts** as actual SVG code, each exploring a different visual direction.

**Design thinking for each concept:**
- Research visual metaphors related to the brand name and meaning
- Explore negative space opportunities
- Ensure memorability and uniqueness — avoid generic shapes
- Balance simplicity with distinctiveness
- Consider cultural appropriateness
- Test that the concept works across all sizes (16px favicon to 512px hero)

For each concept, show the primary logo (the chosen type — combination mark, wordmark, etc.). Write them as temporary HTML files and open in the browser so the user can see them visually. If browser preview fails, describe each concept in text with the design rationale. Include a **design rationale** for each — explain the visual metaphor, why the shapes/composition were chosen, and how it connects to the brand.

Let the user:
- Pick one
- Request tweaks to a concept (adjust colors, proportions, details)
- Ask for a new round
- Skip and move on

### 4c. Full Logo System

**Once the user picks a concept**, generate the full logo system — a set of variants derived from that chosen concept:

| File | Purpose | What it contains |
|---|---|---|
| `logo.svg` | **Primary logo** — the main brand mark | Full logo in the chosen style (combination mark, wordmark, etc.) |
| `logo-icon.svg` | **App icon / symbol** — standalone icon for app stores, profile pictures, social media avatars | Icon/symbol only, no text. Square-friendly (1:1 aspect ratio). Must be recognizable at 64px and look good at 512px. |
| `logo-wordmark.svg` | **Wordmark** — text-only version for headers, footers, navigation | Brand name in the heading font with appropriate letter-spacing. No icon. |
| `favicon.svg` | **Favicon** — browser tab icon | Ultra-simplified version of the icon. Must be legible at 16px — strip fine details, use bold shapes, max 2 colors. Square viewBox (e.g., `0 0 32 32`). |

For each variant, also generate **color versions**:
- **Full color** — primary brand colors (the default)
- **Monochrome dark** — single dark color (`#1F2937`) for light backgrounds
- **Monochrome light** — single white (`#FFFFFF`) for dark backgrounds

Save color versions using the naming convention: `logo.svg` (full color), `logo-mono-dark.svg`, `logo-mono-light.svg`. Same pattern for `logo-icon` and `logo-wordmark` variants. Exception: `favicon.svg` does not need monochrome variants — at 16px, the simplification already reduces it to 1-2 colors.

### SVG Technical Standards

**Structure and semantics:**
```xml
<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 200 60"
     role="img" aria-labelledby="logo-title logo-desc">
  <title id="logo-title">Brand Name Logo</title>
  <desc id="logo-desc">A brief description of the logo's visual design</desc>
  <defs>
    <style>
      .primary { fill: #4F46E5; }
      .secondary { fill: #10B981; }
      .text { fill: #1F2937; }
    </style>
  </defs>
  <g id="icon"><!-- Icon elements --></g>
  <g id="wordmark"><!-- Text elements --></g>
</svg>
```

**Required practices:**
- Use `viewBox` for scalability — never fixed pixel dimensions only
- Define colors via CSS classes in `<defs><style>` — makes color variations trivial
- Use `<g>` groups with semantic IDs (`icon`, `wordmark`, `tagline`)
- Include accessibility: `role="img"`, `aria-labelledby`, `<title>`, `<desc>`
- Use `<defs>` for gradients, patterns, and reusable elements
- No raster images or external dependencies — each SVG must be self-contained
- Use the brand's color palette from Phase 3 (primary, secondary, accent)
- Use the brand's heading font from Phase 3 (or a clean sans-serif fallback)

**Optimization:**
- Remove unnecessary attributes and metadata
- Combine paths where possible
- Use `<symbol>` and `<use>` for repeated elements
- Minimize decimal precision (2 decimal places max)
- Remove invisible or off-canvas elements
- Keep it simple — geometric shapes, clean lines, no complex illustrations

**Variant-specific guidelines:**
- **logo.svg:** Should work at 32px and 512px. This is the hero — it sets the visual language for all other variants.
- **logo-icon.svg:** Square composition (1:1). Must stand alone without the brand name. Think app icon — no text, just the symbol. If the primary logo style is a wordmark or lettermark, derive a distinctive monogram or initial.
- **logo-wordmark.svg:** Text only. Adjust letter-spacing and weight for standalone use. Should feel intentional, not like the icon was just removed.
- **favicon.svg:** The most aggressive simplification. At 16px, detail is noise. Use the strongest single shape from the icon, fill it with the primary color, done.

### 4d. Usage Guidelines

After generating the logo system, write `docs/crucible/logos/USAGE.md` covering:

- **Clear space** — minimum padding around the logo equal to the height of the icon element
- **Minimum sizes** — digital: 100px width minimum; print: 1 inch minimum
- **Color usage** — when to use full color vs monochrome vs reversed
- **Incorrect usage** — do not stretch, rotate, add effects, change colors, or place on busy backgrounds
- **Web implementation** — inline SVG (recommended), `<img>` tag, and CSS background examples
- **Responsive sizing** — CSS snippet for responsive logo scaling
- **Exporting to PNG** — instructions using Inkscape (`inkscape logo.svg -o logo.png -w 1000`) or ImageMagick (`convert -background none logo.svg logo.png`)

Save all variants and usage guidelines to the `docs/crucible/logos/` directory.

**If the user wants to skip:**

Write a logo brief instead — a text description of 3 logo concepts that a designer or AI image tool could execute later. Each concept includes:
- Visual description (shape, composition, style)
- Design rationale — the visual metaphor and how it connects to the brand
- Suggested colors from the Phase 3 palette with color psychology reasoning
- Notes on how the concept would adapt to app icon, favicon, and wordmark variants

Save the brief in `brand.md` under the "## Logo" section.

**In one-shot mode:** Generate a logo brief by default unless the user explicitly requested SVG logos.

**Output:** `docs/crucible/logos/` directory (if generated) or logo brief in `brand.md`

## Phase 5: Tech Stack

Recommend the best-fit tech stack based on the project's needs. Always recommend what fits best, regardless of the user's existing experience.

Cover:
- **Frontend:** Framework, CSS approach, component library
- **Backend:** Server framework or BaaS, database
- **Hosting:** Where to deploy
- **Key libraries:** Auth, state management, etc.

For each choice, include:
- What it is
- Why it's the best fit for this specific project
- Alternatives considered and why they were passed over

**Output:** `docs/crucible/tech-stack.md`

## Phase 6: Generate Output Files

Write all artifacts to the project's `docs/crucible/` directory:

```
docs/crucible/
├── specs/YYYY-MM-DD-<topic>-design.md   # Full design spec (from Phase 1)
├── plans/YYYY-MM-DD-<plan-name>.md      # Implementation plan (from Phase 1, if generated)
├── brand.md                              # Name, tagline, tone, personality
├── design.md                             # Color palette, typography, UI style
├── tech-stack.md                         # Recommended stack with rationale
├── logos/                                # Logo system (if generated in Phase 4)
│   ├── logo.svg                          #   Primary logo (full color)
│   ├── logo-mono-dark.svg                #   Primary logo (monochrome dark)
│   ├── logo-mono-light.svg               #   Primary logo (monochrome light)
│   ├── logo-icon.svg                     #   App icon / symbol (square, no text)
│   ├── logo-icon-mono-dark.svg           #   App icon (monochrome dark)
│   ├── logo-icon-mono-light.svg          #   App icon (monochrome light)
│   ├── logo-wordmark.svg                 #   Text-only wordmark
│   ├── logo-wordmark-mono-dark.svg       #   Wordmark (monochrome dark)
│   ├── logo-wordmark-mono-light.svg      #   Wordmark (monochrome light)
│   ├── favicon.svg                       #   Favicon (simplified, 16px-legible)
│   └── USAGE.md                          #   Logo usage guidelines
└── preview.html                          # Visual brand preview (if user requested)
```

If the brainstorming skill generated an implementation plan during Phase 1, ensure it is placed in the `plans/` directory.

### brand.md format

```markdown
# [Project Name] — Brand Identity

## Name
[Chosen name]

## Tagline
[Chosen tagline]

## Tone of Voice
- Formal ←→ Casual: [position]
- Playful ←→ Serious: [position]
- Technical ←→ Approachable: [position]
- Minimal ←→ Expressive: [position]

## Personality
[3-4 attributes with brief descriptions]

## Logo

<!-- If SVG logos were generated in Phase 4: -->
Logo system saved in `logos/` directory:
- **Primary logo** (`logo.svg`) — [Brief description of the chosen concept and design rationale]
- **App icon** (`logo-icon.svg`) — [How the icon was derived from the primary]
- **Wordmark** (`logo-wordmark.svg`) — [Font and styling notes]
- **Favicon** (`favicon.svg`) — [What was simplified for small sizes]

Each variant includes full color, monochrome dark, and monochrome light versions.
See `logos/USAGE.md` for clear space rules, minimum sizes, and implementation guidelines.

<!-- If logo was skipped in Phase 4, include the brief instead: -->
### Concept 1: [Name]
- **Type:** [wordmark / lettermark / pictorial mark / abstract mark / combination mark / emblem]
- **Description:** [detailed visual description]
- **Design rationale:** [visual metaphor, why this direction, how it connects to the brand]
- **Colors:** [from palette, with color psychology reasoning]
- **Variants:** [how this concept adapts to app icon, favicon, wordmark]

### Concept 2: [Name]
...
```

### design.md format

```markdown
# [Project Name] — Visual Identity

## Color Palette (Light Mode)

| Token | Hex | Usage |
|---|---|---|
| Primary | #XXXXXX | [description] |
| ... | ... | ... |

## Color Palette (Dark Mode)

| Token | Hex | Usage |
|---|---|---|
| Background | #XXXXXX | [description] |
| ... | ... | ... |

[Key adjustments from light mode]

## Typography

- **Headings:** [Font] (weights)
- **Body:** [Font] (weights)
- **Mood:** [keywords]
- **Base size:** 16px, line-height 1.5
- **Google Fonts:** [URL]
- **CSS Import:** [snippet]

## UI Style

- **Style:** [name]
- **Keywords:** [list]
- **Key Effects:** [transitions, animations]
- **Avoid:** [anti-patterns]
```

### tech-stack.md format

```markdown
# [Project Name] — Tech Stack

## Frontend
- **Framework:** [choice] — [rationale]
- **Styling:** [choice] — [rationale]
- **Components:** [choice] — [rationale]

## Backend
- **Server/BaaS:** [choice] — [rationale]
- **Database:** [choice] — [rationale]

## Hosting
- **Platform:** [choice] — [rationale]

## Key Libraries
- [library] — [purpose and rationale]

## Alternatives Considered
[Brief notes on what was passed over and why]
```

Stage only the `docs/crucible/` files and commit with a message like:

```
Add Crucible design artifacts for [Project Name]
```

Do not stage unrelated files. Commit to the current branch.

### Visual Preview (Optional)

After generating all files, ask the user: "Want to see a visual preview of your brand in the browser?"

**If yes:** Generate `docs/crucible/preview.html` by following the template at `templates/preview.html`.

**How to use the template:**
1. Read `templates/preview.html` — it contains the exact HTML structure, CSS, and layout
2. Replace all `{{PLACEHOLDER}}` tokens with actual values from the generated brand/design/tech-stack files
3. For sections with `{{#LOOP}}...{{/LOOP}}` markers, repeat the inner HTML for each item
4. Inline the SVG logos directly (from `logos/*.svg` or generate inline). For the dark mode preview row, use the `-mono-light` variants (white logos for dark backgrounds). If Phase 4 produced a logo brief instead of SVGs, replace SVG placeholders with the text descriptions from the brief, styled as paragraph text.
5. Write the result to `docs/crucible/preview.html`

**Rules:**
- Do NOT add, remove, or reorder sections from the template
- Do NOT modify the CSS — the template's styles are the canonical design
- Only the `{{PLACEHOLDER}}` content values change between projects
- The UI Components section uses fixed component types (item list, stats, grid, buttons, inputs) — adapt the **labels and content** to the project context, not the structure
- The favicon section always shows 3 sizes: 16px, 32px, 64px (use the same SVG with `width`/`height` attributes)

**Opening the preview:**

Open the file in the user's default **browser** (not their code editor). On Windows, `.html` files are often associated with a code editor, so you must detect and launch the browser explicitly:

**Windows (2 steps):**
1. Detect the default browser:
   ```
   powershell -Command "(Get-ItemProperty 'HKCU:\Software\Microsoft\Windows\Shell\Associations\UrlAssociations\http\UserChoice').ProgId"
   ```
   Map the ProgId to a process name: `MSEdgeHTM` → `msedge`, `ChromeHTML` → `chrome`, `FirefoxURL-*` → `firefox`, `BraveHTML` → `brave`
2. Launch it with a `file:///` URL (encode spaces as `%20`):
   ```
   powershell -Command "Start-Process 'msedge' 'file:///C:/path/to/preview.html'"
   ```
   If the path contains spaces, replace them with `%20` (e.g., `John%20Ivan`).

**macOS:** `open -a "Safari" "path/to/preview.html"` (or use `open` which defaults to browser for `.html`)
**Linux:** `xdg-open "path/to/preview.html"`

Do NOT use `start "" "file_path"` on Windows — `.html` files may be associated with a code editor.

**If no:** Skip and move on.

## Phase 7: Push to Tracker (Optional)


Check if `~/.crucible/config.json` exists.

**If config exists:**
- Read the config for `api_url`, `api_key`, and `user_id`
- POST the generated files to the tracker's upload endpoint
- Report success or failure to the user

**If no config:**
- Do nothing. No errors, no warnings, no suggestions to set it up.
- The skill is complete. Files are local and ready to use.

### Config format: `~/.crucible/config.json`

```json
{
  "api_url": "https://your-app.vercel.app/api",
  "api_key": "your-api-key",
  "user_id": "your-user-id"
}
```

## Key Principles

- **One question at a time** — don't overwhelm
- **Multiple choice preferred** — easier than open-ended
- **Best-fit always** — recommend the best stack/design regardless of user familiarity
- **YAGNI** — strip unnecessary complexity from all recommendations
- **Validate incrementally** — get approval after each phase before moving on
- **Standalone first** — the skill works without any external service
