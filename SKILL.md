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

## Phase Transitions

Between each phase, provide a brief recap and preview:

> "Great — [phase name] is locked in. Here's what we decided: [1-2 line summary]. Next up: [next phase name] — [what it involves and why it matters]. Ready?"

This keeps the user oriented and gives them a chance to revisit anything before moving forward.

## Checklist

You MUST create a task for each of these items and complete them in order:

1. **Concept exploration** — understand the idea, who it's for, what problem it solves
2. **Brand identity** — name, tagline, tone of voice, logo direction, personality
3. **Visual identity** — color palette, typography, UI style
4. **Tech stack** — best-fit recommendation with rationale
5. **Generate output files** — write all artifacts to `docs/crucible/`
6. **Push to tracker (if configured)** — upload files via API if `~/.crucible/config.json` exists

## Phase 1: Concept Exploration

Invoke the `superpowers:brainstorming` skill to explore the idea. This handles:

- What's the idea, who's it for, what problem does it solve
- Purpose, constraints, success criteria
- Scope assessment — is this one project or multiple?
- Proposal of 2-3 approaches with trade-offs
- Design spec generation

Follow the brainstorming skill's process fully. Once the design spec is written and approved, continue to Phase 2.

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

### 2d. Logo Direction

Help the user define a logo concept. Ask about:
- **Style:** Wordmark, lettermark, icon + wordmark, abstract symbol, mascot
- **Mood:** Should it feel geometric, organic, playful, minimal, bold?
- **Inspiration:** Any existing logos they admire?

Generate a text description of 2-3 logo concepts that a designer (or AI image tool) could execute. Each concept includes:
- Visual description (shape, composition, style)
- How it connects to the brand name and meaning
- Suggested colors from the palette (once Phase 3 is done, revisit this)

**Note:** Crucible does not generate images. It produces a detailed logo brief that the user can hand to a designer or an image generation tool.

### 2e. Brand Personality

Summarize in 3-4 attributes (e.g., "Calm, organized, encouraging").

**Output:** `docs/crucible/brand.md`

## Phase 3: Visual Identity

Use the `ui-ux-pro-max` skill as a design intelligence reference. Run the design system generator:

```bash
python3 [ui-ux-pro-max-scripts-path]/search.py "<product-type> <keywords>" --design-system -p "<Project Name>"
```

If the script is not available, generate recommendations manually based on the ui-ux-pro-max skill's guidelines.

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

## Phase 4: Tech Stack

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

## Phase 5: Generate Output Files

Write all artifacts to the project's `docs/crucible/` directory:

```
docs/crucible/
├── specs/YYYY-MM-DD-<topic>-design.md   # Full design spec (from Phase 1)
├── brand.md                              # Name, tagline, tone, personality
├── design.md                             # Color palette, typography, UI style
└── tech-stack.md                         # Recommended stack with rationale
```

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

## Logo Direction

### Concept 1: [Name]
- **Style:** [wordmark / lettermark / icon+wordmark / symbol / mascot]
- **Description:** [detailed visual description]
- **Colors:** [from palette]
- **Connection:** [how it ties to the brand name/meaning]

### Concept 2: [Name]
...

### Concept 3: [Name]
...
```

### design.md format

```markdown
# [Project Name] — Visual Identity

## Color Palette

| Token | Hex | Usage |
|---|---|---|
| Primary | #XXXXXX | [description] |
| ... | ... | ... |

### Dark Mode
[Dark mode variant description and key color adjustments]

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

Commit all generated files to git.

## Phase 6: Push to Tracker (Optional)

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
