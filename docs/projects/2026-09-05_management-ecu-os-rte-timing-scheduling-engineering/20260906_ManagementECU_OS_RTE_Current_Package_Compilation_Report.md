# Management ECU OS / RTE Timing & Scheduling — Current Package Compilation Report

Date: 2026-09-06 JST
Status: `LUNA_COMPILE_PROPOSAL`
Mission: current engineering package compilation only

## 1. Result summary

Exactly 18 task rows are compiled: `OSRTE-001` through `OSRTE-018`. No nineteenth task is present. The package is based on exact-pinned Sol-reviewed authority and does not perform new technical research.

For OSRTE-004 through OSRTE-016, the Sol-reviewed Vector product classifications are carried forward unchanged. The exact product procedure is generic and does not select Management ECU values.

## 2. Task-by-task current proposal

| Task | Current engineering route | Primary availability | Project input | Project design | Execution evidence |
|---|---|---|---|---|---|
| OSRTE-001 | architecture/ownership/execution-chain navigation | `WORKFLOW_ONLY` | `PROJECT_INPUT_REQUIRED` | `NOT_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-002 | RunnableEntity category and activation/concurrency | `WORKFLOW_ONLY` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-003 | RTEEvent/TimingEvent activation and observation boundary | `WORKFLOW_ONLY` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-004 | Runnable-to-Task mapping and generated RTE boundary | `EXACT_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-005 | Basic/Extended Task and OS Event lifecycle | `PARTIAL_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-006 | priority/preemption/scheduling surface and outcome boundary | `SURFACE_ONLY` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-007 | ISR category/source/priority and Task boundary | `PARTIAL_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-008 | OS Counter and tick-domain route | `EXACT_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-009 | Alarm expiry/action route | `EXACT_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-010 | ScheduleTable/Expiry Points route | `EXACT_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-011 | local OS Resource boundary | `PARTIAL_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-012 | SchM/ExclusiveArea integration boundary | `NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-013 | multicore/core assignment/cross-core activation | `PARTIAL_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-014 | Spinlock/cross-core mutual exclusion | `PARTIAL_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-015 | OS-Application/memory/timing protection/recovery | `PARTIAL_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-016 | configuration/validation/generation/compile-link handoff | `PARTIAL_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `NOT_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-017 | timing requirements/event chains/analysis realization | `PARTIAL_PROCEDURE_AVAILABLE` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `NOT_REQUIRED_FOR_CURRENT_COMPILE` |
| OSRTE-018 | runtime scheduling/timing/measurement/verdict/coverage | `WORKFLOW_ONLY` | `PROJECT_INPUT_REQUIRED` | `PROJECT_DESIGN_REQUIRED` | `EXECUTION_EVIDENCE_REQUIRED` |

Detailed engineering intent, lifecycle, owner/layer, exact authority refs, input/output states, operations, exit conditions, handoffs, retained negatives and promotion evidence are in the Tool / Task / Reference Matrix.

## 3. Availability counts

| Availability | Count |
|---|---:|
| `EXACT_PROCEDURE_AVAILABLE` | 4 |
| `PARTIAL_PROCEDURE_AVAILABLE` | 8 |
| `SURFACE_ONLY` | 1 |
| `NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE` | 1 |
| `WORKFLOW_ONLY` | 4 |
| `EXECUTION_EVIDENCE_REQUIRED` | 0 |
| Total | 18 |

The `EXECUTION_EVIDENCE_REQUIRED` value is retained as a permitted primary vocabulary item but is used here as the separate closure blocker for OSRTE-018, not as a replacement for its `WORKFLOW_ONLY` route.

## 4. Blocker counts

- Project-input-required: all 18 tasks.
- Project-design-required: OSRTE-002–015 except OSRTE-016, plus OSRTE-017 and OSRTE-018; total 16.
- Execution-evidence-required: OSRTE-018 only.

These blockers do not downgrade generic procedure maturity. In particular, OSRTE-004 remains exact at product-operation scope while its actual mapping is project design/input.

## 5. Evidence-layer contract

```text
configured intent
 -> validation result
 -> generated artifact
 -> compile/link result
 -> runtime activation/dispatch/preemption/blocking/completion trace
 -> timing/mutual-exclusion/protection observation
 -> requirement comparison
 -> verdict
 -> coverage
```

`Validation Successful`, `Generation Successful`, a generic build statement or a generated artifact does not prove runtime scheduling, timing, protection, mutual exclusion, verdict or coverage.

## 6. Fixed high-risk boundaries

- RunnableEntity != OS Task.
- RTEEvent != OS Event.
- Runnable-to-Task mapping != runtime Task execution.
- Counter != Alarm != ScheduleTable.
- OS Resource != Spinlock != SchM/ExclusiveArea != interrupt-control mechanism.
- SW-C ExclusiveArea != BSW ExclusiveArea project identity.
- ExclusiveArea model != RTE/SchM API != selected realization.
- SchM != AUTOSAR OS scheduler.
- OS-Application != CPU core.
- configured priority != observed scheduling outcome.
- period/offset/activation != WCET.
- configuration != validation != generation != compile/link != runtime trace.
- measured timing != timing requirement != verdict != coverage.
- MIL/SIL/VECU timing != physical-target timing.

## 7. Retained documentation negatives

The package retains the Vector-reviewed negatives for missing exact SchM/ExclusiveArea product field/procedure/mapping, incomplete Task/Resource/Spinlock/protection detail, incomplete OS/RTE diagnostic/build manifest, and absent Management ECU build/runtime evidence. These are documentation-scope negatives, not capability-absence claims.

## 8. Scope and review disposition

No Management ECU Task, priority, period, offset, core, ISR, Counter/Alarm/ScheduleTable, Resource/Spinlock, ExclusiveArea mechanism, protection budget, timing requirement, compiler/linker value, runtime value, acceptance criterion, verdict or coverage was invented.

This is a Luna compilation proposal. Final maturity remains subject to Sol fixed-head review.
