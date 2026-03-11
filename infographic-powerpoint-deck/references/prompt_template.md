# Prompt template: 16:9 rich-background infographic slide

Copy this template and fill in the bracketed parts. Keep it explicit and verbose; the model should not guess.

## 0) Output + hard constraints

- Output: a **single 16:9 widescreen PPT slide image** (flat image), no separate layers.
- Keep the generated image as the final artifact by default; no crop/pad/resize/post-processing unless user explicitly requests it.
- Prompt language: **English by default**.
- On-slide text language: **English by default** unless the user explicitly provides another language or requests a bilingual/multilingual slide.
- Ratio lock sentence must be present in each concrete prompt: `Hard canvas constraint: 16:9 widescreen. Do not generate a square image.`
- Must be **print-sharp** and readable; no tiny fonts.
- **No watermark, no logo, no random characters, and no unspecified text in any language.**
- **Do not add any text** beyond the `Must-appear text (verbatim)` section.
- If the required on-slide text is Chinese, German, or bilingual, keep the prompt instructions in English and paste the required text exactly as provided.
- Final delivery mode is one full slide image rendered by the image tools. Do not add text later with Python/PIL/PPT or any other non-image-tool overlay workflow.

## 0b) Tool-call ratio lock (required)

- When calling image generation, explicitly pass ratio config when supported (for example: `generation_config` includes `aspect_ratio: "16:9"`).
- If output still is not 16:9, regenerate the same slide with stricter ratio wording in prompt and ratio config in tool call.
- If deck consistency needs reinforcement, you may supply a previous approved slide or background exploration image as an input/edit reference. The image tool must still render the final full slide image.

## 1) Global style profile (required: select one style block first)

Use style-pack composition:
- Select `pack-id` from `references/style-pack-catalog.md`.
- Optional: list all packs using `python3 scripts/compose_style_pack_blocks.py --list`.
- Compose blocks from `references/style-packs/` using:
  - `python3 scripts/compose_style_pack_blocks.py --pack-id <id>`
- Paste the composed bundle here.
- If user does not specify style, default to `editorial-light`.

## 1b) Recurring motif pack (recommended, paste verbatim)

If you are not using style-pack composition, pick one motif pack from `references/motif_pack.md` and paste it here.

## 1c) Deck consistency lock (recommended, paste verbatim)

If you are not using style-pack composition, pick one lock block from `references/deck_consistency_block.md` and paste it here.

## 1d) Typography + fidelity locks (recommended, paste verbatim)

Paste these blocks verbatim:
- `references/typography_spacing_lock.md`
- `references/text_fidelity_block.md`
- `references/negative_prompt_block.md`

Optional (for stronger narrative): `references/storyboard_library.md`
Optional (for long Chinese passages): `references/chinese_quote_compression.md`

## 2) Slide-specific content (fill in)

### Title
- Title (exact): `[Slide title, including source range if relevant]`
- Scene ID (from `references/scene-catalog.md`): `[scene-id]`
  - Optional: select a ready preset from `references/scene-preset-library.md`.

### Must-appear text (verbatim)

Include **everything** that must appear on the slide, verbatim:
- `[Lead quote / anchor line 1]`
- `[Lead quote / anchor line 2]`
- `[Key point bullet 1]`
- `[Key point bullet 2]`
- `[Footer microcopy]`

Rules:
- If content comes from `deep-research-article/slide_extraction.md`, copy from `Must-appear text (verbatim)` first.
- Keep quote blocks short; if too long, split into 2 slides.
- If any character, word, accent, punctuation mark, or spacing is wrong in output, regenerate with stricter instruction: `All must-appear text must be exact. Do not rewrite. Do not add or remove punctuation or spaces.`
- For long Chinese passages, follow `references/chinese_quote_compression.md` (split, do not paraphrase).
- Do not translate the required text unless the user explicitly asks for translation.

### Layout rules

- Put title at top-left, large.
- Put the quote / insight / bullet sections inside the left text panel with clear section headers (accent color from selected style).
- Keep the right hero visual free of text.
- Maintain generous whitespace and alignment grid.

## 3) Visual scene (be concrete)

Describe visuals as a **scene** plus **infographic elements**:

- Far background (very low contrast): `[location + time: harbor at dawn / city wall in daylight / bright study interior / wilderness at sunrise]`
- Midground: `[main environment objects: wall, colonnade, waves, damaged boat, route line, scroll, stone path, crowd silhouettes]`
- Foreground hero (right side): `[core symbolic object: cross, ring, shield, mask, scale, scissors, chain, basket]`

Add 3–8 concrete objects/icons to reinforce meaning:
- `[Icon 1]` (e.g., thin-line icon + subtle glow)
- `[Icon 2]`

Depth + storytelling cues (optional but recommended):
- Camera feel: `[wide shot / medium shot]` with gentle depth-of-field.
- Atmosphere: `[clean daylight / soft haze / warm interior]` according to selected style pack.
- Motion hint: `[rope lowering basket / waves breaking / spotlight beam]` (implied, not literal animation).

## 4) Final checklist (paste)

- All specified `Must-appear text (verbatim)` content appears **exactly** in the requested language(s).
- No extra words, no watermark, no unspecified text in any language.
- Text is readable at presentation distance.
- Background is engaging but not busy.
- Deck style stays consistent with selected `pack-id` (no cross-style drift).
