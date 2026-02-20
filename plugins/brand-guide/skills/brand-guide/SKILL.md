---
name: brand-guide
description: >
  Two-mode skill for brand consistency in frontend development. Mode 1 (Builder): interactively
  helps users create or refine a structured brand guide through visual previews and guided decisions.
  Mode 2 (Enforcer): reads an existing brand guide and strictly enforces it when building any frontend.
  Use this skill whenever the user mentions brand guide, brand identity, brand consistency, design system,
  style guide, design tokens, or wants to ensure visual consistency across frontends. Also trigger when
  the user has a brand-guide.json file in their uploads or references one. This skill should be used
  IN COMBINATION with the frontend-design skill — brand-guide constrains the creative choices that
  frontend-design would otherwise freestyle.
---

# Brand Guide Skill

This skill ensures frontend work stays visually consistent with a brand identity. It operates in two modes that work together: **Builder** creates the guide, **Enforcer** applies it.

## Detecting the Mode

Determine which mode to enter based on context:

**Enter Builder mode when:**
- User says "create/build/develop a brand guide"
- User says "help me define my brand" or "set up my design system"
- User wants to update or refine an existing brand guide
- User uploads visual references (logos, screenshots, mood boards) and wants to extract a system from them
- No `brand-guide.json` exists yet and the user wants to build frontends with consistency

**Enter Enforcer mode when:**
- A `brand-guide.json` file exists (in uploads or referenced by user)
- User asks to build any frontend (page, component, app, dashboard, etc.)
- User says "follow my brand" or "use my brand guide"
- User references their brand by name and a guide file is available

**Both modes in one session:**
- User creates a guide (Builder) then immediately asks to build something (Enforcer)
- User builds a frontend, notices inconsistencies, and wants to update the guide (Enforcer → Builder)

---

## Mode 1: Builder

The Builder walks the user through creating a comprehensive brand guide. The output is a `brand-guide.json` file the Enforcer can consume, plus a visual preview artifact.

### Read the interview reference first
Before starting the interview, read `references/builder-interview.md` for the full guided flow.

### Builder Principles

1. **Show, don't just ask.** For every design decision (colors, fonts, spacing), generate a visual HTML preview artifact so the user can see the options. Never ask "what color do you want?" without showing curated choices.

2. **Start from what they have.** If the user uploads a logo, screenshot, or existing site, extract colors and visual patterns from it first. Meet them where they are.

3. **Opinionated defaults.** When the user is unsure, make a strong recommendation and explain why. "I'd go with this because..." is better than "what would you prefer?"

4. **Build incrementally.** After each decision, regenerate the preview artifact so the user sees their guide taking shape in real time.

5. **Output a machine-readable file.** The final output is `brand-guide.json` following the schema in `templates/brand-guide-schema.json`. Also generate a polished visual Brand Guide artifact (HTML) as a human-friendly reference.

### Builder Flow (Summary)

The full flow is in `references/builder-interview.md`, but at a high level:

1. **Discovery** — What's the brand? What do they have already? Upload logos/screenshots?
2. **Personality & Tone** — Describe the brand in adjectives. What feeling should the UI evoke?
3. **Color Palette** — Extract from assets or build from scratch. Primary, secondary, neutral, semantic.
4. **Typography** — Heading + body + mono font pairing. Type scale.
5. **Spacing & Layout** — Spacing unit, scale, layout philosophy (airy vs dense).
6. **Shape & Depth** — Border radii, shadows, border treatments.
7. **Components** — Button style, card style, input style, navigation patterns.
8. **Motion** — Animation philosophy, duration, easing.
9. **Rules & Guardrails** — Explicit do's and don'ts.
10. **Review & Export** — Final preview artifact + `brand-guide.json` file.

### Builder Output

Two deliverables:

1. **`brand-guide.json`** — Machine-readable. Follows the schema in `templates/brand-guide-schema.json`. This is what the Enforcer reads.

