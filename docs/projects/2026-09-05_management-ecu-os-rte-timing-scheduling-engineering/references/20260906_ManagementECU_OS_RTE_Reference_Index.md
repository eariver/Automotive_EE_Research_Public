# Management ECU OS / RTE Timing & Scheduling — Reference Index

Date: 2026-09-06 JST
Status: `LUNA_COMPILE_PROPOSAL`

## 1. Authority selection

Only exact-pinned Sol-reviewed authority is used for technical claims in this package. The project context and project-input baseline are read-only blocker references, not technical authority.

### 1.1 Primary AUTOSAR authority

- Repository: `eariver/Research_AUTOSAR_CP_Documents`
- Exact commit: `938ac4af696d263019ebdc61106a444447e15c4d`
- Platform/release: AUTOSAR Classic 4.4.0
- Review status: `SOL_REVIEWED`

| Reference key | Reviewed Knowledge path | Entry ID | Requirement IDs / scope |
|---|---|---|---|
| `AUTOSAR-RUNNABLE-RTEEVENT-BOUNDARY` | `docs/knowledge/concepts/runnable-rteevent-os-activation-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-RUNNABLE-RTEEVENT-OS-ACTIVATION-BOUNDARY` | SRS_Rte_00134, SRS_Rte_00072, SRS_Rte_00049, SRS_Rte_00092 |
| `AUTOSAR-RTEEVENT-ACTIVATION-TRACE` | `docs/knowledge/workflows/rteevent-to-runnable-activation.json` | `AUTOSAR-CP-4.4.0-WORKFLOW-RTEEVENT-TO-RUNNABLE-ACTIVATION` | SRS_Rte_00072, SRS_Rte_00049, SRS_Rte_00134, SRS_Rte_00092, SRS_Rte_00143 |
| `AUTOSAR-RTE-GENERATION-RUNTIME-BOUNDARY` | `docs/knowledge/concepts/rte-generation-contract-runtime-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-RTE-GENERATION-CONTRACT-RUNTIME-BOUNDARY` | SRS_Rte_00048, SRS_Rte_00021, SRS_Rte_00065, SRS_Rte_00049, SRS_Rte_00027 |
| `AUTOSAR-OS-EXECUTION-BOUNDARY` | `docs/knowledge/concepts/os-execution-lifecycle-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-OS-EXECUTION-LIFECYCLE-BOUNDARY` | SWS_Os_00424, SWS_Os_00425, SWS_Os_00616, SWS_Os_00617, SWS_Os_00621 |
| `AUTOSAR-OS-RUNTIME-OBJECTS` | `docs/knowledge/concepts/os-runtime-object-scheduling-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-OS-RUNTIME-OBJECT-SCHEDULING-BOUNDARY` | SRS_Os_00098, SRS_Os_11020, SWS_Os_00301, SWS_Os_00401–00404, SWS_Os_00409, SWS_Os_00412 |
| `AUTOSAR-OS-COUNTER-ALARM-SCHEDULETABLE` | `docs/knowledge/workflows/os-counter-alarm-scheduletable-execution-path.json` | `AUTOSAR-CP-4.4.0-WORKFLOW-OS-COUNTER-ALARM-SCHEDULETABLE-EXECUTION-PATH` | SRS_Os_11020, SWS_Os_00301, SWS_Os_00401–00404, SWS_Os_00409, SWS_Os_00412 |
| `AUTOSAR-OS-MULTICORE-RESOURCE-SPINLOCK` | `docs/knowledge/concepts/os-multicore-resource-spinlock-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-OS-MULTICORE-RESOURCE-SPINLOCK-BOUNDARY` | SRS_Os_80005, SRS_Os_80015, SRS_Os_80016, SRS_Os_80021, SWS_Os_00598, SWS_Os_00816, SWS_Os_00602, SWS_Os_00817, SWS_Os_00629, SWS_Os_00648, SWS_Os_00649, SWS_Os_00652, SWS_Os_00655, SWS_Os_00694, SWS_Os_00695 |
| `AUTOSAR-OS-CROSS-CORE-TRACE` | `docs/knowledge/workflows/os-multicore-cross-core-synchronization.json` | `AUTOSAR-CP-4.4.0-WORKFLOW-OS-MULTICORE-CROSS-CORE-SYNCHRONIZATION` | SRS_Os_80005, SRS_Os_80015, SRS_Os_80016, SRS_Os_80021, SWS_Os_00598, SWS_Os_00816, SWS_Os_00602, SWS_Os_00817, SWS_Os_00629, SWS_Os_00634, SWS_Os_00648, SWS_Os_00649, SWS_Os_00652, SWS_Os_00655 |
| `AUTOSAR-OS-APPLICATION-PROTECTION` | `docs/knowledge/concepts/os-protection-osapplication-recovery-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-OS-PROTECTION-OSAPPLICATION-RECOVERY-BOUNDARY` | SRS_Os_11008, SRS_Os_11013, SRS_Os_11014, SWS_Os_00028, SWS_Os_00064, SWS_Os_00465, SWS_Os_00466, SWS_Os_00210, SWS_Os_00033, SWS_Os_00037, SWS_Os_00107, SWS_Os_00553–00555 |
| `AUTOSAR-OS-PROTECTION-RECOVERY` | `docs/knowledge/workflows/os-protection-violation-to-recovery-action.json` | `AUTOSAR-CP-4.4.0-WORKFLOW-OS-PROTECTION-VIOLATION-TO-RECOVERY-ACTION` | SWS_Os_00064, SWS_Os_00465, SWS_Os_00466, SWS_Os_00210, SWS_Os_00033, SWS_Os_00037, SWS_Os_00107, SWS_Os_00553–00555 |
| `AUTOSAR-OS-TIME-DOMAIN` | `docs/knowledge/concepts/os-counter-swfrt-time-service-stbm-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-OS-COUNTER-SWFRT-TIME-SERVICE-STBM-BOUNDARY` | SRS_Os_11002, SRS_Os_11020, SWS_Os_00409, SRS_Frt_00020, SRS_Frt_00033, SRS_Frt_00047, SWS_Tm_00001, SWS_Tm_00009, SWS_Tm_00019, SWS_Tm_00023 |
| `AUTOSAR-TIMING-EVENT-CHAIN` | `docs/knowledge/concepts/timing-event-chain-observation-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-TIMING-EVENT-CHAIN-OBSERVATION-BOUNDARY` | TPS_TIMEX_00001, TPS_TIMEX_00002 |
| `AUTOSAR-TIMING-CONSTRAINT-REALIZATION` | `docs/knowledge/concepts/timing-constraint-runtime-realization-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-TIMING-CONSTRAINT-RUNTIME-REALIZATION-BOUNDARY` | TPS_TIMEX_00003–00008, TPS_TIMEX_00037, TPS_TIMEX_00054 |
| `AUTOSAR-TIMING-REALIZATION-TRACE` | `docs/knowledge/workflows/timing-constraint-to-runtime-realization.json` | `AUTOSAR-CP-4.4.0-WORKFLOW-TIMING-CONSTRAINT-TO-RUNTIME-REALIZATION` | TPS_TIMEX_00034, TPS_TIMEX_00036, TPS_TIMEX_00037, TPS_TIMEX_00007, TPS_TIMEX_00008 |
| `AUTOSAR-TIMING-ANALYSIS-WORK-PRODUCTS` | `docs/knowledge/concepts/timing-analysis-work-product-boundary.json` | `AUTOSAR-CP-4.4.0-CONCEPT-TIMING-ANALYSIS-WORK-PRODUCT-BOUNDARY` | timing requirements/model/analysis/verification work-product boundary |

