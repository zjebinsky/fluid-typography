# Fluid Typography — Claude Code Skill

A [Claude Code skill](https://skills.sh/) that generates a complete fluid typography and layout scaling system in CSS, tuned for editorial-style web design.

## What it does

Generates a proportional CSS scaling system anchored to your Figma artboard dimensions. Font sizes, spacing, and layout all scale fluidly across every screen size — no manual media query overrides needed.

```css
/* Everything you need, ready to paste */
html { font-size: var(--size-font); }

h1   { font-size: 7.5rem; }   /* 120px in Figma → scales automatically */
h2   { font-size: 4rem; }     /* 64px */
p    { font-size: 1.125rem; } /* 18px */

.article-body { max-width: 40rem; }     /* comfortable reading column */
.full-bleed   { width: 100vw; }         /* edge-to-edge */
```

## Install

Pick your AI tool:

### Claude Code
```bash
npx skills add zjebinsky/fluid-typography
```
Then ask: *"set up fluid typography"* or *"add the scaling system"*

---

### Cursor
Copy `platforms/cursor.mdc` into your project:
```bash
mkdir -p .cursor/rules
curl -o .cursor/rules/fluid-typography.mdc \
  https://raw.githubusercontent.com/zjebinsky/fluid-typography/master/platforms/cursor.mdc
```
Cursor will apply it automatically when working on CSS files.

---

### GitHub Copilot
Copy `platforms/copilot-instructions.md` into your project:
```bash
mkdir -p .github
curl -o .github/copilot-instructions.md \
  https://raw.githubusercontent.com/zjebinsky/fluid-typography/master/platforms/copilot-instructions.md
```

---

### OpenAI Codex CLI
Copy `platforms/AGENTS.md` to your project root:
```bash
curl -o AGENTS.md \
  https://raw.githubusercontent.com/zjebinsky/fluid-typography/master/platforms/AGENTS.md
```

---

### opencode
Same as Codex — copy `platforms/AGENTS.md` to your project root:
```bash
curl -o AGENTS.md \
  https://raw.githubusercontent.com/zjebinsky/fluid-typography/master/platforms/AGENTS.md
```

---

### Gemini CLI
Copy `platforms/GEMINI.md` to your project root:
```bash
curl -o GEMINI.md \
  https://raw.githubusercontent.com/zjebinsky/fluid-typography/master/platforms/GEMINI.md
```

## What's included

- **Scaling system** — viewport-proportional `font-size` on `html`, so every `rem` value scales automatically
- **4 breakpoints** — Desktop, Tablet, Mobile Landscape, Mobile Portrait
- **Configurable** — set your Figma artboard widths and max viewport per project
- **Editorial type scale** — Display → Headline → Title → Subheading → Body → Meta → Caption
- **Layout patterns** — reading column, breakout, full-bleed, pull quote, drop cap, section rhythm
- **Rem conversion guide** — how to translate any Figma px value to rem

## How it works

The system sets a `--size-font` CSS variable that scales the root font size proportionally to the viewport, relative to your Figma design width:

```
font-size = viewport width ÷ (design width ÷ base font size)
```

At your design width, `1rem = base font size`. At any other viewport, everything scales in proportion. No JavaScript, no build step — pure CSS custom properties.

## Configuration

| Variable | Description | Default |
|---|---|---|
| `--size-unit` | Base font size from Figma (no px) | `16` |
| `--size-design` | Figma artboard width per breakpoint (no px) | `1500` desktop, `393` mobile |
| `--size-scale-max` | Widest viewport the system scales to | `2560px` |

## License

MIT
