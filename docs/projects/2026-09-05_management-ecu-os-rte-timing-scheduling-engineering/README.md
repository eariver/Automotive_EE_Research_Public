# Management ECU — OS / RTE Timing & Scheduling Engineering

Date: 2026-09-05

## Purpose

This project establishes a provenance-preserving engineering baseline for Management ECU OS / RTE timing and scheduling behavior in AUTOSAR Classic.

The project separates SW-C behavior, RunnableEntity and RTEEvent modeling, generated RTE realization, OS Task/ISR scheduling objects, Counter/Alarm/ScheduleTable time-driven activation, Resource/Spinlock/multicore protection, OS-Application protection, timing requirements/models, and runtime timing evidence.

This baseline is a decomposition and navigation artifact. It is not a claim that Management ECU-specific Runnable-to-Task mapping, task priorities, periods, core assignment, WCET, deadlines, generated RTE/OS configuration, or runtime scheduling behavior has been validated.

## Current state

Status: `SOL_BASELINE_INITIALIZED`

No Luna baseline compilation has been executed yet. No Management ECU-specific OS/RTE/timing value is accepted by this initialization.

Inherited downstream source:

- repository: `eariver/Automotive_EE_Engineering_Knowledge`
- branch: `work/management-ecu-nvm-memory-persistence-engineering-20260905`
- exact inherited head: `f0087d5705353a23cc6b45eca34daf2d66a15835`

Sol project branch:

- `work/management-ecu-os-rte-timing-scheduling-engineering-20260905`

Planned Luna execution branch:

- `work/luna-management-ecu-os-rte-timing-scheduling-baseline-compilation-20260905`

The exact Luna Starting SHA is the Sol initialization commit containing these control files. It must be supplied externally when the Luna unit is launched; this file does not self-pin that future commit.

## Primary authority

Technical compilation is source-bounded to exact-pinned Sol-reviewed authority in `references/authority-pins.yaml`.

Primary reviewed corpus:

- `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d`
- platform/release: AUTOSAR Classic 4.4.0

The reviewed corpus already provides explicit boundaries for:

- RunnableEntity and RTEEvent model semantics versus OS runtime objects;
- RTE generation versus design-time model entities and generated runtime artifacts;
- Basic/Extended Task, OS Event, Counter, Alarm and ScheduleTable ownership;
- OS execution/lifecycle substrate;
- multicore locality, cross-core activation, Resource and Spinlock separation;
- OS-Application, memory/timing protection and ProtectionHook recovery;
- OS Counter versus SWFRT/Tm/StbM time-domain separation;
- timing-description events/event chains;
- timing constraints versus runtime realization;
- timing-analysis work products;
- workflows for RTEEvent-to-Runnable activation, Counter/Alarm/ScheduleTable execution, multicore synchronization, OS protection recovery and timing-constraint realization.

The reviewed corpus does not by itself establish:

- Management ECU-specific mappings or configuration values;
- an exact project-specific DaVinci Configurator Classic / MICROSAR OS/RTE GUI/CLI procedure;
- a complete pinned SchM/ExclusiveArea semantic/procedure authority for this project;
- generated/build correctness;
- actual runtime scheduling/timing evidence.

## Project control files

- `20260905_ManagementECU_OS_RTE_Timing_Scheduling_Project_Scope.md`
- `references/authority-pins.yaml`
- `references/project/os-rte-timing-scheduling-project-input-baseline.yaml`
- `luna/2026-09-05_os-rte-timing-scheduling-baseline-compilation-plan.md`
- `luna/2026-09-05_os-rte-timing-scheduling-baseline-compilation-instruction.md`
- `../../prompts/2026-09-05_luna-management-ecu-os-rte-timing-scheduling-baseline-compilation.md`

## Canonical navigation model

```text
SW-C behavior
-> RunnableEntity
-> RTEEvent
-> RTE generation / task mapping realization
-> OS Task or ISR execution context
-> Counter / Alarm / ScheduleTable where time-driven
-> priority / preemption / Resource / multicore / Spinlock
-> SchM / ExclusiveArea only where separately established
-> compiled/linked runtime
-> observed activation / dispatch / preemption / blocking / completion
-> measured timing
-> requirement comparison
-> verdict / coverage
```

This is a navigation model, not a project-specific mapping.

## Non-collapse rules

Do not collapse:

- RunnableEntity != OS Task;
- RTEEvent != OS Event or other OS activation object;
- Runnable-to-Task mapping != Task runtime execution;
- configured Task != observed execution trace;
- task priority != actual scheduling outcome;
- core assignment != timing proof;
- period / offset / activation != WCET;
- WCET estimate/model != measured execution time;
- Counter != Alarm != ScheduleTable;
- Counter/Alarm/ScheduleTable configuration != observed wake-up timing;
- OS Resource != Spinlock != SchM ExclusiveArea;
- ISR != Task;
- ISR category/priority != Runnable scheduling;
- multicore mapping != cross-core synchronization correctness;
- OS-Application != CPU core;
- memory/timing protection configuration != proven runtime containment;
- TIMEX timing constraint != OS task configuration;
- TimingDescriptionEvent != runtime instrumentation API;
- configuration != generation != compile/link != runtime trace;
- measured execution timing != timing requirement != verdict != coverage;
- MIL/SIL/VECU timing != physical-target timing.

## Project-owned values

Runnable identities, RTEEvent identities, Runnable-to-Task mapping, task identities/types/priorities/activation limits/periods/offsets/core assignment, ISR identities/categories/priorities/sources, Counter/tick configuration, Alarm actions, ScheduleTable expiry points/synchronization, Resource/Spinlock/SchM identities and mappings, OS-Application/protection policy, WCET/BCET/deadline/jitter/response budgets, tool versions, generated artifacts, test vectors, acceptance thresholds, observed traces, verdicts and coverage remain unresolved project inputs until explicitly supplied and accepted.

Unsupported points must remain explicit gaps rather than inferred values or procedures.
