## 1. Purpose
Provide a lightweight, traceable planning and execution framework that enforces incremental delivery, continuous integration, and test discipline.

## 2. Core Principles
1. Deliver in vertical, releasable slices.
2. Keep the main branch releasable at all times (green build + tests pass).
3. Each atomic change keeps build and tests green.
4. Explicit, minimal documentation only where value is added.
5. No silent technical debt: document deferrals with expiry.
6. At the end of EVERY phase: full solution compiles and ALL tests pass (mandatory gate).

## 3. Workflow
1. Plan (identify scope, phases, impacted files if >1 file will change).
2. Execute steps sequentially; do not start a new step before completing the current one.
3. Update phase file immediately on scope or assumption changes.
4. Validate green build + tests after each completed checklist item and at phase end.

## 4. Task Folder & Phases
For tasks requiring >2 steps or touching multiple files create:
`.IA/Tasks/{dd-MM-yy}_{nn}_{short_name}/`
Phase files (create only those needed):
01_planificacion.md (planning / analysis)
02_diseno.md (design)
03_implementacion.md (implementation)
04_pruebas.md (testing)
05_documentacion_cierre.md (closure)

Functional segmentation (mandatory when adding more than one distinct functionality in the same task):
If the task introduces multiple independent features (A, B, ...), create a subfolder per feature:
`.IA/Tasks/{date}_{nn}_{task}/{feature_key}/0x_phase.md`
Each feature keeps its own minimal phase files (only those needed). End of every phase per feature: build + all tests pass (including tests for previously completed features).
Shared cross-cutting changes (e.g., refactor touching all features) may use root-level phase files, but prefer isolation inside each feature folder.
If there is only one feature, do NOT create a nested feature folder—use the root phase files only.

## 5. Phase File Minimal Sections
Each phase file contains only what is required:
1. Objective (mandatory)
2. Context (only if not already obvious from earlier phases)
3. References (only directly used artifacts; include `.IA/commands.md` if commands run)
4. Impacted Files (present ONLY if >1 file is or will be changed in this phase)
5. Checklist (numbered: 1, 1.1, 1.2 ...; one in‑progress item max)
6. Notes (timestamped decisions for this phase only)
7. Partial DoD (phase exit criteria – must include green build + passing tests)

Omit future or unrelated information. Do not duplicate content from other phases—reference them briefly if needed.

## 6. Checklist Conventions
`- [ ]` Pending
`- [/]` In Progress (only one at a time)
`- [x]` Completed (implies build + tests verified)

## 7. Impacted Files Rules
List ONLY files touched in the active phase (repeat a file if touched again with new rationale).
Format: `/path/file (Add|Modify|Delete, Type) – Rationale`
No wildcards. Strike through (markdown `~~`) items no longer needed with a short reason.
Do not copy the list to later phases; recreate only if further changes occur.

## 8. Updates & Rework
If requirements change mid‑phase, adjust the checklist before proceeding.
If reopening a closed phase, add a Rework subsection and re‑activate only necessary items.

## 9. Retention & Cleanup
At session start scan `.IA/Tasks`:
– Do not delete folders <24h old.
– Candidates >10 days: present (or mark) for deletion or archive (`_archived`).
– Summarize removed vs retained.

## 10. Definition of Done (Iteration / Task)
All phases closed when applicable and:
1. Code integrated on main branch (or ready to merge) with green build.
2. All tests pass (no skips/placeholders for changed scope).
3. Documented refactors applied or deferred with explicit note + expiry.
4. Documentation updated only where behavior/usage changed.
5. Partial DoDs satisfied and consolidated into a final DoD in closure phase.

## 11. Phase Completion Rule (Hard Gate)
Phase ends ONLY when:
– All checklist items completed.
– Solution builds successfully.
– Full automated test suite executes successfully.
– Partial DoD recorded.

## 12. Prohibited
– Parallel in‑progress checklist items.
– Undocumented scope changes.
– Adding broad boilerplate or redundant text.
– Carrying unresolved failing tests into next phase.

## 13. Example (Implementation Phase Fragment)
```
## Objective
Implement batch notification endpoint.

## Impacted Files
/VL.Notifications.Service/Controllers/NotificationController.cs (Modify, Logic) – Add batch endpoint
/VL.Notifications.Domain/Entities/Notification.cs (Modify, Model) – Add BatchId
/VL.Notifications.DB/Repositories/NotificationRepository.cs (Modify, Persistence) – Store BatchId
/VL.Notifications.API/Validators/BatchNotificationValidator.cs (Add, Validation) – New validator
/VL.Notifications.API.Tests/Validators/BatchNotificationValidatorTests.cs (Add, Test) – Coverage

## Checklist
- [x] 1 Add BatchId to domain entity
- [x] 2 Repository persistence
- [/] 3 Controller endpoint
  - [ ] 3.1 Request model & validator
  - [ ] 3.2 Service call
  - [ ] 3.3 Response mapping
```

End of document.
