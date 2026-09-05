# Management ECU OS / RTE Timing & Scheduling Project Scope

Date: 2026-09-05

## 1. Objective

Build a bounded, source-explicit engineering baseline for Management ECU AUTOSAR Classic OS/RTE execution, timing and scheduling behavior while preserving the distinction between design-time SW-C/RTE model semantics, generated RTE realization, OS runtime objects/configuration, timing requirements/models and measured execution evidence.

This baseline is a decomposition/navigation artifact. It does not claim project-specific scheduling feasibility, generated correctness, deadline satisfaction, target timing or safety sufficiency.

## 2. In scope

- SW-C behavior to RunnableEntity and RTEEvent activation semantics at reviewed depth.
- Runnable category/activation constraints where source-explicit.
- RTE generation and Runnable-to-Task realization boundary.
- Basic/Extended Task and OS Event semantics.
- Task activation, priority/preemption and scheduling semantics only where reviewed authority supports them.
- ISR/Task distinction and Category 2 protection boundary where reviewed authority supports it.
- Counter, Alarm and ScheduleTable ownership and time-driven execution path.
- Resource, Spinlock and multicore locality/cross-core service boundaries.
- OS-Application, memory/access/timing protection and ProtectionHook recovery boundary.
- SchM/ExclusiveArea as a separate integration concern; no identity/mapping inference from OS Resource or Spinlock.
- TIMEX observable events/event chains and timing constraints.
- Timing-analysis requirements/model/analysis/verification work-product separation.
- Configuration/generation/build/tool procedure availability as a separate maturity axis.
- Runtime activation/dispatch/preemption/blocking/completion/timing evidence and requirement/verdict/coverage separation.

## 3. Out of scope for this baseline

- invention of Management ECU Runnable, RTEEvent, Task, ISR, Counter, Alarm, ScheduleTable, Resource, Spinlock, OS-Application or SchM identities;
- invention of priorities, periods, offsets, activation limits, core assignment or event masks;
- automatic derivation of Task priorities/mappings from TIMEX constraints;
- WCET/BCET/deadline/jitter/CPU-utilization values without project evidence;
- exact DaVinci Configurator Classic/MICROSAR procedure without reviewed product/release authority;
- assuming SchM ExclusiveArea is realized by a particular OS Resource/Spinlock;
- generated-RTE/OS acceptance without generation/build evidence;
- target timing claims from MIL/SIL/VECU results;
- runtime deadline/verdict/coverage claims without observed evidence;
- project safe-state or safety-case conclusions from OS ProtectionHook mechanics alone.

## 4. Canonical engineering chain

Use this navigation model without collapsing adjacent artifacts:

```text
SW-C behavior
-> RunnableEntity
-> RTEEvent
-> generated RTE activation / mapping realization
-> OS Task / ISR execution context
-> Counter / Alarm / ScheduleTable where applicable
-> priority / preemption / Resource / multicore / Spinlock
-> SchM / ExclusiveArea where separately established
-> generated/compiled/linked implementation
-> runtime activation
-> dispatch/start
-> preemption/blocking
-> completion
-> measured response/execution timing
-> timing requirement comparison
-> verdict
-> coverage
```

## 5. Mandatory task set

The first Luna baseline compilation must contain exactly these 18 task identities and must not add a nineteenth task.

- `OSRTE-001` architecture, ownership and execution-chain baseline
- `OSRTE-002` RunnableEntity semantics, category and activation/concurrency constraints
- `OSRTE-003` RTEEvent and TimingEvent activation semantics
- `OSRTE-004` Runnable-to-Task mapping and generated RTE activation boundary
- `OSRTE-005` Basic/Extended Task lifecycle, activation and OS Event wait/set semantics
- `OSRTE-006` Task priority, preemption and scheduling semantics
- `OSRTE-007` ISR category/priority/source and Task boundary
- `OSRTE-008` OS Counter and tick-domain semantics
- `OSRTE-009` Alarm expiry and configured action semantics
- `OSRTE-010` ScheduleTable expiry points, actions and synchronization boundary
- `OSRTE-011` OS Resource and local mutual-exclusion boundary
- `OSRTE-012` SchM / ExclusiveArea integration and mapping boundary
- `OSRTE-013` multicore core assignment, locality and cross-core Task/Event activation
- `OSRTE-014` Spinlock and cross-core mutual-exclusion boundary
- `OSRTE-015` OS-Application, memory/timing protection and recovery boundary
- `OSRTE-016` RTE/OS configuration, generation, compile/link and vendor-procedure availability
- `OSRTE-017` timing requirements, event chains, constraints, models and analysis/realization boundary
- `OSRTE-018` runtime scheduling/timing observation, measurement, verdict and coverage evidence

