# AI Task Workflow

Every implementation task follows this workflow.

## Phase 1 — Understand

Read:

* `AGENTS.md`
* `.ai/PROJECT_RULES.md`
* `.ai/PROJECT_STATE.md`
* Relevant subsystem rules

Understand the requested behavior.

Do not code yet.

## Phase 2 — Inspect

Inspect:

* Existing files
* Related classes
* Existing APIs
* Existing database models
* Existing components
* Existing tests
* Existing dependencies

Search before assuming something is missing.

## Phase 3 — Plan

Before implementation, identify:

### Files to create

List every new file.

### Files to modify

List every existing file that will change.

### Files to reuse

Identify existing implementations that will be reused.

### Database

Describe migrations/schema changes if required.

### API

Describe new or changed endpoints if required.

### Tests

Identify tests that need to be created or updated.

### Edge Cases

List important failure and boundary cases.

For non-trivial tasks, wait for user approval before implementation unless the user explicitly requested autonomous implementation.

## Phase 4 — Implement

Implement only the approved/requested scope.

Follow all applicable rules.

Prefer existing abstractions.

Do not introduce unrelated improvements.

## Phase 5 — Test

Run relevant:

* Unit tests
* Integration tests
* Build
* Type checking
* Linting when configured

Fix failures caused by the implementation.

Do not hide or ignore failures.

## Phase 6 — Review

Review the implementation against:

* Project rules
* Naming rules
* Architecture
* Security
* API contract
* Database rules
* Edge cases

Check for:

* Duplicate code
* Unnecessary files
* Unused imports
* Dead code
* Accidental changes
* Missing tests

## Phase 7 — Update State

Update `.ai/PROJECT_STATE.md` when the task changes meaningful project progress.

Record:

* Completed work
* Current phase
* Important decisions
* Known issues

Do not put large implementation details into PROJECT_STATE.md.

## Phase 8 — Report

Final response must contain:

1. Summary
2. Created files
3. Modified files
4. Tests executed
5. Build/type-check result
6. Important decisions
7. Known issues
8. Follow-up work, if any

Never claim a test passed unless it was actually executed.
