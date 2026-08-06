# Architecture Control Template

Use this template only for greenfield, architecture-change, or multi-slice work. Remove sections that do not affect the critical flow. Keep every statement testable or explicitly mark it as an assumption.

## `ARCHITECTURE.md`

```markdown
# Architecture: <project or feature>

## Status
- State: draft | approved | superseded
- Updated: YYYY-MM-DD
- Scope: <what this document governs>

## Outcome
- User outcome: <observable result>
- Acceptance criteria:
  - <measurable condition>
- Non-goals:
  - <explicit exclusion>
- Constraints: <runtime, deployment, integration, security, performance, deadline>

## Critical Flow
1. <actor or system input>
2. <validation and primary processing>
3. <result, persistent state, or external effect>
- Expected error path: <caller-visible failure behavior>

## Components And Boundaries
| Component | Owns | Inputs and outputs | Error behavior | Persistent data / external dependency |
| --- | --- | --- | --- | --- |
| <module> | <responsibility> | <contract> | <behavior> | <ownership> |

## Data And Interfaces
- Data model or schema changes: <none or concise definition>
- Public API, event, CLI, or UI contracts: <none or concise definition>
- Compatibility and migration: <none or plan>

## Decisions
| ID | Decision | Reason | Rejected alternative | Revisit trigger |
| --- | --- | --- | --- | --- |
| ADR-001 | <choice> | <constraint or evidence> | <alternative> | <condition> |

## Vertical Slices
| ID | Outcome | Components / contracts | Acceptance criteria | Validation |
| --- | --- | --- | --- | --- |
| S1 | <first verifiable flow> | <affected boundary> | <observable condition> | <test or manual check> |

## Known Risks
| Risk or assumption | Early test | Owner | Result |
| --- | --- | --- | --- |
| <uncertainty> | <fastest evidence> | <role or module> | pending |
```

## `IMPLEMENTATION_STATUS.md`

```markdown
# Implementation Status: <project or feature>

## Current State
- Updated: YYYY-MM-DD
- Current slice: S1
- Overall state: planned | in progress | blocked | verified
- Current blocker: <none or concrete dependency / decision>

## Slice Ledger
| Slice | Status | Spec / modules | Acceptance result | Validation evidence | Blocker or deviation |
| --- | --- | --- | --- | --- | --- |
| S1 | planned | <link or section> | pending | pending | none |

## Deviations
| ID | Affected slice | Approved change | Reason and impact | Required spec update | State |
| --- | --- | --- | --- | --- | --- |
| D-001 | S1 | <change> | <reason> | <section or decision> | open |

## Next Action
- <one smallest action that can change the current state>
```

## Status Rules

- `planned`: Specification exists; work has not started.
- `in progress`: Implementation work is active; acceptance is not yet proven.
- `blocked`: Progress depends on a named external input, decision, or failed prerequisite.
- `verified`: The acceptance criteria passed and the ledger links to real validation evidence.
- `superseded`: The slice or decision was replaced; link to its replacement and retain history.

Do not use percentages as the primary progress signal. A slice has only one current status. Update the ledger after a state change, and keep a failed check visible until it is resolved or superseded.

## Conformance Check

For each slice, verify the implementation against `ARCHITECTURE.md`:

1. The changed files belong to the specified modules or an approved deviation explains the new boundary.
2. Public interfaces, validation, error behavior, and data ownership match the stated contract.
3. Tests or manual checks prove the stated acceptance criteria.
4. The ledger records the command, result, or repeatable manual evidence.
5. Any deviation updates the relevant decision, affected slice, and future validation before dependent work begins.
