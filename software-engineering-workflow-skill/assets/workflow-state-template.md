# Workflow State

Use this file as the mandatory stage-control artifact for the ticket.
Update this file before every stage transition and before any source-code edit.

## Current Snapshot

- Ticket:
- Current Stage: `0` / `1` / `2` / `3` / `4` / `5` / `6` / `7` / `8` / `9` / `10`
- Next Stage:
- Code Edit Permission: `Locked` / `Unlocked`
- Active Re-Entry: `No` / `Yes`
- Re-Entry Classification (`Local Fix`/`Design Impact`/`Requirement Gap`/`Unclear`): `N/A`
- Last Transition ID:
- Last Updated:

## Stage Gates

| Stage | Gate Status (`Not Started`/`In Progress`/`Pass`/`Fail`/`Blocked`) | Gate Rule Summary | Evidence |
| --- | --- | --- | --- |
| 0 Bootstrap + Draft Requirement | Not Started | Ticket bootstrap complete + `requirements.md` Draft captured |  |
| 1 Investigation + Triage | Not Started | `investigation-notes.md` current + scope triage recorded |  |
| 2 Requirements | Not Started | `requirements.md` is `Design-ready`/`Refined` |  |
| 3 Design Basis | Not Started | Design basis updated for scope (`implementation-plan.md` sketch or `proposed-design.md`) |  |
| 4 Runtime Modeling | Not Started | `future-state-runtime-call-stack.md` current |  |
| 5 Review Gate | Not Started | Runtime review `Go Confirmed` (two clean rounds) |  |
| 6 Implementation | Not Started | Plan/progress current + source + unit/integration verification complete |  |
| 7 API/E2E Testing | Not Started | API/E2E test implementation complete + AC scenario gate complete |  |
| 8 Code Review | Not Started | Code review gate `Pass`/`Fail` recorded |  |
| 9 Docs Sync | Not Started | Docs updated or no-impact rationale recorded |  |
| 10 Handoff / Ticket State | Not Started | Final handoff complete + ticket state decision recorded |  |

## Stage Transition Contract (Quick Reference)

| Stage | Exit Condition | On Fail/Blocked |
| --- | --- | --- |
| 0 | Bootstrap complete + `requirements.md` is `Draft` | stay in `0` |
| 1 | `investigation-notes.md` current + scope triage recorded | stay in `1` |
| 2 | `requirements.md` is `Design-ready`/`Refined` | stay in `2` |
| 3 | Design basis current for scope | stay in `3` |
| 4 | Runtime call stack current | stay in `4` |
| 5 | Runtime review `Go Confirmed` (two clean rounds) | stay in `5` or return upstream and rerun |
| 6 | Source + required unit/integration verification complete | stay in `6` |
| 7 | API/E2E gate closes all executable mapped acceptance criteria (`Passed` or explicit user `Waived`) | `Blocked` on infeasible/no waiver; otherwise classified re-entry |
| 8 | Code review gate decision is `Pass` | classified re-entry then rerun |
| 9 | Docs updated or no-impact rationale recorded | stay in `9` |
| 10 | Final handoff complete; ticket move requires explicit user confirmation | stay in `10`/`in-progress` |

## Transition Matrix (Reference)

| Trigger | Required Transition Path | Gate Result |
| --- | --- | --- |
| Normal forward progression | `0 -> 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8 -> 9 -> 10` | Pass |
| Stage 6 unit/integration failure | stay in `6` | Fail |
| Stage 7 failure (`Local Fix`) | `6 -> 7` | Fail |
| Stage 7 failure (`Design Impact`) | `1 -> 3 -> 4 -> 5 -> 6 -> 7` | Fail |
| Stage 7 failure (`Requirement Gap`) | `2 -> 3 -> 4 -> 5 -> 6 -> 7` | Fail |
| Stage 7 failure (`Unclear`/cross-cutting root cause) | `0 -> 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7` | Fail |
| Stage 7 infeasible criteria without explicit user waiver | stay in `7` | Blocked |
| Stage 8 failure (`Local Fix`) | `6 -> 7 -> 8` | Fail |
| Stage 8 failure (`Design Impact`) | `1 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8` | Fail |
| Stage 8 failure (`Requirement Gap`) | `2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8` | Fail |
| Stage 8 failure (`Unclear`/cross-cutting root cause) | `0 -> 1 -> 2 -> 3 -> 4 -> 5 -> 6 -> 7 -> 8` | Fail |

Note:
- In re-entry paths, Stage 0 means re-open bootstrap controls in the same ticket/worktree (`workflow-state.md`, lock state, artifact baselines); do not create a new ticket folder.

## Pre-Edit Checklist (Stage 6 Source-Code Edits)

- Current Stage is `6`: `Yes` / `No`
- Code Edit Permission is `Unlocked`: `Yes` / `No`
- Stage 5 gate is `Go Confirmed`: `Yes` / `No`
- Required upstream artifacts are current: `Yes` / `No`
- Pre-Edit Checklist Result: `Pass` / `Fail`
- If `Fail`, source code edits are prohibited.

## Re-Entry Declaration

- Trigger Stage (`7`/`8`):
- Classification (`Local Fix`/`Design Impact`/`Requirement Gap`/`Unclear`):
- Required Return Path:
- Required Upstream Artifacts To Update Before Code Edits:
- Resume Condition:

## Transition Log (Append-Only)

| Transition ID | Date | From Stage | To Stage | Reason | Classification | Code Edit Permission After Transition | Evidence Updated |
| --- | --- | --- | --- | --- | --- | --- | --- |
| T-001 | YYYY-MM-DD | 0 | 1 | Bootstrap complete, moving to investigation | N/A | Locked | requirements.md, workflow-state.md |

## Audible Notification Log (Optional Tracking)

| Date | Trigger Type (`Transition`/`Gate`/`Re-entry`/`LockChange`) | Summary Spoken | Speak Tool Result (`Success`/`Failed`) | Fallback Text Logged |
| --- | --- | --- | --- | --- |
| YYYY-MM-DD | Transition | Stage 0 complete, moving to Stage 1 investigation. | Success | N/A |

## Process Violation Log

| Date | Violation ID | Violation | Detected At Stage | Action Taken | Cleared |
| --- | --- | --- | --- | --- | --- |
| YYYY-MM-DD | V-001 | Source code edited while `Code Edit Permission = Locked` | 3 | Stopped edits, declared re-entry, updated upstream artifacts | No |
