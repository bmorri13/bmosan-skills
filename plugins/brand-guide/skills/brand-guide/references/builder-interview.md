# Builder Interview Flow

This reference guides the interactive process of building a brand guide with the user. Each stage produces visual previews so the user can see their decisions taking shape.

## General Approach

- Ask 1-2 questions at a time, never overwhelm with a wall of choices
- After every major decision, regenerate the running preview artifact
- If the user uploads assets (logo, screenshots, existing site), analyze them FIRST and extract what you can before asking questions
- Be opinionated: "I'd recommend X because..." is always better than "what do you want?"
- If the user says "I don't know" or "you pick," make a confident choice and explain your reasoning

## Stage 1: Discovery

**Goal:** Understand what exists and what's needed.

Questions to ask (adapt based on context):
- "What's the brand name?"
- "Do you have any existing assets — a logo, current website, screenshots, or colors you already use?"
- "Who's the audience? (developers, consumers, enterprise clients, etc.)"
- "Are there any brands whose visual style you admire?"

**If the user uploads assets:**
- Extract dominant colors from logos/screenshots using visual analysis
- Identify any existing font choices
- Note the overall visual direction (minimal, bold, playful, corporate, etc.)
- Present your findings: "From your logo, I'm seeing these core colors: [swatches]. And the overall vibe feels [description]. Sound right?"

**If starting from scratch:**
- Move directly to personality/tone to establish a foundation

## Stage 2: Personality & Tone

**Goal:** Define the brand's character in words before visuals.

Ask the user to pick 3-5 adjectives that describe their brand. Offer a curated selection organized by spectrum:

```
Professional ←→ Playful
Minimal ←→ Maximalist  
Traditional ←→ Modern
Serious ←→ Whimsical
Corporate ←→ Indie
Luxury ←→ Accessible
Bold ←→ Subtle
Technical ←→ Friendly
```

Synthesize their choices into a short tone statement:
> "Confident and modern with a technical edge, but approachable — never cold or corporate."

This statement goes into the brand guide and informs every subsequent decision.

## Stage 3: Color Palette

**Goal:** Define primary, secondary, neutral, and semantic colors.

### If extracted from assets:
- Present the extracted colors as a starting palette
- Suggest complementary additions for secondary/accent

### If building from scratch:
Generate 3 distinct palette options as an HTML preview artifact. Each option should:
- Have a primary color that matches the brand personality
- Include a complementary secondary color
- Show full neutral scale (50-950)
- Include semantic colors (success, warning, error, info)

**Preview artifact should show:**
- Large swatches with hex values and names
- A mini UI mockup (button, card, nav) using each palette
- Light and dark mode variants

### Color structure to define:
```
primary:    base, light, dark, contrast (text color on primary)
secondary:  base, light, dark, contrast
accent:     base (optional pop color)
neutral:    50, 100, 200, 300, 400, 500, 600, 700, 800, 900, 950
semantic:   success, warning, error, info
background: primary (main bg), secondary (card/surface bg), tertiary (subtle sections)
text:       primary (headings/body), secondary (muted), tertiary (subtle), inverse (on dark)
border:     default, strong, subtle
```

Ask the user to pick a palette, then refine if needed.

## Stage 4: Typography

**Goal:** Select font pairings and define the type scale.

Generate 3 font pairing options as an HTML preview. For each:
- A display/heading font
- A body font
- A monospace font (for code/technical content)

**Preview artifact should show:**
- Each pairing rendering the same sample content (a heading, a paragraph, a button label, a code snippet)
- Multiple heading sizes (h1-h4) to show the hierarchy
- The fonts loaded from Google Fonts

### Type scale to define:
```
xs:    0.75rem   (12px) — captions, fine print
sm:    0.875rem  (14px) — secondary text, labels
base:  1rem      (16px) — body text
lg:    1.125rem  (18px) — lead paragraphs
xl:    1.25rem   (20px) — h4 / small headings
2xl:   1.5rem    (24px) — h3
3xl:   1.875rem  (30px) — h2
4xl:   2.25rem   (36px) — h1
5xl:   3rem      (48px) — display / hero
```

Also define:
- Line heights (tight: 1.25, normal: 1.5, relaxed: 1.75)
- Font weights used (regular, medium, semibold, bold)
- Letter spacing adjustments if any

## Stage 5: Spacing & Layout

**Goal:** Define the spacing system and layout philosophy.

Present two approaches with visual preview:

**Airy / Generous spacing:**
- Base unit: 4px (0.25rem)
- Generous padding, lots of breathing room
- Good for: luxury, editorial, minimal brands

**Compact / Dense spacing:**
- Base unit: 4px (0.25rem) but tighter scale usage
- Efficient use of space
- Good for: dashboards, technical tools, data-heavy UIs

**Preview artifact should show:**
- Same card component rendered with both spacing approaches
- Same page section with both approaches

