# Management ECU — DEM Fault Management Engineering

Date: 2026-09-04

Status: **SOL_REVIEWED_CURRENT_PACKAGE / PUBLICATION_STAGING_APPROVED**

## Purpose

This project provides an engineering and tool-use reference for AUTOSAR Classic DEM-centered fault management on a Management ECU. It does not invent ECU fault policy, DTC values, monitor behavior, or test acceptance. It makes the lifecycle, ownership, tool operations, artifacts, states, evidence, and project-input boundaries explicit enough to navigate from a monitored fault condition to DEM configuration, persistent fault memory, tester-visible DTC behavior, and verification evidence.

## Canonical engineering lifecycle

```text
physical / logical fault condition
  -> Application monitor / detection logic
  -> monitor result / diagnostic event reporting contract
  -> DEM event processing
  -> debounce / qualification / status evolution
  -> DTC relation + event-related data
  -> event-memory / persistence behavior
  -> DCM client access to DEM for tester-facing DTC services
  -> UDS 0x19 / 0x14 observable behavior
  -> CANoe / DiVa execution and result evidence
```

Supporting concerns remain separate:

```text
DEM state -> FiM function-permission/inhibition
DEM persistence -> NvM storage support
Simulink Fault Analyzer fault injection -> model-level injected-fault evidence
```

## Hard boundaries

- physical/logical fault condition != monitor algorithm != monitor result.
- monitor result != DEM event report != DEM debounce/qualification.
- debounce/qualification != monitor status != event UDS status != DTC status.
- DTC identity != event-memory entry != NvM stored representation.
- DEM event != DTC identity.
- DEM != DCM; DEM != FiM; DEM != NvM.
- DCM tester-facing DTC service processing != DEM fault-memory ownership.
- NvM persistence support != diagnostic-event/DTC semantics.
- FiM function permission/inhibition != DTC status.
- modeled/injected Fault Analyzer fault != DEM DiagnosticEvent.
- fault-injection evidence != DEM state != test verdict != coverage.
- enable condition != storage condition.
- operation cycle != ignition cycle by default.
- ClearDTC != monitor pass != aging != AUTOSAR DEM indicator healing.
- configuration != generated configuration != runtime state != tester response != test verdict/report.
- MIL != SIL != VECU/CANoe execution != physical-SUT evidence.

## Current reviewed authority

### AUTOSAR Classic Platform 4.4.0

`eariver/Research_AUTOSAR_CP_Documents@4eff43bdc4a99f3219104c2b16994a539e0b08eb`

Primary current supplement:

`docs/knowledge/management-ecu-dem-autosar-semantic-depth.md`

This closes the reviewed semantic/configuration model for debounce, cycles/conditions, status layers, Event/DTC relation, event memory, event-related data, aging/healing/ClearDTC boundaries, DEM/NvM ownership, and the AUTOSAR-side configuration checklist without inferring vendor GUI realization.

### Vector

`eariver/Research_Vector_Documents@d922812a20ed1e9669fff45f26aa17791254ae65`

Primary current supplement:

`docs/knowledge/management-ecu-dem-vector-procedure-runtime-test.md`

This provides the reviewed Configurator/MICROSAR bounded realization, vVIRTUALtarget Integration/CANoe runtime route, and DiVa/CANoe test-generation/execution routes while retaining the detailed Configurator and internal-observability gaps.

### MathWorks R2025b

`eariver/Research_MathWorks_Documents@2fb38fe40d87a9cb8e7a22f7fe4a1a6a04354187`

The exact R2025b model/AUTOSAR/MIL/SIL/test/coverage/fault-injection paths are listed in `20260904_ManagementECU_DEM_Fault_Management_Reference_Index.yaml` and `references/authority-pins.yaml`.

## Current package

The current Sol-reviewed package contains:

- `20260904_ManagementECU_DEM_Fault_Management_Methodology.md`
- `20260904_ManagementECU_DEM_Fault_Management_Step_by_Step_Guide.md`
- `20260904_ManagementECU_DEM_Fault_Management_Tool_Task_Reference_Matrix.yaml`
- `20260904_ManagementECU_DEM_State_and_Evidence_Model.md`
- `20260904_ManagementECU_DEM_Fault_Management_Execution_Reference_Guide.md`
- `procedures/20260904_ManagementECU_DEM_Procedure_Coverage_Matrix.yaml`
- `20260904_ManagementECU_DEM_Fault_Management_Reference_Index.yaml`
- `20260904_ManagementECU_DEM_Fault_Management_Compilation_Report.md`
- `procedures/20260904_ManagementECU_DEM_Final_Availability_Overlay.yaml`
- `20260904_ManagementECU_DEM_Fault_Management_Sol_Review.md`

Historical baseline compilation remains under `baseline/` and is not overwritten.

## Final procedure availability

Sol accepted the Luna current-package proposal unchanged:

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

The machine-readable current authority is:

`procedures/20260904_ManagementECU_DEM_Final_Availability_Overlay.yaml`

DFM-000 remains project-input-first. DFM-002 remains project-design-first.

## Retained bounded gaps

- DaVinci Configurator Classic 6.3.10 reviewed HELP does not establish a complete object-by-object DEM procedure for several detailed semantic areas. AUTOSAR ECUC names must not be used to invent Vector GUI routes.
- Dem/NvM Event Memory Blocks Assistant is bounded mapping evidence, not a complete DEM procedure.
- vVIRTUALtarget `Integration` is the canonical virtual-ECU route; BSW Emulation is not substituted.
- CANoe tester-visible DTC response is not proof of internal DEM debounce, event-memory entry, or NvM stored representation. Direct internal observation requires a project-authorized instrumentation bridge.
- Actual vVIRTUALtarget/CANoe execution, DiVa generation, and CANoe import/recompile/execution/result/report require project inputs.
- No one universal cross-product Test Unit package/build/runtime contract is established in the reviewed documentation scope; DiVa generation and CANoe product-local import/execution remain separately valid routes.

These are documentation/observability boundaries, not assertions that the products lack the capabilities.

## Project-input rule

Do not infer or invent:

- DiagnosticEvent IDs/names or DTC values/formats/mappings;
- monitor algorithm, pass/fail policy, runnable/callback mapping;
- debounce route/threshold/timing;
- operation-cycle physical meaning;
- enable/storage-condition values;
- confirmation/aging/healing parameters;
- event-memory destination/size/priority/displacement;
- freeze-frame/extended-data content;
- NvM block identity/layout/CRC;
- FiM FID/Event relation;
- DCM session/security/NRC policy;
- CAN addressing, qualifier/variant;
- fault stimulus, expected status transition, test vector, tolerance, or acceptance criteria;
- actual project tool versions.

These remain explicit project inputs/design decisions until supplied and reviewed.

## Scope

Detailed included/excluded scope and task namespace `DFM-000` through `DFM-019` are defined in `20260904_ManagementECU_DEM_Fault_Management_Project_Scope.md`.

## Publication

Private management branch:

`work/management-ecu-dem-fault-management-engineering-20260904`

Prepared/staging Public branch:

`publish/management-ecu-dem-fault-management-engineering-20260904`

The current Sol-reviewed package is approved for byte-identical staging to the prepared Public branch. Internal Luna plans/prompts/worklogs/checkpoints/observations, raw vendor/standard sources, canonical upstream `docs/knowledge/**` bodies, and confidential project values are excluded. Public `main` must not be merged without explicit human approval.
