# Management ECU — UDS on CAN Diagnostic Engineering Toolchain

Date: 2026-09-02

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
            -> vVIRTUALtarget
            -> Lv3 VECU
            -> CANoe

CANdela diagnostic specification
  -> CANoe.DiVa diagnostic test design/generation
  -> CANoe test execution
  -> diagnostic result/report evidence
```

The diagram shows handoffs and ownership, not one universal automatic synchronization path.

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
- code generation != compile != link.
- MathWorks local RTE stub != production MICROSAR RTE.
- MIL != SIL != VECU/HIL/physical-SUT evidence.
- test verdict != coverage.
- CANdela export/import overlap != lossless round-trip or universal producer contract.
- DiVa generated test definition != CANoe execution result/report.

## Start here

1. `20260902_ManagementECU_UDS_CAN_Diagnostic_Toolchain_Execution_Reference_Guide.md`
2. `20260902_ManagementECU_UDS_CAN_Diagnostic_Tool_Task_Reference_Matrix.yaml`
3. `20260902_ManagementECU_UDS_CAN_Diagnostic_Development_Methodology.md`
4. `20260902_ManagementECU_UDS_CAN_Diagnostic_Step_by_Step_Guide.md`
5. `20260902_ManagementECU_UDS_CAN_Diagnostic_Reference_Index.yaml`
6. `procedures/20260902_ManagementECU_UDS_CAN_Tool_Procedure_Compilation_Matrix.yaml`
7. `procedures/20260902_ManagementECU_UDS_CAN_Tool_Procedure_Compilation_Report.md`
8. `references/*/reference-locators.yaml`
9. `references/project/*.yaml`

## Project-input rule

Concrete Management ECU values are not sourced from vendor/AUTOSAR authority. DID/RID/DTC values, sessions/security policy, NRC policy, P2/P2* timing, DEM debounce/confirmation, CAN identifiers, CanTp addressing, callback mappings, calibration values, test vectors and actual tool releases remain explicit project inputs until supplied and accepted.

## Procedure compilation status

The fixed-authority procedure compilation for `DTR-002` through `DTR-019` has been Sol-reviewed and accepted at Luna Ending SHA:

`3b5f2cdfc418e46cd2ad4a8509fc77ac50eacc12`

Accepted classification summary:

- `EXACT_PROCEDURE_AVAILABLE`: 1
- `PARTIAL_PROCEDURE_AVAILABLE`: 11
- `WORKFLOW_ONLY`: 5
- `NO_EXPLICIT_PROCEDURE`: 0
- `PROJECT_INPUT_REQUIRED`: 1
- `UNRESOLVED_AUTHORITY`: 0

The strongest exact bounded route is `DTR-019`, the named CANoe.DiVa -> CANoe import/bind/execute/report sequence.

`DTR-013` remains `PROJECT_INPUT_REQUIRED` because the Management ECU CAN/CanTp/PduR/CanIf project values are intentionally not yet selected.

This status does not mean every tool has click-by-click coverage. Exact GUI/API/CLI details are exposed only where they were explicit in frozen Reviewed Knowledge.

## Publication rule

Intermediate work and Luna compilation remain in `eariver/Automotive_EE_Engineering_Knowledge`. Only Sol-reviewed publication artifacts are later packaged into `eariver/Automotive_EE_Research_Public`.
