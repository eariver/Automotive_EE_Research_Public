# Publication — Management ECU DEM Fault Management Engineering

Status: **SOL_REVIEWED_STAGED**

This branch contains the Sol-reviewed, publication-staged technical package for Management ECU DEM Fault Management Engineering.

## Accepted Private source

- repository: `eariver/Automotive_EE_Engineering_Knowledge`
- branch: `work/management-ecu-dem-fault-management-engineering-20260904`
- accepted source HEAD: `b7d6e645db359416fe848608b5b7a5fd8134d4f9`
- Luna current-package terminal: `283409a12eca334a619daccdf2733726e503cc09`

The source-derived files in this Public package are byte-identical to the accepted Private source.

## Current authority

Final procedure availability is defined by:

`procedures/20260904_ManagementECU_DEM_Final_Availability_Overlay.yaml`

Current counts:

```text
EXACT_PROCEDURE_AVAILABLE     1
PARTIAL_PROCEDURE_AVAILABLE  12
WORKFLOW_ONLY                 3
NO_EXPLICIT_PROCEDURE         2
PROJECT_INPUT_REQUIRED        1
PROJECT_DESIGN_REQUIRED       1
-------------------------------
total                        20
```

The fixed-head Sol review is:

`20260904_ManagementECU_DEM_Fault_Management_Sol_Review.md`

## Publication bundle

The staged source-derived bundle contains 14 files:

- project README and Project Scope;
- Methodology;
- Step-by-Step Guide;
- Tool / Task / Reference Matrix;
- DEM State & Evidence Model;
- Execution Reference Guide;
- Procedure Coverage Matrix;
- Reference Index;
- Compilation Report;
- Sol final availability overlay;
- Sol fixed-head review;
- exact authority pins;
- publication-safe project-input baseline.

Publication metadata adds 2 files, for a total package count of 16.

## Retained boundaries

- Configurator 6.3.10 reviewed HELP does not establish a complete object-by-object DEM procedure for several detailed semantic areas.
- Dem/NvM Event Memory Blocks Assistant is bounded mapping evidence only.
- vVIRTUALtarget `Integration` is the canonical virtual-ECU route for this project.
- tester-visible DTC behavior is not proof of internal DEM debounce, event-memory entry, or NvM representation;
- actual runtime/test execution remains project-input-first;
- no one universal cross-product Test Unit package/build/runtime contract is established in the reviewed documentation scope.

These are documentation/observability boundaries, not capability negatives.

## Exclusions

This Public package excludes:

- Luna plans, prompts, worklogs, checkpoints and observations;
- historical baseline research artifacts not needed for current consumption;
- raw Vector HELP and raw AUTOSAR documents;
- canonical upstream `docs/knowledge/**` bodies;
- confidential project values or fabricated examples.

## Main branch gate

Public `main` is not merged by this staging operation. Any merge to `main` requires explicit human approval.
