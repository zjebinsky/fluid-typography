---
name: fluid-typography
description: >
  Generates a complete fluid typography and layout scaling system in CSS, tuned
  for editorial-style web design. Use this skill whenever the user wants to set
  up responsive/fluid typography, build an editorial, magazine, or article-based
  layout, asks about scaling CSS across breakpoints, mentions a Figma design they
  want to match at multiple screen sizes, or says things like "fluid type",
  "viewport scaling", "scale font with screen size", "editorial layout", or
  "fluid layout system". Always use this skill even if the user just says
  "set up fluid typography" or "add the scaling system" without further detail.
---

# Fluid Typography System — Editorial Focus

This skill generates a CSS fluid typography system that scales fonts and layouts
proportionally across all screen sizes, anchored to Figma artboard dimensions.
It is optimised for editorial-style web design: expressive display type, strong
typographic hierarchy, generous whitespace, and structured reading layouts.

## How it works

The system sets `--size-font` on `html`, which makes `1rem` equal the fluid scaled
size everywhere. Every value written in `rem` scales automatically across all
viewports — no media query overrides needed for sizing.

## Step 1: Gather configuration

Ask the user for the following. Use these defaults if they don't specify:

| Variable | What to ask | Default |
|---|---|---|
| `--size-unit` | Body font size in their Figma design (px, no unit) | `16` |
| `--size-scale-max` | Widest viewport the system should scale to (px) | `2560px` |
| Desktop `--size-design` | Figma artboard width — Desktop | `1500` |
| Tablet `--size-design` | Figma artboard width — Tablet | `834` |
| Mobile Landscape `--size-design` | Figma artboard width — Mobile Landscape | `550` |
| Mobile Portrait `--size-design` | Figma artboard width — Mobile Portrait | `393` |

You don't need to ask for other min/max values — use the standard breakpoint ranges below.

## Step 2: Output the CSS

Use this exact template, substituting the user's values for the ✦ marked lines:

```css
/* ============================================================
   Fluid Typography System

   HOW IT WORKS:
   Font size and layout scale proportionally with the viewport,
   anchored to your Figma design dimensions.

   WHAT TO CONFIGURE (marked with ✦):
   - --size-unit          Base font size from your design (px, no unit)
   - --size-design        Your Figma artboard width for each breakpoint (px, no unit)
   - --size-scale-max     Widest viewport the system scales to (px)
   ============================================================ */

/* Desktop */
:root {
  --size-unit: 16;              /* ✦ Body font-size in your Figma design (no px) */
  --size-design: 1500;          /* ✦ Figma artboard width — Desktop (no px) */
  --size-scale-min: 992px;
  --size-scale-max: 2560px;     /* ✦ Max viewport to scale to */

  /* — Computed — do not edit below this line — */
  --size-container: clamp(var(--size-scale-min), 100vw, var(--size-scale-max));
  --size-font: calc(var(--size-container) / (var(--size-design) / var(--size-unit)));
}

/* Tablet  |  768px – 991px */
@media screen and (max-width: 991px) {
  :root {
    --size-design: 834;         /* ✦ Figma artboard width — Tablet */
    --size-scale-min: 768px;
    --size-scale-max: 991px;
  }
}

/* Mobile Landscape  |  480px – 767px */
@media screen and (max-width: 767px) {
  :root {
    --size-design: 550;         /* ✦ Figma artboard width — Mobile Landscape */
    --size-scale-min: 480px;
    --size-scale-max: 767px;
  }
}

/* Mobile Portrait  |  320px – 479px */
@media screen and (max-width: 479px) {
  :root {
    --size-design: 393;         /* ✦ Figma artboard width — Mobile Portrait */
    --size-scale-min: 320px;
    --size-scale-max: 479px;
  }
}
```

## Step 3: Output the usage snippet

Always include this after the main CSS block:

```css
/* ============================================================
   USAGE
   ============================================================ */

/* 1. Apply fluid font scaling to html — anchors rem to the scaled size */
html {
  font-size: var(--size-font);
}

/* 2. Use rem for all sizing — font sizes, spacing, padding, gaps.
      To convert from Figma px values: value ÷ base = rem
      e.g. 48px heading with a 16px base → 48 ÷ 16 = 3rem
      e.g. 40px section gap            → 40 ÷ 16 = 2.5rem    */

/* 3. Container widths */
.container {
  max-width: var(--size-container);
}
.container.medium {
  max-width: calc(var(--size-container) * 0.85);
}
.container.small {
  max-width: calc(var(--size-container) * 0.7);
}
```

## Step 4: Styling guide

