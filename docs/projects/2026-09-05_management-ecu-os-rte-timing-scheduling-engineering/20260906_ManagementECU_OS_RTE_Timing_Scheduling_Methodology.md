# Management ECU OS / RTE Timing & Scheduling — Current Package Methodology

Date: 2026-09-06 JST
Status: `LUNA_COMPILE_PROPOSAL`
Scope: downstream compilation from exact-pinned Sol-reviewed authority

## 1. Mission and closure

This package compiles the current Management ECU OS/RTE Timing & Scheduling engineering route. It is not a new AUTOSAR, Vector or vendor research pass. The generic technical research frontier is closed at the reviewed scope.

The package contains exactly the following task identities:

`OSRTE-001` through `OSRTE-018`

No `OSRTE-019` or other task is created.

The package is a navigation and handoff artifact. It does not select Management ECU values, establish generated-code correctness, prove compile/link success, establish runtime scheduling/timing, or produce a verdict or coverage result.

## 2. Authority contract

Technical claims are resolved only through the following exact-pinned Reviewed Knowledge tuples declared by `references/authority-pins.yaml`.

| Authority | Exact tuple | Use |
|---|---|---|
| AUTOSAR CP architecture/workflow | `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d` | Runnable/RTEEvent, RTE generation, OS execution objects, time-driven objects, multicore, protection and timing work products |
| AUTOSAR SchM / ExclusiveArea | `eariver/Research_AUTOSAR_CP_Documents@3eec41439f25f61c29e0c1a06a51df148e493014` | SW-C/BSW ExclusiveArea identity, SchM boundary and conditional realization model |
| Vector/MICROSAR product procedure | `eariver/Research_Vector_Documents@7285e6a773433488c59186bbd241bdab39efb4ce` | Sol-reviewed DaVinci Configurator Classic 6.3.10 procedure maturity for OSRTE-004–016 |
| Downstream project context | `eariver/Automotive_EE_Engineering_Knowledge@e616fce2fb8f2e906a7e77662c89c5f633f82355` | Read-only project context and prior Sol-reviewed integration state; not a new technical source |

The project-input baseline remains the exact branch input at the starting tree and has status `UNRESOLVED_PROJECT_INPUT`. It is used to identify blockers, not to provide values.

Excluded from this compilation: Web, raw AUTOSAR PDFs, raw Vector HELP, current vendor documentation, floating heads, generic knowledge, unreviewed observations and project assumptions.

## 3. Compilation dimensions

Every task row is compiled across independent dimensions:

1. semantic/model identity and owner;
2. lifecycle phase and engineering intent;
3. strongest reviewed workflow or product procedure;
4. primary procedure availability;
5. project-input blocker;
6. project-design blocker;
7. execution-evidence blocker;
8. input artifact/state;
9. operation/activity;
10. output artifact/state;
11. exit condition and next handoff;
12. retained boundary or documentation negative;
13. evidence required for the next promotion.

Procedure availability is not project closure. An exact generic mapping operation can coexist with an unresolved project mapping, and a reviewed workflow can coexist with absent runtime evidence.

## 4. Lifecycle chain

```text
project requirement / model intent
 -> SW-C/RTE contract
 -> OS/RTE configuration
 -> validation result
 -> generated artifact
 -> compile/link result
 -> runtime trace
 -> timing/mutual-exclusion/protection observation
 -> requirement comparison
 -> verdict
 -> coverage
```

Each arrow is a handoff requiring its own artifact or observation. No upstream state is treated as proof of a downstream state.

The following identities remain non-collapsible:

```text
RunnableEntity != OS Task
RTEEvent != OS Event
Runnable-to-Task mapping != runtime Task execution
Counter != Alarm != ScheduleTable
OS Resource != Spinlock != SchM/ExclusiveArea != interrupt-control mechanism
SW-C ExclusiveArea != BSW ExclusiveArea project identity
ExclusiveArea model != RTE/SchM API != selected realization
SchM != AUTOSAR OS scheduler
OS-Application != CPU core
configuration != validation != generation != compile/link != runtime trace
measured timing != timing requirement != verdict != coverage
MIL/SIL/VECU timing != physical-target timing
```

## 5. Task-family compilation route

| Family | Tasks | Compilation treatment |
|---|---|---|
| Architecture and activation | OSRTE-001–004 | Preserve model, RTE and generated-realization boundaries; use project input/design for actual identities and mapping. |
| Task, ISR and scheduler | OSRTE-005–007 | Preserve Basic/Extended Task, Event, priority/preemption and ISR distinctions; do not infer a schedule. |
| Time-driven OS objects | OSRTE-008–010 | Trace Counter → Alarm/ScheduleTable roles without collapsing objects or asserting timing results. |
| Mutual exclusion and multicore | OSRTE-011–014 | Keep Resource, Spinlock and SchM/ExclusiveArea separate; preserve local/cross-core boundaries. |
| Protection and integration | OSRTE-015–016 | Preserve OS-Application/protection semantics and separate configuration, generation and build handoff. |
| Timing and evidence | OSRTE-017–018 | Keep requirements, models, measurements, verdict and coverage as separate records. |

## 6. Availability vocabulary

Primary procedure labels are restricted to:

- `EXACT_PROCEDURE_AVAILABLE`
- `PARTIAL_PROCEDURE_AVAILABLE`
- `SURFACE_ONLY`
- `NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE`
- `WORKFLOW_ONLY`
- `EXECUTION_EVIDENCE_REQUIRED`

Blocker fields are orthogonal and use `PROJECT_INPUT_REQUIRED`, `PROJECT_DESIGN_REQUIRED`, `EXECUTION_EVIDENCE_REQUIRED`, or an explicit `NOT_REQUIRED` state. A blocker is not silently converted into a procedure maturity label.

The Sol-reviewed Vector distribution is preserved:

- Exact: OSRTE-004, 008, 009, 010;
- Partial: OSRTE-005, 007, 011, 013, 014, 015, 016;
- Surface only: OSRTE-006;
- No explicit reviewed procedure: OSRTE-012.

The remaining current-package labels are compiled from the reviewed AUTOSAR workflow/evidence boundary: OSRTE-001, 002, 003 and 018 are `WORKFLOW_ONLY`; OSRTE-017 is `PARTIAL_PROCEDURE_AVAILABLE`.

## 7. Project-value discipline

No task name, Runnable/RTEEvent identity, Runnable-to-Task mapping, Task/Event type or mask, priority, preemption, period, offset, activation limit, ISR value, Counter/Alarm/ScheduleTable value, Resource/Spinlock identity, ExclusiveArea mechanism, core/OS-Application relation, protection budget, timing requirement, compiler/linker value, runtime stimulus, acceptance criterion, verdict or coverage value is invented or defaulted.

Generic authority is retained where it exists. The project-specific closure remains blocked until an explicit project artifact or design decision supplies the value.

## 8. Package outputs and validation

The nine outputs are:

1. Methodology;
2. Step-by-Step Guide;
3. Tool / Task / Reference Matrix;
4. State & Evidence Model;
5. Execution Reference Guide;
6. Procedure Coverage Matrix;
7. Reference Index;
8. Current Package Compilation Report;
9. terminal checkpoint.

Before the bounded commit, validate:

- both YAML matrices contain each of OSRTE-001–018 exactly once;
- no duplicate or extra task exists;
- availability counts total 18;
- each supported technical claim resolves to an exact tuple in the authority catalog;
- project/design/execution blockers are separate;
- documentation negatives and non-collapse rules remain visible;
- only the nine allowlisted paths are changed.

Final maturity is subject to Sol fixed-head review.
