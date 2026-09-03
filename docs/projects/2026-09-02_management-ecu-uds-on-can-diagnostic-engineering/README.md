# Management ECU — UDS on CAN Diagnostic Engineering Toolchain

Date: 2026-09-03

## Purpose

This project compiles a task-oriented engineering route for Management ECU diagnostic development using CANdela Studio, DaVinci Developer Classic, MathWorks AUTOSAR/Simulink tooling, DaVinci Configurator Classic/MICROSAR, vVIRTUALtarget, CANoe and CANoe.DiVa.

The purpose is **not** to invent the Management ECU diagnostic specification. The purpose is to make it clear, for each engineering intent:

- which lifecycle stage owns the work;
- which tool is primary and which tools support it;
- what project input must exist before work begins;
- which exact-pinned Reviewed Knowledge must be read;
- what operation is supported at the current evidence level;
- what artifact/state is produced;
- what boundary must not be collapsed;
- what must be true before moving to the next stage.

## Scope

Canonical protocol scope: **UDS on CAN only**.

Included:

- CANdela diagnostic specification authoring;
- UDS service/DID/Routine/DTC/session/security design boundaries;
- Application SWC diagnostic contract and behavior;
- AUTOSAR DCM/DEM ownership and configuration;
- UDS-on-CAN transport through the configured PduR/CanTp/CanIf/Can path;
- production RTE/BSW integration;
- Lv3 VECU construction with vVIRTUALtarget;
- CANoe integration;
- CANoe.DiVa diagnostic test design/generation and CANoe execution/evidence.

Excluded from this compilation:

- DoIP;
- OBD-specific workflow;
- SAE J1939 diagnostics;
- physical ECU/HIL procedure;
- TargetLink as the canonical Application SWC implementation route.

## Canonical toolchain

```text
CANdela Studio
  -> diagnostic specification / CDD (and bounded interchange such as ODX where used)
  -> responsibility allocation
       |-> DaVinci Developer Classic
       |    -> AUTOSAR SWC contract ARXML
       |    -> AUTOSAR Blockset
       |    -> Simulink / Stateflow
       |    -> Embedded Coder
       |    -> generated C/H + implementation ARXML
       |
       `-> DaVinci Configurator Classic / MICROSAR
            -> DCM / DEM / PduR / CanTp / CanIf / Can + production RTE/BSW/OS integration
            -> integrated ECU software
            -> vVIRTUALtarget Integration
            -> Integration SUT DLL / simulation-package family
            -> CANoe

CANdela diagnostic specification
  -> CANoe.DiVa diagnostic test design/generation
  -> CANoe test execution
  -> diagnostic result/report evidence
```

The diagram shows handoffs and ownership, not one universal automatic synchronization path.

Sol project decision after targeted Vector review: the canonical vVIRTUALtarget route for this Management ECU Lv3 VECU methodology is **Integration**. BSW Emulation remains a separate alternate route and must not be collapsed into the Integration artifact family.

## Hard semantic boundaries

```text
CANdela diagnostic specification
  != Application SWC contract
  != Application SWC behavior
  != generated Application SWC implementation
  != DCM service/session/security processing
  != DEM event/DTC/fault-memory processing
  != PduR/CanTp/CanIf/Can transport realization
  != production RTE/BSW/OS integration
  != VECU artifact
  != DiVa test definition
  != CANoe/DiVa execution result
