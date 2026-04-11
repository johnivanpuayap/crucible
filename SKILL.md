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
4. **Logo** — generate SVG logos or write a brief (uses colors from Phase 3)
5. **Tech stack** — best-fit recommendation with rationale
6. **Generate output files** — write all artifacts to `docs/crucible/`
7. **Push to tracker (if configured)** — upload files via API if `~/.crucible/config.json` exists

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

## Phase 4: Logo

Now that the brand identity (Phase 2) and color palette/typography (Phase 3) are locked in, create the logo.

Ask the user: "Want me to generate some logo options using your brand colors? I can create SVG logos you can use right away, or we can skip this and just write a logo brief for later."

**If the user wants logos generated:**

Ask about preferences (one question at a time):
- **Style:** Wordmark, lettermark, icon + wordmark, abstract symbol
- **Mood:** Geometric, organic, playful, minimal, bold?
- **Any inspiration?** Existing logos they admire?

Then generate **3 SVG logo concepts** as actual code. Each logo should:
- Use the brand's color palette from Phase 3 (primary, secondary, accent)
- Use the brand's heading font from Phase 3 (or a clean sans-serif fallback)
- Be simple, clean, and scalable — logos should work at 32px and 512px
- Include the brand name (for wordmarks and icon+wordmark styles)

**SVG guidelines:**
- Keep it simple — geometric shapes, clean lines, no complex illustrations
- Use `viewBox` for proper scaling
- No raster images or external dependencies
- Each SVG should be self-contained

Present all 3 to the user (write them as temporary HTML files and open in browser if possible, or describe them clearly). Let the user:
- Pick one
- Request tweaks to a concept
- Ask for a new round
- Skip and move on

Save the chosen logo as `docs/crucible/logo.svg`.

**If the user wants to skip:**

Write a logo brief instead — a text description of 2-3 logo concepts that a designer or AI image tool could execute later. Each concept includes:
- Visual description (shape, composition, style)
- How it connects to the brand name and meaning
- Suggested colors from the Phase 3 palette

Save the brief in `brand.md` under the "## Logo" section.

**In one-shot mode:** Generate a logo brief by default unless the user explicitly requested SVG logos.

**Output:** `docs/crucible/logo.svg` (if generated) or logo brief in `brand.md`

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
└── logo.svg                              # Generated SVG logo (if user chose one)
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
<!-- If SVG logo was generated in Phase 4: -->
Generated logo saved as `logo.svg`. [Brief description of the chosen concept.]

<!-- If logo was skipped in Phase 4, include the brief instead: -->
### Concept 1: [Name]
- **Style:** [wordmark / lettermark / icon+wordmark / symbol]
- **Description:** [detailed visual description]
- **Colors:** [from palette]
- **Connection:** [how it ties to the brand name/meaning]

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
