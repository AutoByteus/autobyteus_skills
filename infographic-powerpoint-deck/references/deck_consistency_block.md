# Deck-level consistency blocks (reduce randomness across slides)

Legacy component library. Preferred flow is style-pack composition (`references/style-packs/`).
Use this file when manually selecting consistency rules.

Paste **one** block into every slide prompt. This acts like a “style lock” so the deck feels coherent across slides.

## Block 1 — Cinematic Keynote Lock

Paste this verbatim:

```text
This deck is one cohesive series (consistency rules are mandatory):
- Layout lock: the left frosted text panel occupies 58% of the canvas width (±2%); the right illustration zone occupies 42% (±2%). Keep the same corner radius, opacity style, position, and margins across all slides.
- Type lock: keep a fixed hierarchy for title, section headers, quotes, bullets, and footer. Comfortable leading. No tiny text on any slide.
- Light-direction lock: the main light direction stays fixed from upper-right to lower-left. Strong beams belong only in the right illustration zone, never across the left text panel.
- Rim-light lock: the right-side hero object uses the same gold rim-light intensity on every slide.
- Horizon / silhouette lock: keep the far-background silhouette band (city / harbor / wall / colonnade) at a consistent height in the lower 35%-45% of the frame, always low-contrast and softly blurred.
- Texture lock: apply the same ultra-low-contrast parchment-grain texture across the full deck at roughly 5%-10% strength.
- Icon lock: use a consistent thin-line icon style and consistent glow strength for checkmarks and dividers.
- Forbidden: no extra text, logos, watermarks, or random characters.
- Readability hard constraint: all text must stay sharp and high-contrast; the background must not interfere with the text panel.
```

## Block 2 — Movie Poster Epic Lock (stronger impact)

Paste this verbatim:

```text
This deck is a movie-poster-style series (consistency rules are mandatory):
- Layout lock: the left text panel occupies 55% of the frame (±2%); the right illustration zone occupies 45% (±2%). The text panel stays cleaner while the background is more narrative but still low-contrast.
- Key-light lock: use one diagonal primary light beam from upper-right toward center at the same angle on every slide. A slight vignette is allowed only when it improves focus.
- Landmark-silhouette lock: each slide includes the same class of far-background landmark silhouette (harbor / wall / colonnade / wilderness horizon) with consistent placement and blur.
- Gold-accent lock: each slide uses only 1-2 gold highlight points. All other gold elements stay as low-contrast fine lines.
- Grain and haze lock: keep stronger atmospheric depth separation, with cooler softer far backgrounds and slightly warmer foregrounds.
- Text hard constraint: do not sacrifice readability for poster drama. All required text must appear exactly.
- Forbidden: no extra text, logos, watermarks, or random characters.
```

## Block 3 — Editorial Light Lock (bright + relaxed)

Paste this verbatim:

```text
This deck is a bright editorial series (consistency rules are mandatory):
- Layout lock: the left light text card occupies 56% of the frame (±2%); the right illustration zone occupies 44% (±2%). Card shadows stay subtle and consistent.
- Brightness lock: keep overall medium-high brightness. Do not let large dark areas make the slide feel dim. No vignette.
- Lighting lock: rely on natural diffused light from a consistent upper-left or upper-right direction. No dramatic volumetric beams.
- Color lock: use light backgrounds (off-white / light gray / pale blue), dark gray-blue body text with strong contrast, and restrained accent colors.
- Texture lock: only very weak paper or fabric texture with low noise. No dirty grain or grunge.
- Icon lock: use consistent thin-line icons with matched corner radius and accent color treatment.
- Text hard constraint: readability is non-negotiable. All required text must appear exactly.
- Forbidden: no extra text, logos, watermarks, or random characters.
```

## How to use

- Add the chosen block under a `Series consistency lock` section in every slide prompt.
- Match the block with style pack from `references/style-pack-catalog.md`:
  - `cinematic-dark` → Block 1 or 2
  - `editorial-light` / `airy-relaxed` / `clean-corporate` → Block 3
- Combine with `references/motif_pack.md` (motifs) + `references/prompt_template.md` (structure).
