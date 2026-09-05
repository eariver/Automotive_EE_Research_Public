# Publication — Management ECU NvM Memory Persistence Engineering

Status: **SOL_REVIEWED_STAGED**

This branch contains the Sol-reviewed, publication-staged technical package for Management ECU NvM Memory Persistence Engineering.

## Accepted Private source

- repository: `eariver/Automotive_EE_Engineering_Knowledge`
- branch: `work/management-ecu-nvm-memory-persistence-engineering-20260905`
- accepted source HEAD: `f0087d5705353a23cc6b45eca34daf2d66a15835`
- Luna current-package terminal: `09b3ced974717f32405e9df35910bd7b82f5c365`

The source-derived files in this Public package are byte-identical to the accepted Private source, except that the Sol review is placed at a publication-facing top-level filename without changing its content.

## Current authority

Final procedure availability is defined by:

`procedures/20260905_ManagementECU_NvM_Final_Availability_Overlay.yaml`

Current primary counts:

```text
EXACT_PROCEDURE_AVAILABLE      0
PARTIAL_PROCEDURE_AVAILABLE   10
WORKFLOW_ONLY                  5
NO_EXPLICIT_PROCEDURE          1
PROJECT_DESIGN_REQUIRED        1
EXECUTION_EVIDENCE_REQUIRED    1
-------------------------------
total                         18
```

All 18 tasks retain unresolved project-input gates as a separate closure dimension.

The fixed-head Sol review is:

`20260905_ManagementECU_NvM_Memory_Persistence_Sol_Review.md`

## Publication bundle

The staged source-derived bundle contains 14 files:

- project README and Project Scope;
- Methodology;
- Step-by-Step Guide;
- Tool / Task / Reference Matrix;
- NvM State & Evidence Model;
- Execution Reference Guide;
- Procedure Coverage Matrix;
- Reference Index;
- Compilation Report;
- Sol final availability overlay;
- Sol fixed-head review;
- exact authority pins;
- publication-safe unresolved project-input baseline.

Publication metadata adds 2 files, for a total package count of 16.

## Retained boundaries

- Application persistence semantics != NvData/ARXML contract != RTE access != NvM configuration.
- NvM != MemIf != Fee != Ea != Fls != Eep.
- NvM NVRAM block != Fee/Ea logical block != Fls/Eep physical storage/address.
- MemIf `DeviceIndex` != NvM Dataset index.
- `NVM_REQ_*` != `MEMIF_JOB_*`.
- Request/job completion does not prove durable persistence or power-loss safety.
- Write protection, write once and block lock remain separate.
- Permanent RAM, temporary RAM and explicit-sync mirror remain separate.
- Generic DaVinci validation/generation does not establish complete NvM configuration, compile/link or runtime persistence.
- Test definition != execution result != verdict != coverage.

## Exclusions

This Public package excludes:

- Luna plans, prompts, worklogs, checkpoints and observations;
- historical baseline/research-gap artifacts not needed for current consumption;
- raw Vector HELP and raw AUTOSAR documents;
- canonical upstream `docs/knowledge/**` bodies;
- confidential project values or fabricated examples.

## Main branch gate

Public `main` is not merged by this staging operation. Any merge to `main` requires explicit human approval.
