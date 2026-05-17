# Dove — logo image-generation prompt

The Dove logo is **one mark**, used across all three sister repositories (dove-edu, dove-health, dove-hire). Vertical-specific lockups append a thin sub-mark (e.g. `Dove · edu`) but the symbol itself does not change.

Render externally (Midjourney, DALL·E, GPT-image, Figma + AI). Save the rendered outputs into each consuming repo's `brand/` folder — *not* into this org repo (`.gitignore` excludes `brand/renders/` here).

## Design intent

The mark must communicate **three things at once**:

1. **A dove** — the bird, in profile, taking off or in mid-flight. Not a peace dove with an olive branch (too political, too saccharine). Not a heraldic dove (too ornate). A working dove: a carrier-pigeon-as-witness, calm but in motion, carrying something the recipient is entitled to receive. The mid-flight pose signals *delivery of evidence*, which is what the agent does.

2. **An audit seal** — a thin ring or wreath element behind / around / over the dove that reads as a checked seal, a signature glyph, or a stamped attestation. This is what distinguishes Dove from a generic peace-dove brand. It must read as "the bird carries provenance," not "the bird represents peace."

3. **A negative-space hint of two figures or two profiles** — the dual-audience commitment. Optional, only if it can be done subtly inside the seal ring or in the dove's silhouette without making the mark busy. If the negative-space figures fight the rest of the mark, drop them — the dove + seal is the primary read.

The mark must work as a 16×16 favicon, a 64×64 GitHub avatar, a 256×256 PyPI thumbnail, and at print scale on an A4 paper. It must read in pure black at favicon scale (no internal detail finer than 1px at 16×16).

## Palette

Use exclusively the Dove brand palette (see [colors.md](colors.md)):

- **Imperial Green** `#004B3C` — the dove body / primary fill
- **Marble White** `#FAF9F6` — background canvas (the mark is also rendered against a transparent background for use over non-white surfaces)
- **Deep Slate** `#1F2933` — fine outline if any (typically the seal ring or wreath)
- **Mist Sage** `#D6E2DA` — optional 5%-of-canvas accent (a soft glow behind the dove; do NOT use as a fill on the dove itself)

Do **not** use Steel Silver in the logo (reserved for UI structure, not brand mark). Do **not** use any forbidden tone from `colors.md` (Radiant Gold, Sunlit Wheat, pure black, institutional blue).

## Typography in the logo

Two variants:

**Symbol-only variant** — just the dove + seal, no wordmark. Used as favicon, GitHub avatar, PyPI thumbnail, and as the small ☉ inside dual-audience figures across all Dove papers.

**Wordmark variant** — symbol on the left, the word **Dove** to the right in **Fraunces** (the brand headline face, see colors.md). Imperial Green for the wordmark; weight semi-bold; tracking slightly open. The wordmark sits on the dove's optical baseline, not the descender line.

A vertical-specific lockup appends a thin separator and the vertical name in Satoshi small caps:

```
[symbol] Dove  ·  edu
[symbol] Dove  ·  health
[symbol] Dove  ·  hire
```

The separator (·) and the vertical name are in Deep Slate, not Imperial Green — they must read as secondary to the brand mark.

---

## Generator prompt — symbol-only variant

```
Generate a square minimalist vector LOGO MARK for an open-source AI agent
project called "Dove", on a transparent / pure white background. The
finished output must read at 16x16 favicon size as well as at 1024x1024
print size, and must read in pure black at favicon scale.

THE MARK is a stylised DOVE in profile, mid-flight or taking off, head
forward, wings spread asymmetrically (one wing further extended, the
other tucked — captures motion). The dove is filled in solid Imperial
Green #004B3C with NO internal feather detail visible at 16x16. At
larger sizes, a single thin Deep Slate #1F2933 line may suggest the
wing edge, but only one such line — never multiple feathers.

SURROUNDING the dove on three sides (top-left, top-right, bottom), a
THIN broken circle outline in Deep Slate #1F2933, reading as a stamped
audit seal or signature ring. The ring is INCOMPLETE — broken at the
top where the dove's beak or head crosses it, so the dove appears to be
flying OUT of the seal (delivering the evidence). The ring's stroke
weight is 1/30th of the canvas height (visible at the 64x64 GitHub
avatar size, hairline-but-present at favicon).

A SOFT Mist Sage #D6E2DA glow occupies the lower-third behind the dove,
suggesting a horizon or an audit-trail surface. The glow has no hard
edge — it fades smoothly to white over ~20% of the canvas. Do NOT use
the glow if it makes the mark busy at favicon scale; in that case render
without the glow.

NEGATIVE SPACE inside the seal ring, optional: if it can be done WITHOUT
adding visual noise, the dove's silhouette may suggest TWO subtle
profiles facing each other (one on each side of the dove's body — the
"two audiences" the agent serves). This is a stretch goal; if it fights
the primary read of the dove + seal, OMIT it.

STRICT NEGATIVE INSTRUCTIONS:
- Do NOT add an olive branch in the dove's beak. This is not a peace
  dove. The dove is a carrier of evidence, not a symbol of peace.
- Do NOT add a halo, crown, wings of fire, or any ornate flourish. The
  mark is clinical-calm, not religious or heraldic.
- Do NOT render the word "Dove" inside the mark. The wordmark is a
  separate variant.
- Do NOT use Radiant Gold (#D4AF37), Sunlit Wheat (#F9E79F), pure
  black (#000000), institutional blue, or saturated red anywhere.
- Do NOT add a watermark, signature, or "AI-generated" tag.
- Do NOT use a circle background (no gradient circle behind the mark).
- Do NOT add the dove's eye if it would render as a single black dot
  at favicon size — at that scale the eye becomes a smudge.

Style: flat vector, two colours plus optional sage glow, generous
whitespace around the mark (10% padding minimum on each side), no
photo-realism, no 3D rendering, no shadow under the dove.
```