### Spacing scale to define:
```
0:   0
px:  1px
0.5: 0.125rem  (2px)
1:   0.25rem   (4px)
2:   0.5rem    (8px)
3:   0.75rem   (12px)
4:   1rem      (16px)
5:   1.25rem   (20px)
6:   1.5rem    (24px)
8:   2rem      (32px)
10:  2.5rem    (40px)
12:  3rem      (48px)
16:  4rem      (64px)
20:  5rem      (80px)
24:  6rem      (96px)
```

Also define:
- Container max-width (e.g., 1280px)
- Content max-width for readable text (e.g., 65ch)
- Section padding defaults

## Stage 6: Shape & Depth

**Goal:** Define border radii, shadows, and border treatments.

Generate a preview showing the same card and button with different shape systems:

**Sharp** — 0-2px radii, crisp edges (corporate, editorial)
**Soft** — 6-12px radii, gentle rounding (friendly, modern)
**Round** — 16px+ radii, very rounded (playful, approachable)
**Mixed** — Sharp containers, rounded interactive elements

### Tokens to define:
```
borderRadius:
  none: 0
  sm:   2px (or 4px)
  md:   6px (or 8px)
  lg:   12px (or 16px)
  xl:   24px
  full: 9999px (pills, circles)

shadows:
  sm:   subtle lift
  md:   medium card shadow
  lg:   pronounced elevation
  xl:   dramatic/modal shadow
  inner: inset shadow (for pressed states)
  none:  explicitly no shadow

borders:
  width: 1px (default)
  style: solid
  color: references border tokens from colors
```

## Stage 7: Components

**Goal:** Define the visual patterns for core UI components.

Generate a component showcase artifact showing all of these with the already-chosen brand tokens applied:

### Buttons
- Primary (filled), secondary (outlined), tertiary (ghost/text)
- Sizes: sm, md, lg
- States: default, hover, active, disabled
- Decide: rounded or pill? shadow or flat? uppercase text?

### Cards
- Default card style
- Interactive (hoverable) variant
- Decide: bordered, shadowed, or both? Background color?

### Inputs
- Text input, select, checkbox, radio
- States: default, focus, error, disabled
- Decide: underline style, outlined, or filled?

### Navigation
- Top nav style preferences
- Mobile menu approach (hamburger, bottom nav, slide-out)

Ask the user to approve or adjust each component pattern.

## Stage 8: Motion & Animation

**Goal:** Define the animation philosophy.

Present 3 philosophies with subtle animated previews:

**Minimal** — Almost no animation. Content appears instantly. Hover states are instant color changes. For serious/professional brands.

**Subtle & Purposeful** — Gentle fades, slight lifts on hover, smooth transitions. Nothing bouncy or attention-grabbing. The most universally safe choice.

**Expressive** — Staggered reveals, playful hover effects, entrance animations. For brands that want personality and delight.

### Tokens to define:
```
motion:
  philosophy: "subtle and purposeful" (or their choice)
  durations:
    fast:   100ms (hover states, toggles)
    normal: 200ms (transitions, reveals)
    slow:   400ms (page transitions, complex animations)
  easings:
    default:  cubic-bezier(0.4, 0, 0.2, 1)  — general purpose
    enter:    cubic-bezier(0, 0, 0.2, 1)     — elements appearing
    exit:     cubic-bezier(0.4, 0, 1, 1)     — elements leaving
    bounce:   cubic-bezier(0.34, 1.56, 0.64, 1) — playful (if expressive)
  reduced-motion: true  (always respect prefers-reduced-motion)
```

## Stage 9: Rules & Guardrails

**Goal:** Define explicit do's and don'ts.

Based on everything defined so far, suggest a list of guardrails and ask the user to confirm, add, or remove:

**Common do's:**
- Always use the defined color tokens, never hardcode hex values
- Always import brand fonts, never fall back to system fonts in designs
- Maintain consistent spacing using the scale
- Use semantic color tokens for status (success/error/warning)

**Common don'ts:**
- Never use gradients unless specifically defined in the guide
- Never mix rounded and sharp radii on the same level of hierarchy
- Never use more than 3 font weights on a single page
- Never use pure black (#000) or pure white (#FFF) — use the neutral scale
- Never auto-play animations or use animation durations over 500ms
- Never use more than 2 accent colors on a single screen

Ask: "Are there any other rules specific to your brand?"

## Stage 10: Review & Export

**Goal:** Final review and file generation.

1. Generate the complete Brand Guide Preview artifact — a polished, single-page HTML reference showing:
   - Brand name and personality statement
   - Full color palette with swatches and values
   - Typography samples at all scale sizes
   - Spacing visualization
   - Component showcase (buttons, cards, inputs)
   - Do's and Don'ts list

2. Generate `brand-guide.json` following the schema in `templates/brand-guide-schema.json`

3. Present both to the user: "Here's your brand guide — the visual reference and the JSON file that Claude will use to enforce it. Want to adjust anything?"

4. Save the JSON to the outputs directory so the user can download it and reuse it in future conversations.

## Updating an Existing Guide

If the user already has a `brand-guide.json` and wants to modify it:

1. Parse the existing guide
2. Generate the visual preview from it
3. Ask what they want to change
4. Walk through only the relevant stages
5. Regenerate both outputs

Don't make them redo the entire interview — jump to the specific section they want to change.
