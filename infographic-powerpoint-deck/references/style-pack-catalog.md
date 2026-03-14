# Style-pack catalog

Use this table to map user wording or inferred deck archetype to one style pack ID.
Style pack selects mood and visual language. Layout is a separate per-slide decision, normally auto-routed by the skill using `references/layout_routing_policy.md`.

| Pack ID | Positioning | Common layout fits | Trigger wording (examples) | Default scene tags |
|---|---|---|---|---|
| `cinematic-dark` | Dramatic, epic, tense | `L4`, `L5`, `L6`, `L8`, sometimes `L1` | cinematic, epic, tension, warning | `dramatic,night,high-contrast-symbol` |
| `cinematic-light` | Filmic, bright, uplifting | `L4`, `L5`, `L6`, `L1` | bright cinematic, hopeful cinematic, cinematic daylight, not dark | `cinematic,daylight,hopeful,open-space` |
| `cinematic-editorial` | Premium, polished, magazine-like | `L4`, `L5`, `L6`, `L1`, `L7` | cinematic editorial, premium keynote, campaign film, cover-story | `cinematic,editorial,architectural,refined` |
| `illustrative-cinematic` | Immersive illustrated teaching, polished and scene-rich | `L4`, `L5`, `L6`, `L9`, `L10`, `L11`, `L1` | illustrative cinematic, scene-rich explainer, immersive teaching, polished illustration, not sketchy | `illustrative,cinematic,daylight,architectural` |
| `editorial-light` | Bright, readable, balanced | `L4`, `L5`, `L6`, `L1`, `L2`, `L9`, `L10`, `L11` | bright, clear, shareable, not too dark | `daylight,clean,teaching` |
| `airy-relaxed` | Soft, calm, low-pressure | `L4`, `L5`, `L6`, `L1` | relaxed, fresh, gentle, healing | `airy,calm,pastel,open-space` |
| `clean-corporate` | Professional, report-like | `L1`, `L2`, `L7`, `L9`, `L10`, `L11`, `L6` | corporate, training, briefing, professional | `corporate,minimal,diagram-friendly` |
| `animated-feature-bright` | Stylized 3D family-animation energy | `L4`, `L5`, `L6`, `L1` | animated feature, family animation, stylized 3D, character-led | `animated,bright,character,optimistic` |
| `warm-sermon` | Warm, pastoral, devotional | `L4`, `L5`, `L6`, `L1` | warm, pastoral, testimony, sermon, prayer gathering | `warm,heritage,pastoral,daylight` |
| `neo-tech` | Futuristic, AI/startup, dynamic | `L2`, `L6`, `L7`, `L1` | AI, technology, futuristic, startup, growth | `tech,futuristic,network,data` |
| `youth-social` | Vibrant, energetic, youth-oriented | `L4`, `L5`, `L6`, `L7`, `L1` | youth, energetic, community, social, new-media | `vibrant,social,gradient,optimistic` |
| `research-academic` | Neutral, objective, analytical | `L1`, `L2`, `L3`, `L7`, `L9`, `L10`, `L11` | research, academic, framework, methodology, evidence | `academic,neutral,structured,diagram` |
| `whiteboard-sketch` | Hand-drawn, diagram-led, technical teaching | `L9`, `L10`, `L11`, sometimes `L7` or `L1` | whiteboard, sketch, doodle, hand-drawn, visual notes, technical explainer | `bright,sketch,diagram,teaching` |

## Default choice

If user intent and inferred archetype are both unclear, pick `editorial-light`.

## Routing note

- When the user provides raw article content, prefer choosing style through `references/deck_archetype_routing.md` first, then use this catalog to pick the concrete pack.
- Style pack and layout are orthogonal: choose the pack for mood, then let the skill auto-route `L1`–`L11` for each slide based on text budget and slide role unless the user explicitly overrides it.
- The `Common layout fits` column is descriptive, not a fixed order that overrides routing policy.
- Keep one pack across the deck by default, but vary layouts slide by slide when that improves readability and pacing.
- For `cinematic-light`, `cinematic-editorial`, `cinematic-dark`, `editorial-light`, `airy-relaxed`, `warm-sermon`, `animated-feature-bright`, and `youth-social`, use a direct-overlay-first bias unless text density or structure clearly requires a split-panel layout.
- If user says "not too dark" or "more relaxed", prefer `editorial-light` or `airy-relaxed`.
- If user asks for maximum cinematic impact, use `cinematic-dark`.
- If user asks for cinematic but bright, hopeful, or daylight-driven, use `cinematic-light`.
- If user asks for a premium keynote, campaign-film, or cover-story feel, use `cinematic-editorial`.
- If user wants an immersive illustrated deck with meaningful teaching density, rich background atmosphere, and polished non-sketch diagrams, use `illustrative-cinematic`.
- If user needs meeting-room readability and structured delivery, use `clean-corporate`.
- If user asks for Disney/Pixar-like energy, route to `animated-feature-bright` and rewrite the prompt with non-branded descriptors such as `stylized 3D family animated feature`, `expressive character-led composition`, and `soft cinematic global illumination`.
- If user wants warm pastoral sharing, use `warm-sermon`.
- If topic is AI/product/startup growth, use `neo-tech`.
- If audience is students/youth/community groups, use `youth-social`.
- If topic is research-heavy and evidence-driven, use `research-academic`.
- If the user wants a hand-drawn explainer, whiteboard feel, doodle-style teaching board, or technical sketch-note deck, use `whiteboard-sketch`.
- For `whiteboard-sketch`, do not force every section into a visible card. Prefer implied zones, curved arrows, floating modules, thin separators, and a strong reading path.
- If the user wants classroom, lecture, textbook-like, reaction-scheme, or self-contained didactic explainer slides, prefer `research-academic`, `editorial-light`, `clean-corporate`, or `illustrative-cinematic` and bias the layout system toward `L9`, `L10`, or `L11`.
