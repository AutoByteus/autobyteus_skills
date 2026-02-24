# System Validation

Use this document for Stage 6 aggregated validation (API/E2E/System).
Do not use this file for unit/integration tracking; that belongs in `implementation-progress.md`.

## Validation Scope

- Ticket:
- Scope classification: `Small` / `Medium` / `Large`
- Requirements source: `tickets/in-progress/<ticket-name>/requirements.md`
- Call stack source: `tickets/in-progress/<ticket-name>/future-state-runtime-call-stack.md`
- Design source (`Medium/Large`): `tickets/in-progress/<ticket-name>/proposed-design.md`

## Coverage Rules

- Every critical requirement must map to at least one scenario.
- Every in-scope use case must map to at least one scenario, or explicitly `N/A` with rationale.
- `Design-Risk` scenarios must include explicit technical objective/risk and expected outcome.
- Manual testing is not part of the default workflow.

## Scenario Catalog

| Scenario ID | Source Type (`Requirement`/`Design-Risk`) | Requirement ID(s) | Use Case ID(s) | Level (`API`/`E2E`/`System`) | Objective/Risk | Expected Outcome | Command/Harness | Status (`Not Started`/`In Progress`/`Passed`/`Failed`/`Blocked`/`N/A`) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| SV-001 | Requirement | R-001 | UC-001 | API | N/A |  |  | Not Started |

## Failure Escalation Log

| Date | Scenario ID | Failure Summary | Investigation Required (`Yes`/`No`) | Classification (`Local Fix`/`Design Impact`/`Requirement Gap`) | Action Path | `investigation-notes.md` Updated | Requirements Updated | Design Updated | Call Stack Regenerated | Review Re-Entry Round | Resolved |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| YYYY-MM-DD | SV-001 |  |  |  |  |  |  |  |  |  | No |

Rules:
- `Design Impact` requires `Investigation Required = Yes` and investigation checkpoint before design write-backs.
- If requirement-level gaps are found during design-impact investigation, reclassify to `Requirement Gap`.
- `Design Impact` and `Requirement Gap` both require review re-entry to `Go Confirmed` before final validation completion.

## Feasibility And Risk Record

- Any infeasible scenarios (`Yes`/`No`):
- If `Yes`, concrete infeasibility reason per scenario:
- Environment constraints (secrets/tokens/access limits/dependencies):
- Compensating automated evidence:
- Residual risk notes:

## Stage 6 Gate Decision

- Stage 6 complete: `Yes` / `No`
- Critical scenarios passed: `Yes` / `No`
- Infeasibility + compensating evidence documented (if applicable): `Yes` / `No` / `N/A`
- Unresolved escalation items: `Yes` / `No`
- Notes:
