---
name: software-engineering-workflow-skill
description: "Create software-engineering planning artifacts with triaged depth: proposed-design-based runtime call stacks + runtime call stack review + implementation planning/progress for all sizes, plus proposed design docs for medium/large scope. Includes requirement clarification, call-stack validation, and iterative refinement."
---

# Software Engineering Workflow Skill

## Overview

Produce a structured planning workflow for software changes: triage scope, build proposed-design-based runtime call stacks per use case, verify those call stacks with a dedicated review artifact, and drive implementation with plan + real-time progress tracking. For medium/large scope, include a full proposed design document organized by separation of concerns.
This workflow is stage-gated. Do not batch-generate all artifacts by default.

## Workflow

### Ticket Folder Convention (Project-Local)

- For each task, create/use one ticket folder under the current project's `tickets/` directory.
- Folder naming: use a clear, short kebab-case name (no date prefix required).
- Write all task planning artifacts into that ticket folder.
- If the user specifies a different location, follow the user-specified path.

### Execution Model (Strict Stage Gates)

- Work in explicit stages and complete each gate before producing downstream artifacts.
- Do not finalize `implementation-plan.md` or generate `implementation-progress.md` until the runtime call stack review gate is fully satisfied for the current scope.
- `Small` scope exception: drafting `implementation-plan.md` (solution sketch only) before review is allowed as design input, but this draft does not unlock implementation kickoff.
- For `Medium/Large`, enforce at least 2 review rounds:
  - Round 1 is diagnostic/challenge by design and cannot unlock implementation.
  - Round 2 (or later) is the first round allowed to make a `Go` decision.
- Any review finding with a required design/call-stack update is blocking; regenerate affected artifacts and re-review before proceeding.
- If the user asks for all artifacts in one turn, still enforce stage gates within that turn (iterate review rounds first; only then produce implementation artifacts).

### 0) Triage Change Size First (Decide Workflow Depth)

- Do a quick requirement + codebase scan before choosing artifacts.
- Classify as `Small`, `Medium`, or `Large` using practical signals:
  - Estimated files touched (roughly <= 3 is usually `Small` if not cross-cutting).
  - New/changed public APIs, schema/storage changes, or cross-cutting behavior.
  - Multi-layer impact (API + service + persistence + runtime flow) or architectural impact.
- Choose workflow depth:
  - `Small`: create a draft implementation plan (with a short solution sketch), build per-use-case proposed-design-based runtime call stacks from that plan, review them, then refine until review-pass and track progress in real time.
  - `Medium/Large`: create proposed design doc first, build proposed-design-based runtime call stacks from the proposed design doc, run iterative review rounds (minimum 2), and only after final review `Go` create implementation plan and track progress in real time.
- Re-evaluate during implementation; if scope expands or smells appear, escalate from `Small` to full workflow.

### 1) Clarify Requirements And Scope

- Ask for goals, non-goals, primary use cases, and constraints.
- Confirm the triage result (`Small` vs `Medium/Large`) and why.
- If scope is ambiguous, ask whether to run medium/large depth (includes full proposed design doc). Otherwise proceed with the triaged depth.

### Core Modernization Policy (Mandatory)

- Mandatory stance: no backward compatibility and no legacy code retention.
- Do not preserve legacy behavior, legacy APIs, compatibility wrappers, dual-write paths, or fallback branches kept only for old flows.
- Prefer clean replacement and explicit deletion of obsolete code, files, tests, flags, and adapters in the same ticket.
- Do not add compatibility exceptions in this workflow.

### 2) Draft The Proposed Design Document

- Required for `Medium/Large`. Optional for `Small`.
- For `Small`, do not require a full proposed design doc; use the draft implementation plan solution sketch as the lightweight design basis for runtime call stacks.
- Follow separation of concerns: each file/module owns a clear responsibility.
- Make the proposed design doc delta-aware, not only target-state:
  - include current-state summary (as-is),
  - include target-state summary (to-be),
  - include explicit change inventory rows for `Add`, `Modify`, `Rename/Move`, `Remove`.
- List files/modules and their public APIs.
- For each file/module, state responsibility, key APIs, inputs/outputs, dependencies, and change type.
- Document dependency flow and cross-reference risk explicitly (including how cycles are avoided or temporarily tolerated).
- For `Rename/Move` and `Remove`, include decommission/cleanup intent (import cleanup and dead-code removal).
- Capture data models and error-handling expectations if relevant.
- Version the design during review loops (`v1`, `v2`, ...) and record what changed between rounds.
- Use the template in `assets/proposed-design-template.md` as a starting point.

### 3) Build Proposed-Design-Based Runtime Call Stacks Per Use Case

- Required for all sizes (`Small`, `Medium`, `Large`).
- For `Small`, keep it concise but still cover each in-scope use case with primary path plus key fallback/error branch when relevant.
- Basis by scope:
  - `Small`: use the draft implementation plan solution sketch as the design basis.
  - `Medium/Large`: use the proposed design document as the design basis.
