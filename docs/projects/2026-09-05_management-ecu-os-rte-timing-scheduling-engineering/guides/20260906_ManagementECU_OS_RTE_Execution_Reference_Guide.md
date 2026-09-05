# Management ECU OS / RTE Timing & Scheduling — Execution Reference Guide

## 1. How to use this guide

Start with the task identity in the two YAML matrices, load its exact authority tuple, then use the row's input/state, operation, output/state and handoff fields. Do not add a project value while following a generic route.

## 2. Task route reference

| Task | Engineering route | Current package use |
|---|---|---|
| OSRTE-001 | architecture, ownership and execution-chain baseline | navigate layers and evidence states |
| OSRTE-002 | RunnableEntity category and activation/concurrency | accept SW-C model constraints |
| OSRTE-003 | RTEEvent/TimingEvent activation | separate activation and timing-observation models |
| OSRTE-004 | Runnable-to-Task mapping / generated RTE boundary | use reviewed Task Mapping procedure; project mapping remains open |
| OSRTE-005 | Basic/Extended Task and OS Event | preserve Task/Event lifecycle and wait/set distinction |
| OSRTE-006 | priority, preemption and scheduling | preserve configuration/outcome separation |
| OSRTE-007 | ISR category/source/priority and Task boundary | keep ISR and Task/protection scope separate |
| OSRTE-008 | OS Counter and tick domain | trace Counter ownership and increment source |
| OSRTE-009 | Alarm expiry and action | trace Counter-to-Alarm-to-action path |
| OSRTE-010 | ScheduleTable expiry points/actions | trace one driving Counter and ordered expiry actions |
| OSRTE-011 | local OS Resource | trace local mutual exclusion without SchM inference |
| OSRTE-012 | SchM/ExclusiveArea integration | preserve product-documentation negative and separate realization ledger |
| OSRTE-013 | multicore/core assignment/cross-core activation | preserve owner core and sync/async service distinction |
| OSRTE-014 | cross-core Spinlock | preserve acquisition/release and local Resource distinction |
| OSRTE-015 | OS-Application and protection/recovery | separate OS reaction from project safe state |
| OSRTE-016 | configuration/generation/build handoff | use exact subcommands while retaining aggregate partial maturity |
| OSRTE-017 | timing requirements/models/analysis | keep constraints separate from OS configuration and measurement |
| OSRTE-018 | runtime observation/verdict/coverage | require the complete execution-evidence chain |

## 3. Reviewed product procedure route

The Sol-reviewed DaVinci Configurator Classic 6.3.10 package exposes the following generic surfaces:

- Task Mapping map/unmap/reorder, including `Requires Mapping`, `Show Unmapped Only`, `Priority`, `OS Application`, `Core Assignment` and `Trigger Conditions`;
- OS Core, OS Application, Task, ISR, Event, Counter, Alarm, ScheduleTable/Expiry Points, Resource, Spin Lock, Memory Protection and timing/resource-lock surfaces;
- project validation;
- BSW/RTE generation;
- schema generation;
- bounded CI/build handoff wording involving DaVinci Team, Gradle, Bazel and RTE generation.

The exact reviewed commands are:

```shell
dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
```

The reviewed validation/generation success states are `Validation Successful` and `Generation Successful`; schema output is documented under `/Output/Schema`. These are product workflow states, not runtime proof.

## 4. Handoff records

### 4.1 Model-to-configuration handoff

Required: accepted SW-C/RTE model, project mapping design, OS object design and explicit toolchain/project inputs.
Not established by this package: actual Runnable, Task, Event, ISR, core, priority, period or mapping values.

### 4.2 Configuration-to-generation handoff

Required: exact project configuration, validation result, generation invocation and generated artifact inventory.
Not established by this package: generated Management ECU file/symbol identity or generated-code inspection.

### 4.3 Generation-to-build handoff

Required: generated RTE/OS/BSW artifacts, compiler/linker baseline, build variant, compile/link logs and binary identity.
Not established by this package: compiler/linker choice, build result or deployment identity.

### 4.4 Build-to-runtime handoff

Required: executable target/environment, instrumentation, runtime stimulus and trace correlation.
Not established by this package: dispatch, preemption, blocking, mutual exclusion, protection or timing results.

### 4.5 Observation-to-verdict handoff

Required: measurement method, accepted timing/protection requirement, comparison rule, verdict record and coverage denominator/result.
Not established by this package: acceptance criteria, verdict, coverage or physical-target correlation.

## 5. Special handling

### OSRTE-004

The product operation is exact at reviewed scope. Actual Management ECU mapping and activation remain project input/design and must not be inferred.

### OSRTE-006

The `Priority` display is retained as `SURFACE_ONLY`; it is not a complete priority/preemption procedure or runtime schedule.

### OSRTE-012

The AUTOSAR semantic authority is reviewed. The Vector product route remains `NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE`. The RTE/service-component surface is supporting context only. Do not infer `RteExclusiveAreaImplMechanism` or a Resource/Spinlock/interrupt mapping.

### OSRTE-016

Validation, generation and schema commands are exact sub-procedures. The aggregate remains `PARTIAL_PROCEDURE_AVAILABLE` because complete OS/RTE diagnostics, generated-file manifest, compile/link ownership and runtime evidence are not established.

### OSRTE-017

Timing constraints and event chains guide realization and analysis; they do not directly assign OS priority, Task mapping, WCET or acceptance thresholds.

### OSRTE-018

Do not close runtime evidence from generic validation/generation. Required layers are configured intent, generated artifact, compile/link, runtime trace, measurement, requirement comparison, verdict and coverage.

## 6. Stop conditions

Stop the current package route for a task when:

- the exact authority tuple cannot be resolved;
- a project-specific value would have to be guessed;
- an unsupported product step would have to be invented;
- an upstream state would be promoted without its independent evidence;
- the task would exceed OSRTE-001–018 or the nine-path output allowlist.

Local project blockers are recorded and handed off; they do not reopen generic research.
