# Management ECU OS / RTE Timing & Scheduling — State & Evidence Model

## 1. Purpose

This model prevents a static configuration or generic workflow from being promoted into a generated, executable, measured, or verified state. Each state has its own owner, artifact and evidence requirement.

## 2. Required evidence chain

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

The arrows are handoffs, not proofs. A state can be available while the next state is unresolved or not executed.

## 3. State ledger

| State | Owner/layer | Minimum artifact | What it can establish | What it cannot establish |
|---|---|---|---|---|
| `S0_PROJECT_INTENT` | project/system design | requirement or engineering goal | scope and intended concern | AUTOSAR object identity, mapping or implementation |
| `S1_SWC_RTE_CONTRACT` | SW-C/RTE design | accepted SW-C behavior, RunnableEntity, RTEEvent and timing-model references | model semantics and activation contract | OS Task/Event, generated code or runtime execution |
| `S2_OS_RTE_CONFIGURATION` | ECU integration/configuration | OS/RTE/ECUC configuration values and references | configured intent and object relations | validation, generation, build, runtime or timing result |
| `S3_VALIDATED_CONFIGURATION` | validation tool/process | validation log/result tied to input state | validation status for the checked model/configuration | generated correctness, compile/link or runtime behavior |
| `S4_GENERATED_ARTIFACT` | generator | generated RTE/OS/BSW source/configuration artifact | generation output and traceability to inputs | compile/link success or runtime behavior |
| `S5_COMPILED_LINKED` | build/integration | compiler/linker logs and binary identity | build result for exact inputs/toolchain | runtime schedule, protection, timing or mutual exclusion |
| `S6_RUNTIME_TRACE` | execution/instrumentation | activation/dispatch/preemption/blocking/completion trace | observed runtime events for the executed stimulus | requirement satisfaction, verdict or coverage by itself |
| `S7_MEASURED_OBSERVATION` | timing/protection/trace analysis | measured timing, lock, protection or event observation | observation under stated method/stimulus | requirement definition, verdict or coverage |
| `S8_REQUIREMENT_COMPARISON` | verification/analysis | comparison against accepted requirement/criterion | pass/fail comparison under stated rule | general proof beyond scope and evidence |
| `S9_VERDICT` | verification owner | test/analysis verdict record | stated verdict for stated scope | coverage or physical-target correlation unless separately recorded |
| `S10_COVERAGE` | verification owner | coverage record and denominator | coverage for stated tests/requirements | correctness or timing proof |

## 4. Independent evidence dimensions

The following records are linked, not collapsed:

| Dimension | Example identity | Required separation |
|---|---|---|
| model | `RunnableEntity`, `RTEEvent`, `ExclusiveArea` | model element is not its generated API or OS object |
| OS object | Task, OS Event, Counter, Alarm, ScheduleTable, Resource, Spinlock | OS objects remain distinct from SW-C/RTE and SchM model identities |
| configuration | ECUC/OS/RTE values | configured intent is not validation or runtime evidence |
| generation | generated RTE/BSW/OS source/configuration | generated output is not compile/link or runtime proof |
| build | compile/link result and binary identity | build success is not schedule/timing/mutual-exclusion proof |
| runtime | trace of activation, dispatch, preemption, blocking, completion | trace is not a requirement, verdict or coverage record |
| timing | requirement, model, measured observation, analysis report | measured timing is not a requirement or verdict |
| protection | OS-Application/protection configuration and fault reaction | OS reaction is not project safe-state policy |
| verification | comparison, verdict, coverage | verdict and coverage are independent outputs |

## 5. ExclusiveArea realization ledger

For OSRTE-012, maintain at least these linked records:

1. semantic/model identity;
2. SW-C or BSW owner context;
3. access-context relations;
4. ECUC definition availability;
5. project configuration values;
6. selected realization mechanism;
7. vendor procedure evidence;
8. generated artifact;
9. compile/link result;
10. runtime mutual-exclusion trace;
11. timing comparison;
12. verdict;
13. coverage.

The conditional AUTOSAR mechanism alternatives remain alternatives, not aliases:

```text
ALL_INTERRUPT_BLOCKING
OS_INTERRUPT_BLOCKING
OS_RESOURCE
OS_SPINLOCK
NONE
RTE_PLUGIN
```

No universal mapping from ExclusiveArea to Resource, Spinlock or interrupt control is allowed. `SchM` is not the OS scheduler.

## 6. State transition gates

| Transition | Required independent evidence |
|---|---|
| `S0 -> S1` | accepted model/contract and owner-context identity |
| `S1 -> S2` | project mapping/configuration design and explicit values |
| `S2 -> S3` | validation execution tied to exact input/configuration |
| `S3 -> S4` | generation execution and generated artifact inventory |
| `S4 -> S5` | compile/link execution, toolchain and binary identity |
| `S5 -> S6` | executable target/environment and runtime instrumentation |
| `S6 -> S7` | stated measurement method, stimulus and trace correlation |
| `S7 -> S8` | accepted requirement/model and comparison rule |
| `S8 -> S9` | verification decision record with scope and result |
| `S9 -> S10` | coverage definition, denominator and executed result |

No transition is implied by the existence of an upstream file alone.

## 7. Non-proof rules

- RunnableEntity is not an OS Task; RTEEvent is not an OS Event.
- Runnable-to-Task mapping is not runtime Task execution.
- Counter, Alarm and ScheduleTable are not one timer identity.
- OS Resource, Spinlock, SchM/ExclusiveArea and interrupt-control remain distinct.
- OS-Application is not CPU core.
- OS timing protection is not WdgM Deadline Supervision.
- configuration, validation, generation, compile/link and runtime trace are distinct.
- measured timing, timing requirement, verdict and coverage are distinct.
- MIL/SIL/VECU timing is not physical-target timing.