- For each use case, write a proposed-design-based runtime call stack from entry point to completion in a debug-trace format.
- Include file and function names at every frame using `path/to/file.ts:functionName(...)`.
- Show architectural boundaries explicitly (e.g., controller -> service -> repository -> external API).
- Include primary path and fallback/error paths, not only happy path.
- Mark async/event boundaries (`await`, queue enqueue/dequeue, worker loop handoff).
- Mark state mutations and persistence points (`in-memory state`, `cache write`, `DB/file write`).
- Capture decision gates and conditions that choose one branch over another.
- Note key data transformations (input schema -> domain model -> output payload).
- Version call stacks to match design revisions from review loops (`v1`, `v2`, ...).
- Use the template in `assets/proposed-design-based-runtime-call-stack-template.md`.

### 4) Review Runtime Call Stacks (Gap + Cleanliness Gate)

- Create `runtime-call-stack-review.md` as a mandatory review artifact.
- Run review in explicit rounds and record each round in the same review artifact.
- Review each use case against these criteria:
  - business flow completeness (`Pass`/`Fail`),
  - gap findings,
  - structure and separation-of-concerns check (`Pass`/`Fail`),
  - dependency flow smells,
  - remove/decommission completeness for impacted changes (`Pass`/`Fail`),
  - no-legacy/no-backward-compat check (`Pass`/`Fail`),
  - overall verdict (`Pass`/`Fail`).
- Round policy:
  - `Small`: at least 1 round; iterate until gate passes.
  - `Medium/Large`: at least 2 rounds. Round 1 must be `No-Go` (diagnostic hardening round). Round 2+ may be `Go` only if all gate conditions pass.
- Gate `Go` criteria (all required):
  - all in-scope use cases have overall verdict `Pass`,
  - no unresolved blocking findings (including any required design/call-stack updates),
  - for any `Remove`/`Rename/Move` scope items, decommission/cleanup checks are `Pass`,
  - minimum required round count satisfied for the scope.
- If issues are found:
  - `Medium/Large`: revise the proposed design document, regenerate runtime call stacks, then rerun review.
  - `Small`: refine the implementation plan (and add design notes if needed), regenerate runtime call stacks, then rerun review.
- Repeat until all gate `Go` criteria are satisfied.
- Use the template in `assets/runtime-call-stack-review-template.md`.

### 5) Produce Implementation Plan And Progress Tracker

- Use a bottom-up, test-driven approach: implement foundational dependencies first.
- For each file/module, define unit tests and integration tests as needed.
- Finalize planning artifacts before kickoff:
  - `Small`: refine the draft implementation plan until runtime call stack review passes.
  - `Medium/Large`: create implementation plan only after runtime call stack review passes final gate and minimum review rounds are complete.
- Create the implementation progress document at implementation kickoff, after required pre-implementation artifacts are ready (including the proposed design document for Medium/Large).
- Implementation plan + real-time progress tracking are required for all sizes (`Small`, `Medium`, `Large`).
- Treat proposed-design-based runtime call stack + review as a pre-implementation verification gate: ensure each use case is represented and reviewed before coding starts.
- Start implementation only after the review gate says implementation can start and all in-scope use cases are `Pass`.
- Ensure traceability when a proposed design doc exists: every design change-inventory row (especially `Rename/Move` and `Remove`) maps to implementation tasks and verification steps.
- Enforce clean-cut implementation: do not keep legacy compatibility paths.
- Use "one file at a time" as the default execution strategy, not an absolute rule.
- When rare cross-referencing is unavoidable, allow limited parallel/incomplete implementation, but explicitly record:
  - the cross-reference smell,
  - the blocked dependency edge,
  - the condition to unblock,
  - the required proposed-design-document update.
- Update progress in real time during implementation (immediately after file status changes, test runs, blocker discoveries, and design-feedback-loop updates).
- Track change IDs and change types in progress (`Add`/`Modify`/`Rename/Move`/`Remove`) so refactor deltas remain explicit through execution.
- Track file build state explicitly (`Pending`, `In Progress`, `Blocked`, `Completed`, `N/A`).
- Track unit/integration test state separately (`Not Started`, `In Progress`, `Passed`, `Failed`, `Blocked`, `N/A`).
- If a file is blocked by unfinished dependencies, mark it `Blocked` and record the dependency and unblock condition.
- Mark a file `Completed` only when implementation is done and required tests are passing.
- Use `assets/implementation-plan-template.md` and `assets/implementation-progress-template.md`.

## Output Defaults

If the user does not specify file paths, write to a project-local ticket folder in stage order:

- Stage 1 (design basis):
  - `Small`: start/refine `tickets/<ticket-name>/implementation-plan.md` (solution sketch section only for design basis).
  - `Medium/Large`: create/refine `tickets/<ticket-name>/proposed-design.md`.
- Stage 2 (runtime modeling):
  - `tickets/<ticket-name>/proposed-design-based-runtime-call-stack.md`
- Stage 3 (review gate, iterative):
  - `tickets/<ticket-name>/runtime-call-stack-review.md`
- Stage 4 (only after gate `Go`):
  - finalize/update `tickets/<ticket-name>/implementation-plan.md`
  - `tickets/<ticket-name>/implementation-progress.md`

## Templates

- `assets/proposed-design-template.md`
- `assets/proposed-design-based-runtime-call-stack-template.md`
- `assets/runtime-call-stack-review-template.md`
- `assets/implementation-plan-template.md`
- `assets/implementation-progress-template.md`
