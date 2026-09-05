# Management ECU NvM Memory Persistence Engineering

## Purpose

This project establishes a provenance-preserving engineering package for Management ECU persistent-memory behavior in AUTOSAR Classic, centered on NvM and its reviewed lower-memory boundaries.

The project separates application persistence semantics, NvData/RTE-facing contracts, NvM logical NVRAM-block management, MemIf dispatch, Fee/Ea logical-memory abstraction, Fls/Eep device jobs, configuration/generation, and runtime verification evidence.

## Current state

Status: `SOL_REVIEWED_CURRENT_AUTHORITY`

The generic/documentation research and current-package compilation phases are complete for the present authority set.

Current Private project branch:

- `work/management-ecu-nvm-memory-persistence-engineering-20260905`

Accepted current-package Luna terminal:

- `09b3ced974717f32405e9df35910bd7b82f5c365`

Sol final maturity authority:

- `procedures/20260905_ManagementECU_NvM_Final_Availability_Overlay.yaml`

Sol fixed-head review:

- `checkpoints/2026-09-05_sol-nvm-current-package-fixed-head-review.md`

No Management ECU-specific NvM configuration value has been accepted by the research/compilation phases. Project inputs remain unresolved unless supplied separately.

## Reviewed authority

Technical claims are bounded by `references/authority-pins.yaml`.

Primary exact-reviewed authorities are:

- AUTOSAR reviewed base: `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d`
- NvM semantic depth: `eariver/Research_AUTOSAR_CP_Documents@d021e2471b8c76efc6af43f66c17d7ead68821cc`
  - `docs/knowledge/management-ecu-nvm-autosar-semantic-depth.md`
- Vector NvM procedure boundary: `eariver/Research_Vector_Documents@d7eb75af93ac82d155fe508681b7057802c3aa45`
  - `docs/knowledge/management-ecu-nvm-vector-procedure.md`

The reviewed corpus supports architecture/workflow through NvM, MemIf, Fee/Ea and Fls/Eep and bounded DaVinci Configurator Classic 6.3.10 product procedures/surfaces. It does not establish a complete object-by-object NvM Configurator procedure or actual project durability evidence.

## Current package

Current reviewed package outputs are:

- `20260905_ManagementECU_NvM_Memory_Persistence_Methodology.md`
- `20260905_ManagementECU_NvM_Memory_Persistence_Step_by_Step_Guide.md`
- `matrices/20260905_ManagementECU_NvM_Tool_Task_Reference_Matrix.yaml`
- `models/20260905_ManagementECU_NvM_State_Evidence_Model.md`
- `guides/20260905_ManagementECU_NvM_Execution_Reference_Guide.md`
- `matrices/20260905_ManagementECU_NvM_Procedure_Coverage_Matrix.yaml`
- `references/20260905_ManagementECU_NvM_Reference_Index.md`
- `20260905_ManagementECU_NvM_Current_Package_Compilation_Report.md`
- `checkpoints/2026-09-05_nvm-memory-persistence-current-package-compilation-complete.md`

Final task maturity is defined by the Sol overlay, not by the Luna proposal status embedded in the historical compilation outputs.

## Final availability summary

- `EXACT_PROCEDURE_AVAILABLE`: 0
- `PARTIAL_PROCEDURE_AVAILABLE`: 10
- `WORKFLOW_ONLY`: 5
- `NO_EXPLICIT_PROCEDURE`: 1
- `PROJECT_INPUT_REQUIRED`: 0 as the primary availability label
- `PROJECT_DESIGN_REQUIRED`: 1
- `EXECUTION_EVIDENCE_REQUIRED`: 1
- total: 18

All 18 tasks still retain unresolved project-input gates as a secondary closure dimension. `NVM-002` is the primary project-design-gated task and `NVM-018` is the primary execution-evidence-gated task.

## Non-collapse rules

Do not collapse:

- application persistence semantics != NvData/ARXML contract != RTE access != NvM configuration;
- NvM != MemIf != Fee != Ea != Fls != Eep;
- NvM NVRAM block != Fee/Ea logical block != physical flash/EEPROM layout;
- RAM block != NV block != optional ROM/default block != Administrative block;
- request acceptance != NvM request completion != lower-memory job completion != durable physical persistence proof;
- `NVM_REQ_*` != `MEMIF_JOB_*`;
- ReadAll != ReadBlock; WriteAll != WriteBlock;
- changed state != CRC comparison != WriteAll selection != explicit WriteBlock != job priority;
- write protection != write once != block lock;
- permanent RAM != temporary RAM != explicit-sync mirror;
- configuration validation != generation != compile/link != runtime evidence;
- DEM/DID/RID/application persistence policy != intrinsic NvM semantics;
- test definition != execution result != verdict != coverage.

## Project-owned values

Block IDs/sizes, RAM/NV placement, backend selection, CRC policy, block-management type, queue sizing, write frequency/endurance assumptions, startup/shutdown policy, retention/power-loss policy, application/DEM/DCM mappings, actual project tool release, physical-sector layout, stimuli and acceptance vectors remain project input until explicitly supplied and accepted.

## Next frontier

Do not repeat broad AUTOSAR or Vector documentation research under the current source set.

The next meaningful work requires one or more concrete project inputs/artifacts, especially:

- Application/NvData/ARXML/RTE persistence contract;
- NvM block inventory and per-block management/integrity/protection/synchronization choices;
- MemIf/Fee/Ea/Fls/Eep project mapping and physical-memory design;
- startup/shutdown lifecycle design;
- actual DaVinci/MICROSAR project and generated artifacts;
- compile/link/runtime evidence;
- persistent re-read and reset/power-cycle observations;
- interrupted-write/power-loss evidence;
- test verdict and coverage.

Unsupported points remain explicit gaps rather than inferred values or procedures.