Share this with the user so they know how to style with the system:

---

### Styling with the fluid system

All sizing — font sizes, spacing, padding, gaps, border-radius — should be written
in `rem`. Because `html { font-size }` is set to the fluid value, `1rem` always
equals one unit of the scaled design. Never use `px` for sizing; it won't scale.

**Converting Figma values to rem:**

```
rem value = Figma px value ÷ base font size
```

| Figma value | Base | rem |
|---|---|---|
| 120px display | 16 | `7.5rem` |
| 64px headline | 16 | `4rem` |
| 32px subheading | 16 | `2rem` |
| 18px body | 16 | `1.125rem` |
| 13px caption | 16 | `0.8125rem` |
| 80px section gap | 16 | `5rem` |
| 8px border-radius | 16 | `0.5rem` |

**Why `rem` and not `em`:**
`rem` always anchors to `html`, so values never compound through nesting.
`em` is relative to the parent — a `1.2em` element inside another `1.2em`
element becomes `1.44em`, making it unpredictable for a system like this.

**The only time to use `px`:**
Borders and outlines (`border: 1px solid`) — these should stay fixed and
not scale with the viewport.

---

### Editorial type scale

Editorial design relies on a wide, expressive range of type sizes — from large
display headlines down to captions and labels. A strong scale creates visual
hierarchy without relying on colour or weight alone.

Suggest this as a starting point, adapting sizes from the user's Figma design:

```css
/* — Type scale — */
.text-display    { font-size: 7.5rem;    line-height: 0.95; letter-spacing: -0.03em; } /* 120px — hero/cover */
.text-headline   { font-size: 4rem;      line-height: 1.05; letter-spacing: -0.02em; } /* 64px  — section lead */
.text-title      { font-size: 2.5rem;    line-height: 1.1;  letter-spacing: -0.01em; } /* 40px  — article title */
.text-subheading { font-size: 1.5rem;    line-height: 1.3;  }                          /* 24px  — standfirst, intro */
.text-body       { font-size: 1.125rem;  line-height: 1.6;  }                          /* 18px  — body copy */
.text-meta       { font-size: 0.875rem;  line-height: 1.5;  letter-spacing: 0.04em;  } /* 14px  — byline, date, tags */
.text-caption    { font-size: 0.8125rem; line-height: 1.4;  }                          /* 13px  — image captions */
```

**Line-height guidance for editorial:**
- Display and headlines: tight (`0.9–1.1`) — large type needs less leading
- Body copy: open (`1.5–1.7`) — long-form reading needs room to breathe
- UI labels and meta: `1.3–1.5`

---

### Editorial layout patterns

These patterns cover the most common structural elements in editorial design.
All values are in `rem` and scale automatically with the system.

```css
/* Full-width article wrapper */
.article {
  max-width: var(--size-container);
  margin-inline: auto;
  padding-inline: 2.5rem;
}

/* Comfortable reading column — constrains line length for body text */
/* Ideal: 60–75 characters per line */
.article-body {
  max-width: 40rem;         /* ~640px at base — adjust to match your typeface */
  margin-inline: auto;
}

/* Wide breakout — for images, quotes, or data that exceed the text column */
.breakout {
  max-width: calc(var(--size-container) * 0.75);
  margin-inline: auto;
}

/* Full-bleed — stretches edge to edge, ignoring all column constraints */
.full-bleed {
  width: 100vw;
  margin-inline: calc(50% - 50vw);
}

/* Pull quote */
.pull-quote {
  font-size: 2rem;
  line-height: 1.2;
  letter-spacing: -0.01em;
  padding-block: 2.5rem;
  border-top: 1px solid;
  border-bottom: 1px solid;
  margin-block: 4rem;
}

/* Article section spacing rhythm */
.section        { padding-block: 5rem; }
.section--tight { padding-block: 2.5rem; }

/* Drop cap — first letter of an article */
.article-body p:first-of-type::first-letter {
  font-size: 4.5rem;
  line-height: 0.85;
  float: left;
  margin-right: 0.1em;
  font-weight: 700;
}
```

---

## Tips to share with the user

- The `✦` markers in the CSS show exactly what to update for a new project.
- To add a new breakpoint, duplicate a media query block and adjust `--size-design`,
  `--size-scale-min`, and `--size-scale-max`.
- `--size-scale-max` on desktop controls how large the layout gets on wide monitors.
  2560px covers most studio/large displays.
- The reading column width (`max-width: 40rem` on `.article-body`) is the single
  most important layout decision in editorial design — tune it to your typeface
  and body size until lines feel comfortable to read.
