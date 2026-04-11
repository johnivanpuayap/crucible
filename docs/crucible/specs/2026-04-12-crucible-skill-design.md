# Crucible — Skill Design Spec

**Date:** 2026-04-12
**Tagline:** "Where raw ideas survive the heat"
**Type:** Claude Code Skill (standalone, shareable)

---

## Overview

Crucible is a Claude Code skill that takes a raw idea and transforms it into a fully designed project — brand identity, visual design system, and tech stack recommendation. It is not tied to any backend or project tracker. It produces local files that can optionally be pushed to an external app.

Crucible is designed to be shared with other developers directly (not published to a public marketplace) since it builds on top of existing skills.

## Modes

### Interactive (default)

Walks the user through a guided conversation, one question at a time, multiple choice when possible. Builds up the full project design incrementally with validation at each phase.

### One-shot

User describes everything upfront in a single prompt. Crucible generates the full package in one pass. Useful when the user already has a clear vision and wants to skip the conversation.

## Phases

### Phase 1: Concept Exploration

**Delegated to:** `superpowers:brainstorming`

- What's the idea, who's it for, what problem does it solve
- Purpose, constraints, success criteria
- Scope assessment — is this one project or multiple?
- Produces the design spec document

### Phase 2: Brand Identity

**Handled by:** Crucible (custom logic)

- Name suggestions (3-5 candidates with rationale)
- Tagline options
- Tone of voice definition (formal/casual, playful/serious, etc.)
- Brand personality attributes

### Phase 3: Visual Identity

**Guided by:** `ui-ux-pro-max` (as a reference/intelligence tool)

- Color palette selection (primary, secondary, accent, backgrounds, semantic colors)
- Typography pairing (heading + body fonts via Google Fonts)
- UI style recommendation (flat, glassmorphism, minimal, etc.)
- Component style direction
- Light/dark mode considerations

### Phase 4: Tech Stack Recommendation

**Handled by:** Crucible (custom logic)

- Recommends the best-fit stack based on the project's needs
- Always recommends best-fit regardless of user familiarity
- Covers: frontend framework, backend/database, hosting, key libraries
- Includes rationale for each choice

### Phase 5: Output

**Handled by:** Crucible

- Generates all artifact files (see Output Files below)
- If Canopy (or any tracker) config exists (`~/.crucible/config.json`), pushes files via API
- If no config, files are generated locally only — no errors, no nagging

## Output Files

All files are generated in the project's `docs/crucible/` directory:

| File | Content |
|---|---|
| `docs/crucible/specs/YYYY-MM-DD-<topic>-design.md` | Full design spec (from brainstorming) |
| `docs/crucible/plans/YYYY-MM-DD-<plan-name>.md` | Implementation plan (from brainstorming) |
| `docs/crucible/brand.md` | Name, tagline, tone of voice, personality |
| `docs/crucible/design.md` | Visual identity — palette, typography, style, component approach |
| `docs/crucible/tech-stack.md` | Recommended stack with rationale for each choice |

## Optional Integration

Crucible can optionally push generated files to an external tracker app (like Canopy) via an API endpoint.

### Config File: `~/.crucible/config.json`

```json
{
  "api_url": "https://your-app.vercel.app/api",
  "api_key": "your-api-key",
  "user_id": "your-user-id"
}
```

### Behavior

- **Config exists:** Skill calls the API endpoint at the end of its run to upload files + metadata
- **No config:** Skill generates files locally only. Fully functional without any external service.

### Claude Code Hook Integration

A post-commit hook can be configured in Claude Code settings to detect changes in `docs/crucible/` and sync them to the tracker app. This catches manual edits to specs or plans that happen outside of the skill's run.

## Skill Distribution

- Not published to public marketplace (depends on other skills)
- Shared directly with other developers as a Claude Code skill
- Installable via `npx skills add` from a GitHub repo
- Works with any project — no assumptions about the user's stack or setup

## Dependencies

| Skill | Purpose |
|---|---|
| `superpowers:brainstorming` | Concept exploration, design spec generation |
| `ui-ux-pro-max` | Visual identity intelligence (color, typography, style recommendations) |
