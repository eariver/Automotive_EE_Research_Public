# Publication — Management ECU OS/RTE Timing & Scheduling Engineering

Status: **SOL_REVIEWED_STAGED**

This branch contains the Sol-reviewed, publication-staged technical package for Management ECU OS/RTE Timing & Scheduling Engineering.

## Accepted Private source

- repository: `eariver/Automotive_EE_Engineering_Knowledge`
- branch: `work/management-ecu-os-rte-timing-scheduling-engineering-20260905`
- accepted source HEAD: `161a6cd36bda3ef59ab7ace3e0ef3c69e4e9fd2a`
- Luna current-package terminal reviewed: `154572769446106e98347f6ea5d01ff8352fdcf5`

The current package passed Sol fixed-head review after one administrative path normalization. Luna produced the accepted State & Evidence Model content under a non-canonical filename; Sol reused the exact accepted blob `e4b9e6e367b9cf51c92712474cf0875d3ba480a6` at the canonical publication path:

`models/20260906_ManagementECU_OS_RTE_State_Evidence_Model.md`

No technical content was synthesized to make that normalization.

## Current reviewed maturity

The primary task availability is:

```text
EXACT_PROCEDURE_AVAILABLE                 4
PARTIAL_PROCEDURE_AVAILABLE               8
SURFACE_ONLY                              1
NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE 1
WORKFLOW_ONLY                             4
-------------------------------------------
total                                    18
```

Secondary blockers remain independent:

- `PROJECT_INPUT_REQUIRED`: all 18 tasks;
- `PROJECT_DESIGN_REQUIRED`: 16 tasks;
- `EXECUTION_EVIDENCE_REQUIRED`: OSRTE-018 only.

The fixed-head Sol review is:

`20260906_ManagementECU_OS_RTE_Timing_Scheduling_Sol_Review.md`

Final disposition:

- `GENERIC_OS_RTE_RESEARCH_CLOSED`
- `CURRENT_OS_RTE_ENGINEERING_PACKAGE_SOL_REVIEWED`

## Publication bundle

The staged source-derived bundle contains 13 files:

- project README and Project Scope;
- Methodology;
- Step-by-Step Guide;
- Tool / Task / Reference Matrix;
- State & Evidence Model;
- Execution Reference Guide;
- Procedure Coverage Matrix;
- Reference Index;
- Current Package Compilation Report;
- Sol fixed-head review;
- exact authority pins;
- publication-safe unresolved project-input baseline.

Publication metadata adds 2 files, for a total package count of 15.

## Reviewed authority

Technical claims remain exact-pinned to:

- AUTOSAR CP architecture/workflow: `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d`;
- AUTOSAR SchM / ExclusiveArea semantic depth: `eariver/Research_AUTOSAR_CP_Documents@3eec41439f25f61c29e0c1a06a51df148e493014`;
- Vector/MICROSAR OS/RTE procedure: `eariver/Research_Vector_Documents@7285e6a773433488c59186bbd241bdab39efb4ce`.

## Retained boundaries

- RunnableEntity != OS Task.
- RTEEvent != OS Event.
- Runnable-to-Task mapping != runtime Task execution.
- Counter != Alarm != ScheduleTable.
- OS Resource != Spinlock != SchM/ExclusiveArea != interrupt-control mechanism.
- SW-C ExclusiveArea != BSW ExclusiveArea project identity.
- ExclusiveArea model != RTE/SchM API != selected realization.
- SchM != AUTOSAR OS scheduler.
- OS-Application != CPU core.
- Configuration != validation != generation != compile/link != runtime trace.
- Measured timing != timing requirement != verdict != coverage.
- MIL/SIL/VECU timing != physical-target timing.

## Exclusions

This Public package excludes:

- Luna plans, prompts, instructions, worklogs, observations and historical checkpoints;
- baseline/research-gap artifacts not needed for current package consumption;
- raw Vector HELP and raw AUTOSAR documents;
- canonical upstream `docs/knowledge/**` bodies;
- confidential project values or fabricated examples.

The retained `OSRTE-012` negative is a documentation-scope negative, not a product feature-absence claim.

## Main branch gate

Public `main` is not merged by this staging operation. Any merge to `main` requires explicit human approval.
