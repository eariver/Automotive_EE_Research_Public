# Management ECU OS / RTE Timing & Scheduling — Step-by-Step Guide

This guide is the downstream execution route for the current package. It contains no Management ECU configuration values and does not reopen generic AUTOSAR or Vector research.

## 1. Start with the engineering goal

Record the goal as a project-owned statement, then classify the semantic object before selecting a tool surface.

| Question | Keep separate |
|---|---|
| What executes? | SW-C `RunnableEntity`, BSW schedulable entity, OS Task or ISR |
| What activates it? | RTEEvent, OS Event, Counter/Alarm/ScheduleTable action or interrupt source |
| What protects it? | OS Resource, Spinlock, SchM/ExclusiveArea or interrupt-control mechanism |
| What constrains timing? | timing requirement/model/constraint, OS timing protection or measured observation |
| What proves it? | configuration, generated artifact, compile/link result, runtime trace, assessment, verdict or coverage |

Never rename one identity into another to make the route appear complete.

## 2. Select the task row

Use the exact task identity in the machine-readable matrices. The task set is closed at `OSRTE-001`–`OSRTE-018`.

- Architecture/contract: OSRTE-001–004
- Task/ISR/scheduler: OSRTE-005–007
- Counter/Alarm/ScheduleTable: OSRTE-008–010
- Resource/SchM/multicore/Spinlock: OSRTE-011–014
- OS-Application/protection/build: OSRTE-015–016
- Timing and execution evidence: OSRTE-017–018

## 3. Load the exact authority tuple

Resolve the row's `exact_reviewed_authority_refs` in the Tool / Task / Reference Matrix and then in the Reference Index. Use only the pinned commit, path, blob and reviewed status recorded there.

The three technical authority families are:

- AUTOSAR CP architecture/workflow: `938ac4af696d263019ebdc61106a444447e15c4d`;
- AUTOSAR SchM/ExclusiveArea: `3eec41439f25f61c29e0c1a06a51df148e493014`;
- Vector/MICROSAR procedure: `7285e6a773433488c59186bbd241bdab39efb4ce`.

## 4. Confirm input state before operating

For each row, check whether the required project artifact is present. Typical input families are:

- SW-C `InternalBehavior`, `RunnableEntity` and RTEEvent contract;
- generated-RTE mapping design and OS/RTE configuration;
- Task/Event/ISR and Counter/Alarm/ScheduleTable configuration;
- Resource/Spinlock/SchM/ExclusiveArea and core topology design;
- OS-Application/protection configuration;
- timing requirements, event chains, models and acceptance criteria;
- toolchain, generated artifacts, build records and runtime evidence.

The project baseline is `UNRESOLVED_PROJECT_INPUT`. Missing values remain missing.

## 5. Perform only the supported activity

### 5.1 Model and activation route

For OSRTE-001–004, preserve:

```text
SW-C behavior -> RunnableEntity -> RTEEvent
 -> configured/generated RTE realization -> OS Task/ISR context
```

The route does not establish the actual Runnable-to-Task mapping, runtime dispatch or timing outcome.

### 5.2 Task, event and ISR route

For OSRTE-005–007, keep Basic/Extended Task, OS Event, priority/preemption and ISR as separate OS concerns. A configured priority or mapping is not an observed schedule. Category-specific protection semantics must not be generalized across ISR categories.

### 5.3 Time-driven route

For OSRTE-008–010, trace roles in this order when the project supplies them:

```text
OS Counter tick -> Alarm expiry/action
                  or ScheduleTable expiry point -> Task activation / OS Event set
                  -> OS scheduler state
```

`Counter`, `Alarm` and `ScheduleTable` remain distinct objects. Configuration is not wake-up timing evidence.

### 5.4 Mutual-exclusion and multicore route

For OSRTE-011–014, first classify locality and owner context. Keep these as separate alternatives and records:

```text
local OS Resource
cross-core OS Spinlock
SW-C/BSW SchM or ExclusiveArea contract
interrupt-control mechanism
```

Do not infer an ExclusiveArea realization from a Resource or Spinlock name. Do not treat core assignment as a timing or mutual-exclusion proof.

### 5.5 Protection and integration route

For OSRTE-015–016, preserve:

```text
OS-Application/protection design
 -> configuration validation
 -> generation
 -> compile/link
 -> runtime protection/scheduling observation
```

The product procedure maturity of OSRTE-016 is aggregate `PARTIAL_PROCEDURE_AVAILABLE`; exact subcommands do not close compile/link or runtime evidence.

### 5.6 Timing and evidence route

For OSRTE-017–018, keep the following records separate:

```text
timing requirement/model/constraint
 -> realization design
 -> runtime observation/measurement
 -> requirement comparison
 -> verdict
 -> coverage
```

MIL/SIL/VECU results do not become physical-target timing merely by being measured.

## 6. Record the row state

For every row, record:

1. input artifact and state;
2. operation/activity actually supported by the authority;
3. output artifact and state;
4. exit condition;
5. next handoff;
6. retained negative/boundary;
7. evidence needed for the next promotion.

Use `NOT_EXECUTED` or an equivalent project-approved state for absent validation, generation, build or runtime work. Do not write a success state from a planned operation.

## 7. Preserve blockers

Mark the three blocker dimensions independently:

- `PROJECT_INPUT_REQUIRED`: an explicit project object/value/artifact is missing;
- `PROJECT_DESIGN_REQUIRED`: a project decision or architecture choice is missing;
- `EXECUTION_EVIDENCE_REQUIRED`: generated/build/runtime/measurement/verdict/coverage evidence is missing.

An exact generic procedure remains exact when the project value is absent. Conversely, a project value does not upgrade an incomplete reviewed procedure.

## 8. Use the reviewed Vector sub-procedures only as recorded

The fixed reviewed product route includes:

```shell
dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
```

These commands are generic reviewed product sub-procedures. They do not identify a Management ECU project, select a missing value, prove compile/link, or establish runtime behavior.

## 9. Handoff gate

Before handing a row downstream, confirm:

- the task identity is unchanged;
- the exact authority tuple is recorded;
- no project value was inferred;
- the output state is not stronger than its evidence;
- the next owner and required artifact are explicit;
- model, configuration, generation, build, runtime, timing, verdict and coverage remain distinct.

The terminal package is ready for Sol fixed-head review only after the two matrices and nine-path allowlist validation pass.
