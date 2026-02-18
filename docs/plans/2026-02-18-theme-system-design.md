# Theme System Design

## Problem

Visual Explainer agents invent color palettes each time. Users who prefer a specific palette (Dracula, Nord, etc.) have no way to specify that preference.

## Solution

A theme system that lets users specify a preferred color palette via a config file. The agent reads the theme at generation time and uses its colors instead of inventing its own.

## Configuration

File: `.claude/visual-explainer.local.md`

```yaml
---
theme: dracula
---
```

Agent reads this at the start of Phase 1 (Think). If absent or empty, agent picks colors freely as today.

## Theme Files

Location: `themes/<name>.md` (one file per theme)

Each file contains:
1. CSS custom properties — `:root` block (primary mode) + `@media (prefers-color-scheme)` override
2. Mermaid `themeVariables` JSON object
3. All semantic variables: `--bg`, `--surface`, `--surface-elevated`, `--border`, `--border-bright`, `--text`, `--text-dim`, `--accent`, `--accent-dim`, `--node-a/b/c` + dim variants, `--green`, `--red`, `--orange` + dim variants

Variable names match `css-patterns.md` exactly so all existing patterns work without modification.

## Themes to Implement

Dark-first: Dracula, Nord, One Dark, Catppuccin Mocha, Tokyo Night, Gruvbox Dark, Synthwave '84

Light-first: Solarized Light, GitHub Light, Catppuccin Latte, Gruvbox Light

## Scope of Theme Control

Themes control colors only. The agent still freely chooses:
- Font pairings
- Background atmosphere pattern (dot grid, gradient mesh, etc.)
- Layout approach
- Animations
- Depth tier styling (derived from theme colors via `color-mix`)

## Files to Modify

- `SKILL.md` — Add theme override step to Phase 1
- `references/css-patterns.md` — Note in Theme Setup that active theme replaces example palette

## Files to Create

- `themes/dracula.md`
- `themes/nord.md`
- `themes/one-dark.md`
- `themes/catppuccin-mocha.md`
- `themes/tokyo-night.md`
- `themes/gruvbox-dark.md`
- `themes/synthwave-84.md`
- `themes/solarized-light.md`
- `themes/github-light.md`
- `themes/catppuccin-latte.md`
- `themes/gruvbox-light.md`

## No Changes Needed

- Templates (already use CSS custom properties)
- `libraries.md`
- `responsive-nav.md`
- Prompt files