## 6. Hard semantic boundaries

The compilation must preserve all of the following.

1. RunnableEntity != OS Task.
2. RTEEvent != OS Event or other OS runtime object.
3. Runnable-to-Task mapping != Task runtime execution.
4. Task configuration != observed execution trace.
5. task priority != actual scheduling outcome.
6. core assignment != timing proof.
7. period / offset / activation != WCET.
8. WCET estimate/model != measured execution time.
9. Counter != Alarm != ScheduleTable.
10. Counter/Alarm/ScheduleTable configuration != observed wake-up timing.
11. OS Resource != Spinlock != SchM ExclusiveArea.
12. ISR != Task.
13. ISR category/priority != Runnable scheduling semantics.
14. multicore mapping != cross-core synchronization correctness.
15. OS-Application != CPU core.
16. OS timing protection != general deadline monitoring or WdgM Deadline Supervision.
17. memory/timing protection configuration != proven runtime containment.
18. timing constraint != OS Task priority/mapping/configuration.
19. TimingDescriptionEvent/EventChain != runtime callback/probe/timestamp provider.
20. configuration != RTE/OS generation != compile/link != runtime scheduling trace.
21. measured timing != timing requirement != verdict != coverage.
22. MIL/SIL/VECU timing != physical-target timing.

Generated mapping may relate these artifacts but does not collapse their identities.

## 7. Project-owned inputs that must not be invented

- SW-C and Runnable identities
- Runnable categories and multiple-instantiation/concurrency policy
- RTEEvent identities and event kinds
- TimingEvent period/offset values
- Runnable-to-Task mappings
- Task IDs/names and Basic/Extended type
- task activation count/limit
- task priority and preemption policy
- task period and offset
- task core assignment
- OS Event identities/masks and wait/set mapping
- ISR identity/category/priority/source/core
- Counter identity, tick duration/frequency and driver source
- Alarm identity, timing values and expiry action
- ScheduleTable identity, expiry points/actions and synchronization policy
- Resource identity, ownership and ceiling/priority semantics
- Spinlock identity/order and protected data
- cross-core protection design
- OS-Application identity/core relation
- memory/access region and trusted/non-trusted policy
- OS timing-protection budgets and recovery policy
- SchM ExclusiveArea identity and SchM-to-OS mapping
- WCET / BCET
- deadlines and latency/age constraints
- jitter bounds
- response-time budgets
- CPU-utilization targets
- expected scheduling trace
- actual Vector/MICROSAR/DaVinci release and packages
- compiler/linker/build baseline
- target/VECU execution environment
- test stimuli and instrumentation
- acceptance thresholds and verdict criteria
- coverage requirement and observed coverage

## 8. Authority use

Use only exact-pinned reviewed authority declared in `references/authority-pins.yaml` for technical claims during the first Luna compilation.

Do not use raw AUTOSAR PDFs, floating upstream heads, Web/current vendor documentation, generic model knowledge or sibling worklogs/prompts as technical authority in that unit.

The exact-pinned reviewed AUTOSAR corpus supports substantial architecture/workflow depth. It does not establish Management ECU values, a complete product-specific configuration procedure, a complete SchM/ExclusiveArea authority for this project, or runtime evidence.

## 9. Completion criteria for baseline compilation

The first Luna unit is complete when it produces exactly four allowlisted outputs containing:

- one current baseline row for every `OSRTE-001` through `OSRTE-018`;
- exact-pinned provenance per supported row;
- explicit authority/procedure/project-input/execution gaps;
- preserved semantic boundaries;
- no invented Management ECU configuration values;
- a future research-gap decomposition;
- a human-readable synthesis and completion checkpoint;
- validated task cardinality and write allowlist.

A local gap such as `OSRTE-012` must not downgrade independent reviewed OS/RTE architecture. Missing exact vendor procedure must not be replaced by an inferred procedure from AUTOSAR semantics.
