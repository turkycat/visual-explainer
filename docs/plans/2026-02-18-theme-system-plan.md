# Theme System Implementation Plan

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Add a theme system that lets users specify a preferred color palette (Dracula, Nord, etc.) via a config file, with 11 popular themes.

**Architecture:** Each theme is a standalone `.md` file in `themes/` containing CSS custom properties and Mermaid themeVariables. The agent reads `.claude/visual-explainer.local.md` for the user's theme preference, then reads the corresponding theme file to get the color palette. All existing CSS patterns work unchanged because theme files use the same variable names.

**Tech Stack:** CSS custom properties, Mermaid themeVariables JSON, markdown documentation files.

---

### Task 1: Create Dracula theme file

**Files:**
- Create: `themes/dracula.md`

**Step 1: Create the themes directory**

```bash
mkdir -p themes
```

**Step 2: Write themes/dracula.md**

The file contains:
- Description noting it's dark-first
- CSS `:root` block with Dracula dark colors as primary
- `@media (prefers-color-scheme: light)` override with Alucard (official Dracula light variant) colors
- Mermaid themeVariables JSON matching the dark palette
- All semantic variables: `--bg`, `--surface`, `--surface-elevated`, `--border`, `--border-bright`, `--text`, `--text-dim`, `--accent`, `--accent-dim`, `--node-a/b/c` + dim variants, `--green`, `--red`, `--orange` + dim variants

Official Dracula colors:
- Background: #282a36, Current Line: #44475a, Foreground: #f8f8f2, Comment: #6272a4
- Cyan: #8be9fd, Green: #50fa7b, Orange: #ffb86c, Pink: #ff79c6, Purple: #bd93f9, Red: #ff5555, Yellow: #f1fa8c

Official Alucard (light) colors:
- Background: #fffbeb, Foreground: #1f1f1f, Comment: #6c664b
- Cyan: #036a96, Green: #14710a, Orange: #a34d14, Pink: #a3144d, Purple: #644ac9, Red: #cb3a2a, Yellow: #846e15

Map to CSS vars: `--accent` = purple (BD93F9, the signature Dracula color), `--node-a` = cyan, `--node-b` = green, `--node-c` = pink.

**Step 3: Commit**

```bash
git add themes/dracula.md
git commit -m "feat: add Dracula theme"
```

### Task 2: Create Nord theme file

**Files:**
- Create: `themes/nord.md`

**Step 1: Write themes/nord.md**

Dark-first theme. Official Nord colors:

Polar Night (backgrounds): #2e3440, #3b4252, #434c5e, #4c566a
Snow Storm (text): #d8dee9, #e5e9f0, #eceff4
Frost (accents): #8fbcbb, #88c0d0, #81a1c1, #5e81ac
Aurora: red #bf616a, orange #d08770, yellow #ebcb8b, green #a3be8c, purple #b48ead

Map: `--bg` = #2e3440, `--surface` = #3b4252, `--text` = #eceff4, `--accent` = #88c0d0 (frost blue), `--node-a` = #88c0d0, `--node-b` = #a3be8c, `--node-c` = #b48ead.

Light mode: invert — `--bg` = #eceff4, `--surface` = #e5e9f0, `--text` = #2e3440, keep same accent hues but use darker variants (#5e81ac for accent).

**Step 2: Commit**

```bash
git add themes/nord.md
git commit -m "feat: add Nord theme"
```

### Task 3: Create One Dark theme file

**Files:**
- Create: `themes/one-dark.md`

**Step 1: Write themes/one-dark.md**

Dark-first. Atom One Dark colors:

Background: #282c34, Foreground: #abb2bf, Gutter: #636d83
Red: #e06c75, Green: #98c379, Yellow: #e5c07b, Blue: #61afef, Purple: #c678dd, Cyan: #56b6c2

Map: `--accent` = #61afef (blue), `--node-a` = #61afef, `--node-b` = #98c379, `--node-c` = #c678dd.

Light mode: `--bg` = #fafafa, `--text` = #383a42, accent = #4078f2, green = #50a14f, red = #e45649.

**Step 2: Commit**

```bash
git add themes/one-dark.md
git commit -m "feat: add One Dark theme"
```

### Task 4: Create Catppuccin Mocha theme file

**Files:**
- Create: `themes/catppuccin-mocha.md`

**Step 1: Write themes/catppuccin-mocha.md**

Dark-first. Official Catppuccin Mocha colors:

Base: #1e1e2e, Mantle: #181825, Surface 0: #313244, Surface 1: #45475a, Surface 2: #585b70
Text: #cdd6f4, Subtext 1: #bac2de, Overlay 0: #6c7086
Mauve: #cba6f7, Blue: #89b4fa, Sapphire: #74c7ec, Teal: #94e2d5, Green: #a6e3a1
Yellow: #f9e2af, Peach: #fab387, Red: #f38ba8, Pink: #f5c2e7, Lavender: #b4befe