The authority catalog in both machine-readable matrices adds the exact blob SHA for every entry.

### 1.2 Focused SchM authority

- Repository: `eariver/Research_AUTOSAR_CP_Documents`
- Exact commit: `3eec41439f25f61c29e0c1a06a51df148e493014`
- Path: `docs/knowledge/management-ecu-os-rte-schm-autosar-semantic-depth.md`
- Blob SHA: `9d43ebda90be848232054d953887ff6b98f5f89c`
- Release: AUTOSAR Classic 4.4.0
- Review status: `SOL_REVIEWED`
- Scope: SW-C/BSW ExclusiveArea identity, SchM API boundary, conditional realization and evidence-layer checklist.

### 1.3 Vector/MICROSAR authority

- Repository: `eariver/Research_Vector_Documents`
- Exact commit: `7285e6a773433488c59186bbd241bdab39efb4ce`
- Path: `docs/knowledge/management-ecu-os-rte-vector-procedure.md`
- Blob SHA: `9dba28ab75b9f1ae9f58350e085ffa3291188bb5`
- Product scope: DaVinci Configurator Classic 6.3.10 / MICROSAR Classic configuration, validation and generation surfaces.
- Review status: `SOL_REVIEWED`

This authority supplies the carried-forward product maturity for OSRTE-004–016. It is not reclassified in this compilation.

### 1.4 Project references

- Downstream context: `eariver/Automotive_EE_Engineering_Knowledge@e616fce2fb8f2e906a7e77662c89c5f633f82355`, read-only.
- Project-input baseline: `docs/projects/2026-09-05_management-ecu-os-rte-timing-scheduling-engineering/references/project/os-rte-timing-scheduling-project-input-baseline.yaml`, status `UNRESOLVED_PROJECT_INPUT`.

Project references identify missing inputs; they do not authorize default values or new technical claims.

## 2. Sol-reviewed Vector procedure surfaces carried forward

- Task Mapping: `Requires Mapping`, `Show Unmapped Only`, Selection Area to Overview Area drag mapping, `Unmap`, reorder, and `Priority`/`OS Application`/`Core Assignment`/`Trigger Conditions` display columns.
- OS configuration: Core, OS-Application, Task, ISR, OS Event, Counter, Alarm, ScheduleTable/Expiry Points, Resource, Spin Lock, Memory Protection and timing/resource-lock-related surfaces.
- Validation: `dvcfg-b project validate`.
- Generation: `dvcfg-b project generate`.
- Schema generation: `dvcfg-b project generate-schema` with `/Output/Schema` output.
- Build handoff: bounded DaVinci Team, Gradle, Bazel, RTE generation trigger and basic-software compilation wording.

The exact commands and their product scope are documented in the Vector Reviewed Knowledge tuple above. They do not select project values or prove runtime behavior.

## 3. Retained documentation negatives

The following are documentation-scope negatives, not product capability-absence claims:

- no exact reviewed `RteExclusiveAreaImplMechanism` Configurator field;
- no exact SchM/ExclusiveArea object-by-object realization procedure;
- no exact ExclusiveArea-to-Resource/Spinlock/interrupt-control mapping procedure;
- no complete Basic/Extended Task, activation-limit, priority/preemption procedure;
- no complete Resource ceiling/use or Spinlock ordering/successor/nesting procedure;
- no complete protection-budget/ProtectionHook/recovery procedure;
- no complete OS/RTE-specific diagnostic catalogue, generated-file manifest or build manifest;
- no Management ECU compiler/linker/binary/deployment/runtime evidence.

## 4. Non-authority and non-collapse rules

No Vector product path is inferred from an AUTOSAR semantic name. Preserve:

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
