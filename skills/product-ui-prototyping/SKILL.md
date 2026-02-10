---
name: product-ui-prototyping
description: "Design and validate product UI behavior as visual state prototypes before coding. Use when tasks ask how screens should change after user actions (click, tap, submit), when non-developers need to review web/mobile UX flows, or when teams need interaction-state assets and acceptance checks for implementation."
---

# Product UI Prototyping

## Overview

Turn product ideas into testable UI behavior using generated and edited screen images. Produce state-by-state visuals, click-through transition logic, and a lightweight behavior test matrix that product, design, and engineering can review before implementation.

## Prototype Folder Convention (Project-Local)

- For each prototype effort, create/use one folder under the current project's `ui-prototypes/` directory:
  - `ui-prototypes/<prototype-name>/`
- Keep all prototype artifacts in that folder so each prototype remains self-contained.
- Use clear kebab-case for `<prototype-name>`.
- Keep image assets separated by platform:
  - `ui-prototypes/<prototype-name>/images/web/<flow>/...`
  - `ui-prototypes/<prototype-name>/images/ios/<flow>/...`
  - `ui-prototypes/<prototype-name>/images/android/<flow>/...`
- If the user specifies a different location, follow the user-specified path.

## Workflow

### 1) Define Product Intent And Constraints

- Define target platform (`web`, `ios`, `android`) and viewport assumptions.
- Define user personas, primary jobs-to-be-done, and critical paths.
- Define design constraints: brand tone, accessibility needs, component style, and data density.
- Define fidelity level (`wireframe`, `mid`, `high`) before generating assets.
- Define whether each flow is state-only or click-through simulation.

### 2) Map Screens, Actions, And States

- Create a state transition table for each flow:
  - `screen`
  - `trigger` (click/tap/submit/navigation/system event)
  - `from_state`
  - `to_state`
  - `expected_feedback` (visual + microcopy)
- Cover at minimum: `default`, `focus`, `pressed`, `disabled`, `loading`, `success`, `error`, and `empty` where applicable.
- Prioritize one critical flow first, then expand to secondary flows.

### 3) Create One Canonical Product Base Spec

- Build one reusable `product_base_spec` (platform, viewport, typography, spacing, tokens, accessibility intent).
- Reuse the same base spec in all generate/edit prompts to prevent style drift between screens.

### 4) Generate Baseline Screens

- Generate net-new screens with the image generation tool.
- Use deterministic style instructions and the shared base spec to keep typography, spacing, iconography, and color consistent across screens.
- Save outputs in a stable structure:
  - `ui-prototypes/<prototype-name>/images/<platform>/<flow>/<screen>-default.png`

### 5) Edit Interaction States From Baselines

- Derive state variants with the image editing tool so layout and visual identity remain stable.
- Edit only state-relevant deltas:
  - Hover/focus rings
  - Pressed depth
  - Disabled contrast
  - Loading affordance
  - Validation/success/error messages
- Save outputs as:
  - `ui-prototypes/<prototype-name>/images/<platform>/<flow>/<screen>-<state>.png`

### 6) Connect Screens For Click-Through Simulation

- For click-through flows, create `ui-prototypes/<prototype-name>/ui-flow-map.json` to connect images by trigger.
- Include per-link definitions:
  - `screen`
  - `trigger`
  - `hotspot` (`x`, `y`, `width`, `height`)
  - `target_screen`
  - `transition` (`instant`, `fade`, `slide`)
- Keep hotspot naming deterministic so non-developers can review and iterate quickly.

### 7) Assemble Behavior Test Matrix

- Produce `ui-prototypes/<prototype-name>/ui-behavior-test-matrix.md` with one row per transition.
- Include:
  - `flow`
  - `screen`
  - `trigger`
  - `expected next state image`
  - `acceptance check`
  - `open question / risk`
- Mark blocking issues where any trigger has ambiguous or missing feedback.

### 8) Deliver Review Package For Non-Developers

- Produce a concise review packet:
  - `ui-prototypes/<prototype-name>/ui-prototype-spec.md` with assumptions, flow summary, and behavior rules
  - `ui-prototypes/<prototype-name>/ui-flow-map.json` for click-through linkage
  - `ui-prototypes/<prototype-name>/viewer/` local click-through viewer files
  - Image gallery links grouped by flow and platform
  - Explicit unresolved decisions for product/design sign-off
- Keep wording product-facing and avoid implementation jargon when possible.

### 9) Publish Local Click-Through Viewer

- Copy the viewer template from `assets/prototype-viewer/` into `ui-prototypes/<prototype-name>/viewer/`.
- Keep viewer default config pointing to `../ui-flow-map.json`.
- Serve the workspace root locally and open:
  - `http://localhost:4173/ui-prototypes/<prototype-name>/viewer/index.html`
- Use this viewer for product/design review so non-developers can click through flows.

## Prompt Patterns And Checklists

- Read and reuse `references/prompt-patterns.md` for:
  - UX criteria coverage and product base spec
  - Production screen generation and state edit templates
  - Flow-step and cross-platform adaptation templates
  - Click-through flow map template, viewer compatibility rules, and acceptance checklist

## Default Outputs

- `ui-prototypes/<prototype-name>/ui-prototype-spec.md`
- `ui-prototypes/<prototype-name>/ui-behavior-test-matrix.md`
- `ui-prototypes/<prototype-name>/ui-flow-map.json` (required for click-through simulation)
- `ui-prototypes/<prototype-name>/viewer/index.html`
- `ui-prototypes/<prototype-name>/viewer/viewer.css`
- `ui-prototypes/<prototype-name>/viewer/viewer.js`
- `ui-prototypes/<prototype-name>/images/web/<flow>/*.png`
- `ui-prototypes/<prototype-name>/images/ios/<flow>/*.png`
- `ui-prototypes/<prototype-name>/images/android/<flow>/*.png`

## Quality Gate

- Ensure every critical trigger produces clear, visible feedback within one state transition.
- Ensure states are visually consistent across platforms and flows.
- Ensure error and empty states include recovery guidance.
- Ensure accessibility cues (focus visibility, contrast intent, readable hierarchy) are represented in mockups.
- Ensure each click-through trigger in the flow map points to a valid target screen.
- Ensure viewer navigation works for each clickable hotspot and start screen.

## Handoff

- Hand off approved behavior specs and state assets to implementation.
- If engineering planning is requested next, invoke `$software-engineering-workflow-skill` with `ui-prototypes/<prototype-name>/ui-prototype-spec.md`, `ui-prototypes/<prototype-name>/ui-behavior-test-matrix.md`, `ui-prototypes/<prototype-name>/ui-flow-map.json`, and viewer behavior notes as inputs.