Map: `--accent` = #cba6f7 (mauve), `--node-a` = #89b4fa, `--node-b` = #a6e3a1, `--node-c` = #f5c2e7.

Light mode: Use Catppuccin Latte values.

**Step 2: Commit**

```bash
git add themes/catppuccin-mocha.md
git commit -m "feat: add Catppuccin Mocha theme"
```

### Task 5: Create Tokyo Night theme file

**Files:**
- Create: `themes/tokyo-night.md`

**Step 1: Write themes/tokyo-night.md**

Dark-first. Official Tokyo Night colors:

Background: #1a1b26, Foreground: #a9b1d6, Comment: #565f89
Red: #f7768e, Orange: #ff9e64, Yellow: #e0af68, Green: #9ece6a
Cyan: #2ac3de, Blue: #7aa2f7, Purple: #bb9af7

Map: `--accent` = #7aa2f7 (blue), `--node-a` = #7aa2f7, `--node-b` = #9ece6a, `--node-c` = #bb9af7.

Light mode (Tokyo Night Light): `--bg` = #e6e7ed (official), `--text` = #343b58, Blue: #2959aa, Green: #385f0d, Red: #8c4351.

**Step 2: Commit**

```bash
git add themes/tokyo-night.md
git commit -m "feat: add Tokyo Night theme"
```

### Task 6: Create Gruvbox Dark theme file

**Files:**
- Create: `themes/gruvbox-dark.md`

**Step 1: Write themes/gruvbox-dark.md**

Dark-first. Official Gruvbox colors:

dark0: #282828, dark1: #3c3836, dark2: #504945, dark3: #665c54
light0: #fbf1c7, light1: #ebdbb2, light4 (gray): #a89984
Bright accents: red #fb4934, green #b8bb26, yellow #fabd2f, blue #83a598, purple #d3869b, aqua #8ec07c, orange #fe8019

Map: `--accent` = #fe8019 (orange, Gruvbox signature), `--node-a` = #83a598, `--node-b` = #b8bb26, `--node-c` = #d3869b.

Light mode: `--bg` = #fbf1c7, `--text` = #3c3836, use faded accent variants (red #9d0006, green #79740e, etc.).

**Step 2: Commit**

```bash
git add themes/gruvbox-dark.md
git commit -m "feat: add Gruvbox Dark theme"
```

### Task 7: Create Synthwave '84 theme file

**Files:**
- Create: `themes/synthwave-84.md`

**Step 1: Write themes/synthwave-84.md**

Dark-first. SynthWave '84 colors:

Background: #262335, Sidebar: #241b2f, Activity: #171520
Foreground: #ffffff, Comment: #848bbd
Pink: #ff7edb, Cyan: #36f9f6, Green: #72f1b8, Yellow: #fede5d, Orange: #ff8b39, Red: #fe4450, Coral: #f97e72

Map: `--accent` = #ff7edb (hot pink, signature neon), `--node-a` = #36f9f6, `--node-b` = #72f1b8, `--node-c` = #fede5d.

Light mode: Desaturated versions — `--bg` = #f5f0ff, `--text` = #262335, muted accent versions.

**Step 2: Commit**

```bash
git add themes/synthwave-84.md
git commit -m "feat: add Synthwave 84 theme"
```

### Task 8: Create Solarized Light theme file

**Files:**
- Create: `themes/solarized-light.md`

**Step 1: Write themes/solarized-light.md**

Light-first. Official Solarized colors (Ethan Schoonover):

base3 (bg): #fdf6e3, base2: #eee8d5, base1: #93a1a1, base00 (text): #657b83
base0: #839496, base01: #586e75, base02: #073642, base03: #002b36
Yellow: #b58900, Orange: #cb4b16, Red: #dc322f, Magenta: #d33682, Violet: #6c71c4, Blue: #268bd2, Cyan: #2aa198, Green: #859900

Map: `--accent` = #268bd2 (blue), `--node-a` = #268bd2, `--node-b` = #859900, `--node-c` = #d33682.

Dark mode: `--bg` = #002b36, `--surface` = #073642, `--text` = #fdf6e3, same accent colors.

**Step 2: Commit**

```bash
git add themes/solarized-light.md
git commit -m "feat: add Solarized Light theme"
```

### Task 9: Create GitHub Light theme file

**Files:**
- Create: `themes/github-light.md`

**Step 1: Write themes/github-light.md**

Light-first. GitHub Primer colors:

Background: #ffffff, Surface: #f6f8fa, Border: #d0d7de, Text: #1f2328, Text dim: #656d76
Blue: #0969da, Green: #1a7f37, Red: #cf222e, Orange: #bc4c00, Purple: #8250df

