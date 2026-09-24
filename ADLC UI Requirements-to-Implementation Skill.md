# ADLC UI Requirements-to-Implementation Skill

## Purpose

Convert user stories into complete, traceable, verifiable UI implementations.

The skill prevents direct translation from natural-language user stories into UI code by introducing an explicit requirements and UI-contract layer.

## Core Principle

Never implement a UI directly from a user story.

Always follow:

User Story
→ Requirements
→ UI Contract
→ Traceability
→ Implementation Plan
→ Implementation
→ Validation
→ Fix
→ Re-validation

## Primary Objectives

1. Extract all explicit requirements.
2. Identify derived requirements.
3. Identify assumptions.
4. Identify ambiguities and missing information.
5. Produce a structured UI Contract.
6. Map every requirement to UI elements.
7. Implement only against the approved contract.
8. Validate implementation against every requirement.
9. Detect missing or incorrectly implemented requirements.
10. Iterate until validation passes or unresolved requirements require human input.

## Rules

### Requirement Preservation

Every explicit requirement MUST receive a unique requirement ID.

Never silently discard a requirement.

### No Silent Assumptions

Do not convert an assumption into a requirement without explicitly marking it as an assumption.

### No Feature Invention

Do not introduce business functionality that is not supported by the user story, existing requirements, project documentation, or established product rules.

### Ambiguity Handling

If a missing decision materially affects the UI or behavior, record it as an unresolved question.

Do not silently choose an implementation.

### Traceability

Every UI feature MUST map to one or more requirements.

Every mandatory requirement MUST map to at least one UI element, interaction, state, or behavior.

### Implementation

The implementation must follow the UI Contract.

The original user story is context; the UI Contract is the implementation specification.

### Validation

Before completion, validate:

- requirement coverage
- UI element coverage
- interaction coverage
- state coverage
- route/navigation coverage
- accessibility requirements
- responsive behavior
- design-system consistency
- behavioral correctness

## Workflow

### Phase 1 — Analyze

Read the user story and relevant project context.

Extract:

- actors
- goals
- actions
- data
- constraints
- business rules
- acceptance criteria

Classify information as:

- explicit requirement
- derived requirement
- assumption
- ambiguity

### Phase 2 — Build Requirements Model

Create unique IDs:

REQ-001
REQ-002
...

Each requirement must contain:

- id
- description
- source
- priority
- type
- acceptance criteria

### Phase 3 — Build UI Contract

Define:

- page
- route
- layout
- sections
- components
- data displayed
- actions
- interactions
- navigation
- states
- validation
- permissions
- responsive behavior

### Phase 4 — Completeness Gate

Check that:

- every explicit requirement is represented
- every requirement has acceptance criteria
- every mandatory requirement maps to the UI contract
- critical ambiguities are resolved

If the gate fails, stop implementation.

### Phase 5 — Traceability

Create:

Requirement
→ UI element
→ Component
→ Behavior
→ Test

### Phase 6 — Implementation Planning

Determine:

- existing reusable components
- existing design-system components
- routes
- API requirements
- state management
- validation
- tests

Prefer existing project patterns over introducing new patterns.

### Phase 7 — Implementation

Implement the UI strictly according to the UI Contract.

Do not add unsupported business behavior.

### Phase 8 — Validation

Run:

1. structural validation
2. behavioral validation
3. visual validation when available

Produce a validation report.

### Phase 9 — Remediation

For every failure:

1. identify the requirement
2. identify the implementation gap
3. make the smallest appropriate change
4. re-run validation

Do not declare completion while mandatory requirements remain failed.

## Completion Criteria

The task is complete only when:

- all mandatory requirements are covered
- all required UI elements exist
- required interactions work
- required states exist
- validation passes
- no critical ambiguities remain

Otherwise report:

NOT COMPLETE