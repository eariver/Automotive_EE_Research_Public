# Management ECU DEM Fault Management — Current Package Compilation Report

Status: **Luna compile proposal; Sol final maturity pending**  
Date: 2026-09-04  
Repository: `eariver/Automotive_EE_Engineering_Knowledge`  
Branch: `work/luna-management-ecu-dem-current-package-compilation-20260904`

## Run identity

- Exact Starting SHA: `b52b51b5546965fdb048ce3c1d8952e993fd153e`
- Starting remote HEAD check: **PASS; exact match confirmed before any write**
- Ending SHA: recorded from the non-force remote read-back in the final handoff
- New branch: none
- New research: **not performed**
- Final maturity: **not assigned; Sol owns final decision**

## Candidate current availability

These are Luna proposals from the exact-pinned compilation. They are not final Sol maturity decisions.

| Task | Proposed current availability |
|---|---|
| DFM-000 | `PROJECT_INPUT_REQUIRED` |
| DFM-001 | `WORKFLOW_ONLY` |
| DFM-002 | `PROJECT_DESIGN_REQUIRED` |
| DFM-003 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-004 | `NO_EXPLICIT_PROCEDURE` |
| DFM-005 | `NO_EXPLICIT_PROCEDURE` |
| DFM-006 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-007 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-008 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-009 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-010 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-011 | `EXACT_PROCEDURE_AVAILABLE` |
| DFM-012 | `WORKFLOW_ONLY` |
| DFM-013 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-014 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-015 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-016 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-017 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-018 | `PARTIAL_PROCEDURE_AVAILABLE` |
| DFM-019 | `WORKFLOW_ONLY` |

Proposed availability counts: `EXACT_PROCEDURE_AVAILABLE=1`, `PARTIAL_PROCEDURE_AVAILABLE=12`, `WORKFLOW_ONLY=3`, `NO_EXPLICIT_PROCEDURE=2`, `PROJECT_INPUT_REQUIRED=1`, `PROJECT_DESIGN_REQUIRED=1`; total **20**.

## Task-by-task current findings

| Task | Current finding and next evidence |
|---|---|
| DFM-000 | Project input baseline is not supplied; freeze exact pins and leave project categories TBD. |
| DFM-001 | Reviewed ownership split is usable as a workflow; project RACI/interfaces remain input. |
| DFM-002 | Application monitor algorithm and result policy require project design; MathWorks fault/model identities do not choose them. |
| DFM-003 | DEM reporting API and bounded Vector integration surfaces exist; production RTE identity remains project-specific. |
| DFM-004 | AUTOSAR debounce semantics are reviewed, but no complete exact Configurator object procedure is established; retain both debounce routes. |
| DFM-005 | Cycle/enable/storage semantics are reviewed, but detailed Configurator mapping and physical cycle meaning remain unresolved/input. |
| DFM-006 | Status API/semantic layers are reviewed; configured transition and callback-timing matrix is not closed. |
| DFM-007 | Event/DTC and combination semantics are reviewed; mapping/combination realization and values are project input. |
| DFM-008 | DEM memory lifecycle is reviewed and Dem/NvM mapping is bounded; capacity/policy and internal entry proof remain open. |
| DFM-009 | Event-data semantic class/trigger model is reviewed; data identity/content/provider and Configurator route remain input/bounded. |
| DFM-010 | Pass, indicator healing, aging and ClearDTC are distinct reviewed concepts; project policy and detailed realization remain open. |
| DFM-011 | AUTOSAR DCM–DEM service workflow is explicit at reviewed generic scope; project service/addressing/condition policy remains input. |
| DFM-012 | FiM consumes DEM status for permission/inhibition; FID/EventID/mask/consumer decisions remain project input. |
| DFM-013 | DEM/NvM semantic boundary and minimum closure evidence are explicit; block allocation/layout/CRC/recovery evidence is project-owned. |
| DFM-014 | Configurator validation/generation and generated BSW/RTE boundary are bounded; complete object-by-object DEM procedure is not established. |
| DFM-015 | R2025b model/Test Manager route is bounded; project monitor vectors, expected results, tolerance and coverage policy are missing. |
| DFM-016 | R2025b generated-code/SIL route is bounded; project code scope/toolchain/tolerance and integration evidence are missing. |
| DFM-017 | vVIRTUALtarget Integration -> CANoe route is explicit; actual runtime requires project package, stimulus, diagnostic context and acceptance. |
| DFM-018 | DiVa generation and CANoe product-local import/execution routes are explicit; actual project generation/execution/result/report requires inputs. |
| DFM-019 | Local routes compose into a workflow, but no project-specific end-to-end evidence bundle or internal observability bridge is supplied. |

