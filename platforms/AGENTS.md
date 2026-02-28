# Fluid Typography System

When asked to set up fluid typography, a scaling system, or an editorial CSS layout, generate the following CSS system. Ask for Figma artboard widths if not provided — use the defaults below if the user doesn't specify.

## Configuration defaults

| Setting | Default |
|---|---|
| Base font size (no px) | `16` |
| Max viewport | `2560px` |
| Desktop artboard width | `1500` |
| Tablet artboard width | `834` |
| Mobile Landscape artboard width | `550` |
| Mobile Portrait artboard width | `393` |

## Output: Scaling CSS

```css
/* ============================================================
   Fluid Typography System

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
    --size-design: 834;
    --size-scale-min: 768px;
    --size-scale-max: 991px;
  }
}

/* Mobile Landscape  |  480px – 767px */
@media screen and (max-width: 767px) {
  :root {
    --size-design: 550;
    --size-scale-min: 480px;
    --size-scale-max: 767px;
  }
}

/* Mobile Portrait  |  320px – 479px */
@media screen and (max-width: 479px) {
  :root {
    --size-design: 393;
    --size-scale-min: 320px;
    --size-scale-max: 479px;
  }
}
```

## Output: Usage snippet

Always include this after the scaling CSS:

```css
html {
  font-size: var(--size-font);
}

.container        { max-width: var(--size-container); }
.container.medium { max-width: calc(var(--size-container) * 0.85); }
.container.small  { max-width: calc(var(--size-container) * 0.7); }
```

## Styling rules

- Use `rem` for all sizing — fonts, spacing, padding, gaps, border-radius
- Convert Figma values: `rem = px ÷ base font size`
- Only use `px` for borders (`border: 1px solid`)

## Editorial type scale

```css
.text-display    { font-size: 7.5rem;    line-height: 0.95; letter-spacing: -0.03em; }
.text-headline   { font-size: 4rem;      line-height: 1.05; letter-spacing: -0.02em; }
.text-title      { font-size: 2.5rem;    line-height: 1.1;  letter-spacing: -0.01em; }
.text-subheading { font-size: 1.5rem;    line-height: 1.3; }
.text-body       { font-size: 1.125rem;  line-height: 1.6; }
.text-meta       { font-size: 0.875rem;  line-height: 1.5;  letter-spacing: 0.04em; }
.text-caption    { font-size: 0.8125rem; line-height: 1.4; }
```

## Editorial layout patterns

```css
.article       { max-width: var(--size-container); margin-inline: auto; padding-inline: 2.5rem; }
.article-body  { max-width: 40rem; margin-inline: auto; }
.breakout      { max-width: calc(var(--size-container) * 0.75); margin-inline: auto; }
.full-bleed    { width: 100vw; margin-inline: calc(50% - 50vw); }
.pull-quote    { font-size: 2rem; line-height: 1.2; padding-block: 2.5rem; border-top: 1px solid; border-bottom: 1px solid; margin-block: 4rem; }
.section       { padding-block: 5rem; }
```