2. **Brand Guide Preview** — A polished HTML artifact that visually displays the entire brand system: color swatches, typography samples, component examples, spacing visualization. This is the human-friendly reference the user can share with their team.

---

## Mode 2: Enforcer

The Enforcer reads a `brand-guide.json` and applies it strictly to all frontend output.

### Read the CSS generation reference
Before generating any frontend code, read `references/css-generation.md` for how to translate the brand guide into code.

### Enforcer Rules

These rules are absolute. The brand guide is law.

1. **Colors are locked.** Use ONLY colors defined in the brand guide. Every color in the output must trace back to a brand token. No eyeballed hex values. No "close enough."

2. **Typography is locked.** Use ONLY the fonts specified. Apply the defined type scale. Import fonts from Google Fonts or the CDN specified in the guide.

3. **Spacing follows the scale.** All margin, padding, and gap values must use the brand's spacing scale. No arbitrary pixel values.

4. **Border radii follow the system.** Use the defined radius tokens. Don't round-trip between the guide's "md" radius and some other value.

5. **Shadows and depth follow the guide.** If the guide defines shadow tokens, use them. Don't invent new shadows.

6. **Component patterns are respected.** If the guide specifies "buttons are pill-shaped with no shadow," don't make square buttons with shadows.

7. **Motion follows the philosophy.** Use the defined durations and easings. If the guide says "subtle and purposeful," don't add bouncy entrance animations.

8. **Don'ts are hard stops.** If the guide says "never use gradients on text," that means never, not "except when it would look cool."

9. **Creative freedom exists within constraints.** Layout, content structure, illustration choices, and information hierarchy are still creative decisions — but visual styling is governed by the guide.

10. **When in doubt, reference the guide.** If a situation arises not covered by the guide, choose the option most consistent with the guide's overall personality and patterns.

### Enforcer Workflow

Every time you build a frontend with a brand guide present:

1. **Parse the brand guide.** Read `brand-guide.json` and internalize every token.

2. **Generate CSS custom properties.** Start every stylesheet or `<style>` block with `:root { }` variables derived from the guide. Follow the pattern in `references/css-generation.md`.

3. **Import fonts.** Add the correct Google Fonts `<link>` or `@import` for all specified typefaces.

4. **Build the UI.** Make all creative and layout decisions, but constrain every visual property to brand tokens.

5. **Self-audit before delivering.** Before presenting the output, scan for:
   - Any hardcoded color not from the guide
   - Any font-family not from the guide
   - Any spacing value not on the scale
   - Any violation of the "don'ts" list
   Fix violations before showing the user.

### Interaction with frontend-design skill

This skill works WITH the `frontend-design` skill, not against it. Think of it this way:
- `frontend-design` provides the creative methodology, layout thinking, and implementation quality
- `brand-guide` constrains the visual palette so that creativity happens within guardrails

When both skills are active, the frontend-design skill's instruction to "choose bold, unexpected aesthetics" is tempered by: "bold and unexpected within the brand's defined system." A brand guide doesn't mean boring — it means consistently on-brand.

---

## Brand Audit Mode

If the user pastes existing HTML/CSS or shares a URL and asks "does this follow my brand?" or "audit this against my brand guide":

1. Parse the existing code for all color values, font declarations, spacing values, border-radii, and shadows.
2. Compare each against the brand guide tokens.
3. Report deviations in a clear table: what was found, what it should be, where in the code.
4. Offer to fix the deviations automatically.

---

## File Reference

| File | When to Read | Purpose |
|------|-------------|---------|
| `references/builder-interview.md` | Entering Builder mode | Full guided interview flow with visual preview instructions |
| `references/css-generation.md` | Entering Enforcer mode | How to translate brand-guide.json into CSS custom properties |
| `templates/brand-guide-schema.json` | Builder mode (output) | The JSON schema the brand guide must follow |
| `templates/example-guide.json` | Builder mode (reference) | A complete filled-out example for reference |