## Generator prompt — wordmark variant

```
Generate a horizontal LOCKUP for an open-source AI agent project called
"Dove", on a transparent / pure white background. The lockup is the
symbol-only Dove mark (described above — Imperial Green dove in profile
mid-flight, broken Deep Slate audit-seal ring, optional Mist Sage glow)
on the LEFT, with the word "Dove" set in Fraunces semi-bold to the RIGHT
of the symbol.

The wordmark "Dove" is in Imperial Green #004B3C, with semi-bold weight,
slightly open tracking (~+15), and a height that matches the optical
height of the dove SYMBOL (not the seal ring height). The wordmark sits
on the dove's optical baseline, not on its descender line.

Symbol padding from wordmark: equal to one cap height. Symbol padding
from left canvas edge: equal to half a cap height. Wordmark padding from
right canvas edge: equal to one cap height.

NO descriptor text beneath the wordmark in this variant. The vertical-
specific lockups ("Dove · edu", "Dove · health", "Dove · hire") are a
SEPARATE variant — they append a Deep Slate middot and the vertical name
in Satoshi small caps, with the same padding and baseline rules.

STRICT NEGATIVE INSTRUCTIONS:
- Do NOT use any colour outside the Dove palette (Imperial Green
  #004B3C, Marble White #FAF9F6, Deep Slate #1F2933, Mist Sage #D6E2DA).
- Do NOT stack the wordmark above or below the symbol (this is a
  HORIZONTAL lockup; the stacked variant is a separate render request).
- Do NOT add a tagline beneath the wordmark.
- Do NOT use any face other than Fraunces semi-bold for the wordmark.
- Do NOT render the wordmark in italics.

Style: flat vector, brand-mark-clean, generous whitespace, no shadow,
no 3D, no AI-generated watermark.
```

## Generator prompt — vertical lockup variant (one prompt per vertical)

```
Generate a horizontal LOCKUP for the open-source AI agent project
"Dove · edu" (or "Dove · health" or "Dove · hire" — adjust per render),
on a transparent / pure white background. Layout: the Dove symbol on
the left, then the word "Dove" in Fraunces semi-bold Imperial Green
#004B3C, then a thin Deep Slate middot ("·"), then the vertical name
("edu" or "health" or "hire") in Satoshi small-caps Deep Slate #1F2933.

The vertical name height matches the cap height of the Dove wordmark
(NOT taller). The middot is vertically centred on the dove wordmark's
x-height. Spacing between Dove / middot / vertical name is one
half-cap-height on each side of the middot.

Padding rules and negatives are identical to the wordmark variant.

The three vertical names that should be supported (one render per name):
"edu", "health", "hire". Spell the vertical name in lower case.
```

## Render checklist

After generating:

1. Save the symbol-only variant as `brand/renders/dove-mark.svg` (vector,
   transparent) in **each** of dove-edu / dove-health / dove-hire when
   those repos exist. Also save a `dove-mark-256.png` and
   `dove-mark-favicon.ico` for web use.
2. Save the wordmark variant as `brand/renders/dove-wordmark.svg`.
3. Save each vertical lockup as `brand/renders/dove-edu-lockup.svg`,
   `brand/renders/dove-health-lockup.svg`, `brand/renders/dove-hire-lockup.svg`.
4. Use `dove-mark-favicon.ico` as the favicon in every frontend repo's
   `index.html`.
5. Use the wordmark in the GitHub README header for each Dove repo
   (replacing the current `# dove-edu-backend` text title).
6. Use the vertical lockup as the cover image for the corresponding
   academic paper's title page (IJAIED, npj Digital Medicine, ICIS).

## Notes

- The mark is **not** registered as a trademark. The README of this org
  repo records the open-question on the "Dove" name; before
  commercialising or registering, run the trademark-search step
  described there.
- The symbol's mid-flight pose is a deliberate departure from the more
  static peace-dove convention because Dove is an *active* agent (the
  bird is delivering evidence), not a passive symbol.
- The broken audit-seal ring is the single most important brand-
  differentiating element. If a render does the dove well but the ring
  is closed (intact) or absent, reject that render and regenerate.
