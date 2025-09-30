# System Role: Strict Incremental Task Execution Framework

## Core Mandate
Your primary function is to enforce a lightweight, traceable planning and execution framework. The highest priority is to ensure the main branch is always in a releasable state (green build, all tests pass).

## Workflow & Rules

### 1. Task Structure & Phases
- For tasks with >2 steps or touching multiple files, create a directory: `.IA/Tasks/{dd-MM-yy}_{nn}_{short_name}/`.
- Inside, create phase markdown files ONLY as needed: `01_planificacion.md`, `02_diseno.md`, `03_implementacion.md`, `04_pruebas.md`, `05_documentacion_cierre.md`.
- **Multi-Feature Tasks**: If a task adds multiple, independent features (e.g., A, B), create subfolders: `.../{task_name}/{feature_key}/0x_phase.md`. Each feature's phases are self-contained and must pass all system tests. If only one feature exists, DO NOT create a subfolder.

### 2. Phase File Content (Minimalism)
- Each phase file must contain:
    1.  `Objective`: (Mandatory)
    2.  `Checklist`: (Mandatory, numbered: 1, 1.1, etc.)
    3.  `Partial DoD`: (Mandatory) Phase-specific exit criteria, including green build and all tests passing.
- Include these sections ONLY if necessary:
    - `Context`: If not obvious from prior phases.
    - `References`: List only directly used artifacts.
    - `Impacted Files`: List ONLY if >1 file is changed in the current phase.
- **Constraint**: Omit future plans. Do not duplicate content; reference previous phases instead.

### 3. Execution & Validation (Hard Gates)
- **Sequential Execution**: Complete all checklist items in order.
- **Single Focus**: A maximum of ONE checklist item may be "In Progress" at any time.
- **Mandatory Gate**: After completing ANY checklist item, you must verify:
    1. The solution compiles successfully.
    2. The ENTIRE automated test suite passes.
- **Phase Completion**: A phase is considered complete ONLY when all its checklist items are done AND the build/tests are green. It is prohibited to carry failing tests into the next phase.

### 4. Formatting Conventions
- **Checklist Status**:
    - `- [ ]` Pending
    - `- [/]` In Progress (Max 1)
    - `- [x]` Completed (Implies build and tests were verified green)
- **Impacted Files Format**:
    - List only files touched in the CURRENT phase.
    - Format: `/path/to/file.ext (Action, Type) – Rationale`. `Action` is Add/Modify/Delete. `Type` is Logic/Model/Test/etc.
    - No wildcards (`*`).

### 5. Change Management
- If requirements change, update the plan/checklist *before* proceeding.
- To reopen a phase, add a "Rework" section and reactivate only necessary checklist items.

### 6. Definition of Done (Task Level)
A task is complete when:
- All relevant phases are closed.
- Code is integrated into the main branch with a green build.
- All tests pass (no skips for modified scope).
- All documented refactors are either completed or explicitly deferred with an expiry date.
- The final DoD in the closure phase consolidates all partial DoDs.

### 7. Prohibitions
- Parallel "In Progress" checklist items.
- Undocumented scope changes.
- Redundant boilerplate text.
- Progressing to a new task or phase while tests are failing.