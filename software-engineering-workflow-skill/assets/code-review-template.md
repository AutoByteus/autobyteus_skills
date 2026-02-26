# Code Review

Use this document for `Stage 8` code review after Stage 7 API/E2E testing passes.
This gate enforces structure quality, source-file maintainability, and mandatory re-entry rules.

## Review Meta

- Ticket:
- Review Round:
- Trigger Stage: `7` / `Re-entry`
- Workflow state source: `tickets/in-progress/<ticket-name>/workflow-state.md`
- Design basis artifact:
- Runtime call stack artifact:

## Scope

- Files reviewed (source + tests):
- Why these files:

## Source File Size And SoC Audit (Mandatory)

| File | Effective Non-Empty Line Count | Adds/Expands Functionality (`Yes`/`No`) | `501-700` SoC Assessment | `>700` Hard Check | `>220` Changed-Line Delta Gate | Preliminary Classification (`N/A`/`Local Fix`/`Design Impact`/`Requirement Gap`/`Unclear`) | Required Action (`Keep`/`Split`/`Move`/`Refactor`) |
| --- | --- | --- | --- | --- | --- | --- | --- |
|  |  |  | Pass/Fail/N/A | Pass/Fail/N/A | Pass/Fail/N/A |  |  |

Rules:
- Use explicit measurement commands per changed source file:
  - effective non-empty line count: `rg -n "\\S" <file-path> | wc -l`
  - changed-line delta: `git diff --numstat <base-ref>...HEAD -- <file-path>`
- Enforcement baseline uses effective non-empty line count.
- For effective non-empty line count `<=500`, normal review applies (`501-700` and `>700` checks can be `N/A`).
- For effective non-empty line count `501-700`, SoC split assessment is mandatory and must include itemized split candidates.
- For effective non-empty line count `>700` with functionality expansion, default classification is `Design Impact`.
- `>700` exception is allowed only with explicit rationale and near-term split plan.
- Delta gate: if a single changed source file has `>220` changed lines in current diff, record a design-impact assessment even if file size is `<=700`.
- During Stage 8, `workflow-state.md` should show `Current Stage = 8` and `Code Edit Permission = Locked`.

## Findings

- If none, write `None`.
- Otherwise:
  - `[CR-001] File: ... | Type: SoC/Layering/Naming/Duplication/FileSize/Complexity | Severity: Blocker/Major/Minor | Evidence: ... | Required update: ...`

## Re-Entry Declaration (Mandatory On `Fail`)

- Trigger Stage:
- Classification (`Local Fix`/`Design Impact`/`Requirement Gap`/`Unclear`):
- Required Return Path:
  - `Local Fix` -> update implementation artifacts first -> code fix -> rerun `Stage 6 -> Stage 7 -> Stage 8`
  - `Design Impact` -> `Stage 1 -> Stage 3 -> Stage 4 -> Stage 5 -> Stage 6 -> Stage 7 -> Stage 8`
  - `Requirement Gap` -> `Stage 2 -> Stage 3 -> Stage 4 -> Stage 5 -> Stage 6 -> Stage 7 -> Stage 8`
  - `Unclear`/cross-cutting -> `Stage 0 -> Stage 1 -> Stage 2 -> Stage 3 -> Stage 4 -> Stage 5 -> Stage 6 -> Stage 7 -> Stage 8`
  - Stage 0 in a re-entry path means re-open bootstrap controls in the same ticket/worktree (`workflow-state.md`, lock state, artifact baselines); do not create a new ticket folder.
- Upstream artifacts required before code edits:
  - `investigation-notes.md` updated (if required):
  - `requirements.md` updated (if required):
  - design basis updated (if required):
  - runtime call stacks + review updated (if required):

## Gate Decision

- Decision: `Pass` / `Fail`
- Implementation can proceed to `Stage 9`: `Yes` / `No`
- Notes:
