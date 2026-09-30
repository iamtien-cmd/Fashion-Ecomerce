# AI Development Instructions

This repository uses a hierarchical AI rule system.

These instructions are mandatory for every AI coding task.

## 1. Mandatory Rule Loading

Before modifying, creating, deleting, or renaming any file:

1. Read this file.
2. Read `.ai/PROJECT_RULES.md`.
3. Read `.ai/TASK_WORKFLOW.md`.
4. Read `.ai/PROJECT_STATE.md` if it exists.
5. Identify the affected subsystem.
6. Read all applicable rules for that subsystem.

Do not begin implementation before completing these steps.

## 2. Rule Hierarchy

Rules are hierarchical.

Priority from broadest to most specific:

1. `AGENTS.md`
2. `.ai/PROJECT_RULES.md`
3. `.ai/TASK_WORKFLOW.md`
4. Subsystem rules
5. Technology-specific rules

When a more specific rule conflicts with a general rule, the more specific rule takes precedence.

If two rules at the same level conflict, stop and report the conflict instead of guessing.

## 3. Repository Inspection

Never assume that a class, component, service, endpoint, table, or utility does not exist.

Search the repository before creating new abstractions.

Prefer modifying or reusing existing code when appropriate.

## 4. Scope Control

Only modify files necessary for the requested task.

Do not perform unrelated refactoring.

Do not change architecture, dependencies, database strategy, authentication strategy, or public API contracts unless explicitly requested or required by the task.

## 5. Planning

For non-trivial tasks, provide a plan before implementation.

The plan must identify:

* Files to create
* Files to modify
* Files to reuse
* Database changes
* API changes
* Tests
* Important edge cases

## 6. Verification

After implementation:

* Run relevant tests.
* Run the appropriate build/type-check command.
* Check imports.
* Check naming.
* Check architecture boundaries.
* Check security implications.
* Check for unintended changes.

Report all modified and created files.

## 7. No Guessing

Do not invent:

* Business requirements
* Existing APIs
* Database fields
* Authentication behavior
* Project conventions
* Dependencies
* Architecture decisions

If information is ambiguous and materially affects implementation, stop and ask for clarification.

## 8. State Management

After completing a meaningful task, update:

`.ai/PROJECT_STATE.md`

Keep the project state concise and factual.