Map: `--accent` = #0969da (GitHub blue), `--node-a` = #0969da, `--node-b` = #1a7f37, `--node-c` = #8250df.

Dark mode (GitHub Dark): `--bg` = #0d1117, `--surface` = #161b22, `--text` = #e6edf3, Blue: #58a6ff, Green: #3fb950, Red: #f85149.

**Step 2: Commit**

```bash
git add themes/github-light.md
git commit -m "feat: add GitHub Light theme"
```

### Task 10: Create Catppuccin Latte theme file

**Files:**
- Create: `themes/catppuccin-latte.md`

**Step 1: Write themes/catppuccin-latte.md**

Light-first. Official Catppuccin Latte colors:

Base: #eff1f5, Mantle: #e6e9ef, Crust: #dce0e8, Surface 0: #ccd0da, Surface 1: #bcc0cc
Text: #4c4f69, Subtext 1: #5c5f77, Overlay 0: #9ca0b0
Mauve: #8839ef, Blue: #1e66f5, Sapphire: #209fb5, Teal: #179299, Green: #40a02b
Yellow: #df8e1d, Peach: #fe640b, Red: #d20f39, Pink: #ea76cb, Lavender: #7287fd

Map: `--accent` = #8839ef (mauve), `--node-a` = #1e66f5, `--node-b` = #40a02b, `--node-c` = #ea76cb.

Dark mode: Use Catppuccin Mocha values.

**Step 2: Commit**

```bash
git add themes/catppuccin-latte.md
git commit -m "feat: add Catppuccin Latte theme"
```

### Task 11: Create Gruvbox Light theme file

**Files:**
- Create: `themes/gruvbox-light.md`

**Step 1: Write themes/gruvbox-light.md**

Light-first. Official Gruvbox light colors:

light0: #fbf1c7, light1: #ebdbb2, light2: #d5c4a1
dark0 (text): #282828, dark1: #3c3836, dark4 (gray): #7c6f64
Faded accents: red #9d0006, green #79740e, yellow #b57614, blue #076678, purple #8f3f71, aqua #427b58, orange #af3a03

Map: `--accent` = #af3a03 (orange), `--node-a` = #076678, `--node-b` = #79740e, `--node-c` = #8f3f71.

Dark mode: Use Gruvbox Dark values (bright accents on #282828).

**Step 2: Commit**

```bash
git add themes/gruvbox-light.md
git commit -m "feat: add Gruvbox Light theme"
```

### Task 12: Update SKILL.md with theme override step

**Files:**
- Modify: `SKILL.md:19-27` (Phase 1: Think section)

**Step 1: Add theme override paragraph**

After the existing "What aesthetic?" list (around line 37), add:

```markdown
**Theme override.** Check if `.claude/visual-explainer.local.md` exists in the project root and contains a `theme:` field in its YAML frontmatter. If it does, read `./themes/<theme-name>.md` from this skill's directory and use its CSS custom properties and Mermaid themeVariables instead of inventing your own palette. The theme controls colors only — you still choose fonts, layout, background atmosphere patterns, and animations freely. If the theme specifies dark-first, place its primary palette in `:root` and the alternate in the `@media (prefers-color-scheme)` query. If no config file exists or no theme is set, pick colors freely as usual.

Available themes: `dracula`, `nord`, `one-dark`, `catppuccin-mocha`, `tokyo-night`, `gruvbox-dark`, `synthwave-84`, `solarized-light`, `github-light`, `catppuccin-latte`, `gruvbox-light`.
```

**Step 2: Commit**

```bash
git add SKILL.md
git commit -m "feat: add theme override step to SKILL.md Phase 1"
```

### Task 13: Update css-patterns.md Theme Setup section

**Files:**
- Modify: `references/css-patterns.md:5-51` (Theme Setup section)

**Step 1: Add theme note**

After the "Always define both light and dark palettes via custom properties" sentence on line 7, add:

```markdown
If a theme is active (configured in `.claude/visual-explainer.local.md`), replace the example palette below with the theme's CSS custom properties. The variable names are identical, so all patterns in this file work unchanged. Read the theme file from `./themes/<theme-name>.md` for the exact values.
```

**Step 2: Commit**

```bash
git add references/css-patterns.md
git commit -m "feat: add theme system note to css-patterns.md"
```

### Task 14: Update README with theme documentation

**Files:**
- Modify: `README.md`

**Step 1: Add Themes section**

Add a section documenting:
- How to set a theme (create `.claude/visual-explainer.local.md` with `theme: <name>`)
- List of available themes with brief descriptions
- How to add custom themes

**Step 2: Commit**

```bash
git add README.md
git commit -m "docs: add theme system documentation to README"
```
