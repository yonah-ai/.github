# Dove — brand palette

The Dove palette is adapted from [Vorrai's clinical palette](https://github.com/jhcontext/vendia-models/blob/main/vendia_models/dtos/tenant/config/full/vorrai.yaml) (the same author, the same calm-clinical-authority register), with two changes: (a) the gold accent that Vorrai dropped is absent here too — replaced by Mist Sage as the secondary; (b) one palette is used across all three Doves (edu, health, hire) so the family reads as a family. There is no per-vertical re-skin.

The full palette is intentionally small: **two anchor colours** (Imperial Green + Marble White), **two text colours** (Deep Slate for body, Steel Silver for secondary), and **one accent** (Mist Sage). Every figure, frontend, and brand surface across all Dove repositories uses exactly these five — anything more and the family loses coherence in print and at small sizes.

## Core anchors

### Imperial Green — `#004B3C`

The single colour the eye should remember. Deep, restorative, restrained. Anchors the brand mark, primary CTAs (Marble White text), headlines on light surfaces, and the gold-equivalent role in all figure work. Reads as calm authority — not institutional blue, not luxury-cosmetic gold, not surveillance black. WCAG AAA contrast against Marble White; WCAG AA against Steel Silver.

Use for: brand mark fill, primary CTA fill, large headline text on Marble White, the "shared contract" element in every dual-audience diagram (the rubric pill in dove-edu, the clinical protocol pill in dove-health, the criteria pill in dove-hire), the audit-seal icon on signed envelopes.

### Marble White — `#FAF9F6`

Off-white canvas. Soft enough to settle the eye on long-read documentation; clean enough to print without grey cast. The dominant tone across every page, dashboard, and figure background.

Use for: page backgrounds, card backgrounds, primary CTA text on Imperial Green, the canvas of every figure and logo render.

## Text

### Deep Slate — `#1F2933`

The body-text colour. Replaces pure black — gives WCAG AAA contrast on Marble White without the harshness of `#000000`. Used everywhere text appears on a light surface.

Use for: body text, captions, table cells, code identifiers in dark style, the structural outlines in dual-audience figures (the "professor" pill fill).

### Steel Silver — `#BCC6CC`

Secondary structure. Dividers, disabled states, secondary captions. Avoid for any authority-bearing copy — those promote to Deep Slate.

Use for: card dividers, table rules, disabled-button fill, "metadata" captions (timestamps, version stamps), the secondary outlines on agent boxes in figure work.

## Accent

### Mist Sage — `#D6E2DA`

The 5%-of-surface accent. Pale, desaturated, complements Imperial Green. Carries the role that the dropped Radiant Gold used to play in Vorrai — and is the same colour across all three Doves because the sage register works for education (warm), for clinical (calming), and for hiring (neutral-professional) without re-skin.

Use for: primary-CTA hover surface, card-hover surfaces, success-state backgrounds, the "student" pill fill in dual-audience figures, the secondary background on substrate strips in architecture diagrams.

## Forbidden tones (do not reintroduce in any new Dove work)

| Tone | Hex | Why dropped |
|---|---|---|
| Radiant Gold | `#D4AF37` | Reads as luxury-cosmetic in the Vorrai lineage; reads as financial-services in the Dove lineage. Imperial Green is the only metallic-feeling accent. |
| Sunlit Wheat | `#F9E79F` | Reads as wellness/spa. Disappears on Marble White. |
| Pure black | `#000000` | Too harsh on white in print; Deep Slate replaces it everywhere. |
| Saturated red | any | Reserved for error states only, never decorative. |
| Institutional blue (Bootstrap-blue, Material-blue) | — | The medical-software default; Imperial Green deliberately rejects it. |

## Typography

Same stack as Vorrai. Standardised across all Dove surfaces.

| Role | Family | Fallback |
|---|---|---|
| Headlines | Fraunces | Playfair Display, Georgia, "Times New Roman", serif |
| Body | Satoshi | Inter, Montserrat, system-ui, -apple-system, sans-serif |
| Accent (sparingly — pull quotes, italicised emphasis in figures) | Cormorant Garamond | Georgia, "Times New Roman", serif |
| Code / identifiers | JetBrains Mono | "Fira Code", Menlo, Consolas, monospace |

WCAG AA minimum for all body text; AAA where the contrast pairing permits (Deep Slate on Marble White does pass AAA).

## Figures in academic papers

For figures in the IJAIED / npj Digital Medicine / ICIS papers, an alternative figure-only palette is used because journal print constraints favour higher-contrast pill borders and gold/dark-navy combinations that survive B&W photocopy. That palette is documented separately in each paper repo's `figures/image_prompts.md` ([dove-edu paper figures](https://github.com/jhcontext/jhcontext-papers/blob/main/ijaied/figures/image_prompts.md)). The web/UI palette (this document) and the figures palette are deliberately distinct — neither dominates the other.

## Quick reference

```css
:root {
  /* Anchors */
  --color-imperial-green: #004B3C;
  --color-marble-white:   #FAF9F6;

  /* Text */
  --color-deep-slate:     #1F2933;
  --color-steel-silver:   #BCC6CC;

  /* Accent */
  --color-mist-sage:      #D6E2DA;
}
```

## Provenance

This palette was finalised on 2026-05-17 by adapting the Vorrai clinical palette (which dropped Radiant Gold the same week) to the Dove family. It is intentionally narrow; expanding it requires a council review on this repo.
