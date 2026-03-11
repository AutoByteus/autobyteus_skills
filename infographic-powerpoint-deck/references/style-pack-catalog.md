# Style-pack catalog

Use this table to map user wording to one style pack ID.

| Pack ID | Positioning | Trigger wording (examples) | Default scene tags |
|---|---|---|---|
| `cinematic-dark` | Dramatic, epic, tense | cinematic, epic, tension, warning | `dramatic,night,high-contrast-symbol` |
| `editorial-light` | Bright, readable, balanced | bright, clear, shareable, not too dark | `daylight,clean,teaching` |
| `airy-relaxed` | Soft, calm, low-pressure | relaxed, fresh, gentle, healing | `airy,calm,pastel,open-space` |
| `clean-corporate` | Professional, report-like | corporate, training, briefing, professional | `corporate,minimal,diagram-friendly` |
| `warm-sermon` | Warm, pastoral, devotional | warm, pastoral, testimony, sermon, prayer gathering | `warm,heritage,pastoral,daylight` |
| `neo-tech` | Futuristic, AI/startup, dynamic | AI, technology, futuristic, startup, growth | `tech,futuristic,network,data` |
| `youth-social` | Vibrant, energetic, youth-oriented | youth, energetic, community, social, new-media | `vibrant,social,gradient,optimistic` |
| `research-academic` | Neutral, objective, analytical | research, academic, framework, methodology, evidence | `academic,neutral,structured,diagram` |

## Default choice

If user intent is unclear, pick `editorial-light`.

## Routing note

- If user says "not too dark" or "more relaxed", prefer `editorial-light` or `airy-relaxed`.
- If user asks for maximum cinematic impact, use `cinematic-dark`.
- If user needs meeting-room readability and structured delivery, use `clean-corporate`.
- If user wants warm pastoral sharing, use `warm-sermon`.
- If topic is AI/product/startup growth, use `neo-tech`.
- If audience is students/youth/community groups, use `youth-social`.
- If topic is research-heavy and evidence-driven, use `research-academic`.
