# BMOSAN Skills

A plugin marketplace for Claude Code by [BMOSAN LABS](https://bmosan.com). Production-grade skills for frontend development, brand systems, and more.

Works with **Claude Code**, **Cursor**, **VS Code (Copilot)**, **OpenCode**, **Codex CLI**, and **Claude Desktop / claude.ai**.

---

## Quick Start (Claude Code)

```bash
# Add the marketplace
/plugin marketplace add bmorri13/bmosan-skills

# Install a plugin
/plugin install brand-guide@bmosan-skills
```

That's it. The skill is now available in all your Claude Code sessions.

---

## Installation by Tool

### Claude Code (Recommended — native plugin support)

**Option A: Plugin marketplace (one command)**

```bash
/plugin marketplace add bmorri13/bmosan-skills
/plugin install brand-guide@bmosan-skills
```

**Option B: Manual skill install (global — applies to all projects)**

```bash
git clone https://github.com/bmorri13/bmosan-skills.git ~/.claude/skills/bmosan-skills
```

Then add to `~/.claude/CLAUDE.md`:

```markdown
## Skills

When building frontends or working with brand/design systems, read and follow
the skill at `~/.claude/skills/bmosan-skills/plugins/brand-guide/skills/brand-guide/SKILL.md`.
```

**Option C: Manual skill install (per-project — shared with team)**

```bash
git clone https://github.com/bmorri13/bmosan-skills.git .claude/skills/bmosan-skills
```

Then add to your project's `CLAUDE.md`:

```markdown
## Skills

When building frontends or working with brand/design systems, read and follow
the skill at `.claude/skills/bmosan-skills/plugins/brand-guide/skills/brand-guide/SKILL.md`.
```

---

### Cursor

Cursor uses `.cursor/rules/` with `.mdc` files for project rules. Copy the brand guide skill content into a rule file.

**Option A: Always-on rule (recommended for Enforcer mode)**

Create `.cursor/rules/brand-guide.mdc` in your project root:

```yaml
---
description: "Brand guide enforcement for frontend development. Activates when building UI, creating components, or writing CSS/HTML."
globs: "*.html,*.css,*.jsx,*.tsx,*.vue,*.svelte"
alwaysApply: false
---
```

Then paste the contents of `plugins/brand-guide/skills/brand-guide/SKILL.md` below the frontmatter.

**Option B: Upload your brand-guide.json as context**

When chatting in Cursor, use `@brand-guide.json` to reference your guide file directly in any prompt. Combine with the rule above for maximum enforcement.

**Tip:** For the Builder interview flow, paste the contents of `references/builder-interview.md` into Cursor's chat as context, then ask it to walk you through creating a brand guide.

---

### VS Code (GitHub Copilot)

VS Code supports custom instructions via `.github/copilot-instructions.md`, scoped `.instructions.md` files, and `AGENTS.md`.

**Option A: Copilot instructions file (always-on)**

Create `.github/copilot-instructions.md` in your project root and paste the contents of `SKILL.md`:

```markdown
## Brand Guide Enforcement

When building any frontend code (HTML, CSS, React, Vue, Svelte, etc.),
always check for a brand-guide.json in the project root. If one exists,
read it first and strictly follow all defined tokens for colors, typography,
spacing, borders, motion, and component patterns.

Never freestyle visual values. Every color, font, spacing value, and
border-radius must come from the brand guide tokens.
```

**Option B: Scoped instruction file (frontend files only)**

Create `.github/instructions/brand-guide.instructions.md`:

```yaml
---
applyTo: "**/*.{html,css,jsx,tsx,vue,svelte}"
---
```

Then paste the `SKILL.md` contents below the frontmatter. This auto-attaches only when Copilot is working on frontend files.

**Option C: AGENTS.md (cross-tool compatible)**

VS Code also reads `AGENTS.md` from your project root. See the [Cross-Tool Compatibility](#cross-tool-compatibility-agentsmd) section below — the same file works in VS Code, OpenCode, and Codex.

---

### OpenCode

OpenCode reads `AGENTS.md` files and has built-in Claude Code compatibility.

**Option A: Claude Code compatibility (zero config)**

If you've already installed the skill for Claude Code (in `~/.claude/skills/` or `.claude/skills/`), OpenCode picks it up automatically. No extra setup needed.

To verify it's active, check that `OPENCODE_DISABLE_CLAUDE_CODE_SKILLS` is **not** set in your environment.

**Option B: AGENTS.md**

Add to your project's `AGENTS.md`:

```markdown
## Brand Guide

When building any frontend, first check for brand-guide.json in the project.
If found, read it and strictly enforce all visual tokens.

For the full skill instructions, read:
.claude/skills/bmosan-skills/plugins/brand-guide/skills/brand-guide/SKILL.md
```

**Option C: opencode.json instructions field**

Reference the skill files directly in `opencode.json`:

```json
{
  "$schema": "https://opencode.ai/config.json",
  "instructions": [
    "plugins/brand-guide/skills/brand-guide/SKILL.md",
    "plugins/brand-guide/skills/brand-guide/references/css-generation.md"
  ]
}
```

Or load them straight from GitHub (no local clone needed):

```json
{
  "instructions": [
    "https://raw.githubusercontent.com/bmorri13/bmosan-skills/main/plugins/brand-guide/skills/brand-guide/SKILL.md"
  ]
}
```

---

### Codex CLI (OpenAI)

Codex reads `AGENTS.md` files and supports skills via `.agents/skills/`.

**Option A: AGENTS.md**

Add to your project's `AGENTS.md` (or create one):

```markdown
## Brand Guide Enforcement

When building any frontend code, first check for a brand-guide.json in the
project. If one exists, read it and strictly follow all defined tokens:

- Colors: only use defined color tokens, never hardcode hex values
- Typography: only use specified font families and type scale
- Spacing: follow the defined spacing scale, no arbitrary pixel values
- Borders: use defined radius and shadow tokens
- Components: follow specified button, card, input, and nav patterns
- Motion: use defined durations and easings, respect philosophy

For the full brand guide skill instructions, read:
.agents/skills/brand-guide/SKILL.md
```

**Option B: Skill directory (auto-discovered)**

Codex scans `.agents/skills/` for `SKILL.md` files:

```bash
# Clone the repo and copy the skill into Codex's expected location
git clone https://github.com/bmorri13/bmosan-skills.git /tmp/bmosan-skills
mkdir -p .agents/skills/brand-guide
cp -r /tmp/bmosan-skills/plugins/brand-guide/skills/brand-guide/* .agents/skills/brand-guide/
```

Codex auto-discovers the skill based on its description and invokes it when frontend tasks come up. You can also explicitly invoke it with `$brand-guide` in the Codex composer.

**Option C: Global install**

```bash
git clone https://github.com/bmorri13/bmosan-skills.git /tmp/bmosan-skills
mkdir -p ~/.codex/skills/brand-guide
cp -r /tmp/bmosan-skills/plugins/brand-guide/skills/brand-guide/* ~/.codex/skills/brand-guide/
```

---

### Claude Desktop / claude.ai

**Option A: Project knowledge (claude.ai — best for teams)**

1. Create a Project in claude.ai
2. Upload your `brand-guide.json` to the Project's knowledge base
3. Paste the contents of `SKILL.md` into the Project's custom instructions
4. Every conversation in that Project will enforce your brand automatically

**Option B: Direct upload (per conversation)**

Upload your `brand-guide.json` at the start of any conversation, then tell Claude:

> "Read my brand guide and strictly enforce it for all frontend code you generate. Every color, font, spacing value, and border-radius must come from my guide's tokens."

**Option C: Claude Desktop with skills**

If you have Claude Desktop with skills enabled:

1. Open Claude Desktop → Settings → Skills
2. Add a new skill and upload the `SKILL.md` file
3. The skill activates automatically when you work on frontend tasks

---

### Cross-Tool Compatibility (AGENTS.md)

If you use multiple tools, the simplest approach is a single `AGENTS.md` in your project root. This file is read by **VS Code (Copilot)**, **OpenCode**, **Codex CLI**, and (as a fallback) **Claude Code**.

```markdown
# Project AI Instructions

## Brand Guide

When building any frontend, check for brand-guide.json in the project root.
If found, read it first and strictly enforce all tokens for colors, typography,
spacing, borders, motion, and component patterns.

Full skill instructions: .claude/skills/bmosan-skills/plugins/brand-guide/skills/brand-guide/SKILL.md

## Rules

- Never freestyle hex colors — use brand tokens only
- Never use fonts outside the brand's specified families
- Always generate CSS custom properties from the brand guide
- Self-audit all output against the brand guide before delivering
```

Combine this with a `.cursor/rules/brand-guide.mdc` for Cursor coverage, and you'll have brand enforcement across every major AI coding tool.

---

## Available Plugins

### 🎨 brand-guide

Create brand guides interactively and enforce them when building frontends.

**Three modes:**

| Mode         | What it does                                                                                    | Trigger                                              |
| ------------ | ----------------------------------------------------------------------------------------------- | ---------------------------------------------------- |
| **Builder**  | Walks you through a 10-stage interview to create a `brand-guide.json` and visual HTML reference | "Help me create a brand guide" or `/brand-guide`     |
| **Enforcer** | Reads your `brand-guide.json` and locks all frontend output to your tokens — no freestyling     | Upload a `brand-guide.json` and ask for any frontend |
| **Audit**    | Compares existing HTML/CSS against your guide and flags every deviation                         | "Audit this code against my brand guide"             |

**What it enforces:** colors, typography, spacing, shape (radii/shadows), components (buttons, cards, inputs, nav), motion, and explicit do's/don'ts.

---

## Repository Structure

```
bmosan-skills/
├── .claude-plugin/
│   └── marketplace.json          ← Marketplace catalog (lists all plugins)
├── plugins/
│   └── brand-guide/              ← Each plugin gets its own directory
│       ├── .claude-plugin/
│       │   └── plugin.json       ← Plugin manifest (name, description, version)
│       ├── commands/
│       │   └── brand-guide.md    ← /brand-guide slash command
│       ├── examples/
│       │   └── bmosan-brand-guide.json  ← Real-world example output
│       └── skills/
│           └── brand-guide/      ← The skill itself
│               ├── SKILL.md      ← Entry point — Claude reads this first
│               ├── references/   ← Supporting docs loaded on demand
│               │   ├── builder-interview.md
│               │   └── css-generation.md
│               └── templates/    ← Schemas and example outputs
│                   ├── brand-guide-schema.json
│                   └── example-guide.json
├── LICENSE
└── README.md
```

---

## Creating Your Own Brand Guide

1. Install the plugin (see instructions for your tool above)
2. Run `/brand-guide` (Claude Code) or ask "help me create a brand guide"
3. Walk through the 10-stage interview (colors, type, spacing, components, etc.)
4. Get your `brand-guide.json` + visual HTML reference
5. Commit the JSON to your project — the Enforcer activates automatically

See `plugins/brand-guide/examples/bmosan-brand-guide.json` for what a complete guide looks like.

---

## Contributing

PRs welcome for:

- New plugins (frontend, backend, DevOps, etc.)
- Improvements to existing skills
- Framework-specific output formats (Tailwind config, styled-components, Style Dictionary)
- Additional component patterns in the brand guide schema
- Installation guides for additional tools

---

## License

MIT — see [LICENSE](LICENSE).

---

Built by [BMOSAN LABS](https://bmosan.com) ◆ Automation, data pipelines, and digital infrastructure.