All rows and their complete fields are in the two machine-readable matrices. Exact technical provenance is in the Reference Index. `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922] [MW-PROC-2FB]`

## Project blockers

### Candidate label blockers

- `PROJECT_INPUT_REQUIRED`: DFM-000.
- `PROJECT_DESIGN_REQUIRED`: DFM-002.

### Project-input-gated slices

Project-specific binding remains required for DFM-000, DFM-001, DFM-003, DFM-004, DFM-005, DFM-006, DFM-007, DFM-008, DFM-009, DFM-010, DFM-011, DFM-012, DFM-013, DFM-014, DFM-015, DFM-016, DFM-017, DFM-018 and DFM-019. This does not change the proposed availability label where a generic reviewed route exists.

### Project-design-first slices

DFM-002 is explicitly design-first. Its approved monitor behavior is a prerequisite for selecting the debounce ownership route and for interpreting model/reporting evidence. DFM-003, DFM-004, DFM-005, DFM-006, DFM-007, DFM-009, DFM-010, DFM-015, DFM-016 and DFM-019 consume that design intent but are not automatically blocked from their safe product-local compilation surfaces.

## Retained documentation negatives and observability gaps

1. DaVinci Configurator Classic 6.3.10 exact reviewed evidence does not establish a complete object-by-object DEM procedure for the detailed semantic areas. AUTOSAR ECUC names are not used to infer Vector GUI structure.
2. Dem/NvM Event Memory Blocks Assistant evidence is bounded mapping evidence, not complete DEM procedure.
3. The canonical vVIRTUALtarget route is Integration. BSW Emulation is not substituted.
4. CANoe tester-visible DTC response is not proof of internal DEM debounce, event-memory entry or NvM stored representation. A project-specific instrumentation bridge is required; absent one, the slice is an observability gap.
5. Actual vVIRTUALtarget/CANoe execution, DiVa generation and CANoe import/recompile/execution/result/report are project-input-first.
6. No one universal cross-product Test Unit package/build/runtime contract is established. This negative does not stop product-local DiVa generation or CANoe product-local import/execution research.

These are bounded documentation/observability negatives, not claims that the products cannot perform the capability. `[VECTOR-DEM-D922]`

## Semantic contract retained

```text
fault condition != monitor algorithm / implementation != monitor result
!= DEM event report != debounce / qualification != monitor status
!= event UDS status != DTC status != DTC identity != event-memory entry
!= NvM representation != DCM tester response != test definition
!= execution != verdict != report
```

Also retained: `Event != DTC`; `DEM != DCM`; `DEM != FiM`; `DEM != NvM`; `enable condition != storage condition`; `operation cycle != ignition cycle by default`; `ClearDTC != monitor pass`; `ClearDTC != aging`; `ClearDTC != AUTOSAR DEM indicator healing`; `configuration != generated configuration != runtime state != tester response`; and `verdict != coverage`. `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922] [MW-TEST-2FB] [MW-COVERAGE-2FB]`

## Validation result

The repository-side pre-commit draft validation is **PASS**. It confirmed:

- each task is present exactly once in the Tool / Task / Reference Matrix;
- each task is present exactly once in the Procedure Coverage Matrix;
- availability counts sum to 20 and use only the six allowed labels;
- every technical claim resolves to an exact reviewed authority tuple;
- project input/design blockers and all retained boundaries remain visible;
- no new technical evidence, Web, raw HELP, current source or floating upstream source was used;
- the changed path set is exactly the nine-file allowlist;
- Configurator bounded gap, internal DEM observability gap and universal Test Unit negative remain present.

Machine-readable result: Tool / Task / Reference Matrix `20 unique task records`; Procedure Coverage Matrix `20 unique task records`; availability total `20`; all authority references resolve; changed draft paths `9`.

## Integrity confirmations

- No project Event ID/name, DTC, mapping, algorithm, policy, debounce value, cycle meaning, condition, memory setting, data content, NvM block ID/layout/CRC, FiM relation, Application symbol, network address, variant, stimulus, expected transition, test vector, tolerance, acceptance criterion or actual project tool version was fabricated.
- `docs/knowledge/**` is unchanged.
- `local-help/**` is unchanged and was not used as technical authority.
- No upstream repository was written.
- No new, alternative, fallback, repair, review or iteration branch was created.