```

Additional retained rules:

- DCM != DEM.
- Application diagnostic/fault policy != DCM != DEM.
- DCM uses PduR as a network-independent diagnostic transport boundary; CanTp is a configured CAN transport branch below PduR and above CanIf.
- CanIf != CAN Driver.
- source ARXML != imported Simulink/AUTOSAR representation != generated implementation ARXML.
- code generation != compile != link.
- MathWorks local RTE stub != production MICROSAR RTE.
- vVIRTUALtarget Integration != BSW Emulation.
- MIL != SIL != PIL != VECU/HIL/physical-SUT evidence.
- test verdict != coverage.
- CANdela export/import overlap != lossless round-trip or universal producer contract.
- DiVa generated test definition != CANoe execution result/report.

## Start here

For normal engineering use:

1. `20260902_ManagementECU_UDS_CAN_Diagnostic_Toolchain_Execution_Reference_Guide.md` — intent-first baseline human guide.
2. `20260903_ManagementECU_UDS_CAN_Procedure_Authority_Expansion_Addendum.md` — current reviewed operation routes after targeted Vector/MathWorks research.
3. `20260902_ManagementECU_UDS_CAN_Diagnostic_Tool_Task_Reference_Matrix.yaml` — task/lifecycle/tool/input/output navigation.
4. `procedures/procedure-coverage-matrix.yaml` — current accepted procedure maturity and task-to-family lookup.
5. `procedures/procedure-authority-expansion-overlay.yaml` — final maturity decisions and source-explicit basis for each DTR task.
6. relevant `procedures/<tool-family>.yaml` — historical tool-family operation context from the first procedure compilation.
7. `20260902_ManagementECU_UDS_CAN_Diagnostic_Reference_Index.yaml` — exact technical authority resolution.
8. `references/procedure-authority-expansion-pins.yaml` — exact Sol-reviewed Vector/MathWorks supplement pins.

For methodology/background review:

9. `20260902_ManagementECU_UDS_CAN_Diagnostic_Development_Methodology.md`
10. `20260902_ManagementECU_UDS_CAN_Diagnostic_Step_by_Step_Guide.md`

For procedure-compilation audit/provenance:

11. `procedures/20260902_ManagementECU_UDS_CAN_Tool_Procedure_Compilation_Matrix.yaml`
12. `procedures/20260902_ManagementECU_UDS_CAN_Tool_Procedure_Compilation_Report.md`
13. `references/reference-coverage-matrix.yaml`
14. `references/reference-coverage-report.md`

Project input scaffolds are under `references/project/`.

## Procedure family index

- `procedures/candela-studio.yaml` — DTR-002, DTR-003.
- `procedures/davinci-developer-classic.yaml` — DTR-004.
- `procedures/autosar-blockset.yaml` — DTR-005, DTR-007.
- `procedures/simulink-stateflow.yaml` — DTR-006.
- `procedures/mil-sil.yaml` — DTR-008, DTR-010.
- `procedures/embedded-coder.yaml` — DTR-009.
- `procedures/davinci-configurator-microsar.yaml` — DTR-011, DTR-012, DTR-014.
- `procedures/diagnostic-bsw-uds-on-can.yaml` — DTR-011, DTR-012, DTR-013 ownership/configuration view.
- `procedures/vvirtualtarget.yaml` — DTR-015.
- `procedures/canoe-diva.yaml` — DTR-016 through DTR-019.

The family files preserve the first accepted procedure compilation. The **current classification authority** is `procedures/procedure-coverage-matrix.yaml` plus `procedures/procedure-authority-expansion-overlay.yaml`.

## Project-input rule

Concrete Management ECU values are not sourced from vendor/AUTOSAR authority. DID/RID/DTC values, sessions/security policy, NRC policy, P2/P2* timing, DEM debounce/confirmation, CAN identifiers, CanTp addressing, callback mappings, calibration values, test vectors and actual tool releases remain explicit project inputs until supplied and accepted.

## Procedure authority-expansion status

The first fixed-authority procedure compilation remains retained at Luna Ending SHA:

`3b5f2cdfc418e46cd2ad4a8509fc77ac50eacc12`

Targeted upstream authority expansion has now also been completed and Sol-reviewed.

Vector reviewed authority:

`bcbe4e5b57aa144bfa5cb3d5e86f2a1e5a1274ee`

MathWorks R2025b reviewed authority:

`2fb38fe40d87a9cb8e7a22f7fe4a1a6a04354187`

Current classification summary:

- `EXACT_PROCEDURE_AVAILABLE`: **11**
- `PARTIAL_PROCEDURE_AVAILABLE`: **5**
- `WORKFLOW_ONLY`: **1**
- `NO_EXPLICIT_PROCEDURE`: **0**
- `PROJECT_INPUT_REQUIRED`: **1**
- `UNRESOLVED_AUTHORITY`: **0**

The eleven exact bounded tasks are:

`DTR-002`, `DTR-004`, `DTR-005`, `DTR-007`, `DTR-008`, `DTR-009`, `DTR-010`, `DTR-015`, `DTR-016`, `DTR-018`, `DTR-019`.

`DTR-006` remains `WORKFLOW_ONLY` because Management ECU diagnostic Application behavior is a project-design decision, not a vendor-procedure question.

`DTR-013` remains `PROJECT_INPUT_REQUIRED` because the Management ECU CAN/CanTp/PduR/CanIf network values are intentionally not yet selected.

The remaining partial tasks are `DTR-003`, `DTR-011`, `DTR-012`, `DTR-014` and `DTR-017`. Their bounded gaps are recorded in the 2026-09-03 addendum and coverage overlay.

Exact procedure availability does not imply that project values, actual run results, cross-tool interoperability, production integration or acceptance have already been established. It means the bounded operation route itself is source-explicit at the reviewed product/release scope.

## Publication rule

Intermediate work and Luna evidence remain in `eariver/Automotive_EE_Engineering_Knowledge`. Only Sol-reviewed publication artifacts are packaged into `eariver/Automotive_EE_Research_Public`. The Public package should mirror the current downstream files byte-for-byte and exclude internal Luna evidence/prompts/worklogs.
