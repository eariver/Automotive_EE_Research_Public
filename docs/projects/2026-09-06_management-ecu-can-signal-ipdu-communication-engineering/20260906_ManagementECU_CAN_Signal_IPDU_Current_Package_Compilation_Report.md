# Management ECU CAN Signal / I-PDU Communication
# Current Package Compilation Report

Date: 2026-09-06
Status: LUNA_CURRENT_PACKAGE_COMPILED_PROPOSAL
Repository: eariver/Automotive_EE_Engineering_Knowledge
Execution branch: work/luna-management-ecu-can-signal-ipdu-current-package-compilation-20260906
Exact Starting SHA: 4df6a57dfa233ed803578ac9802117d13f6564ff
Ending SHA: single bounded compilation commit; record by required post-push remote read-back

## 1. Result

This compilation produces the current Management ECU CAN Signal / I-PDU
Communication package for exactly COM-001 through COM-018. Both machine-readable
matrices contain one row for each required task and no additional task.

This is downstream compilation only. No new AUTOSAR research, Vector/MICROSAR
HELP research, Web research, project design, generated-code inspection or
runtime execution was performed.

## 2. Exact authority pins

| Authority | Exact tuple | Use |
|---|---|---|
| Primary AUTOSAR architecture/workflow | eariver/Research_AUTOSAR_CP_Documents @ 8c67ddc4cc6ce4bba1881a879b933cf2b751d733; AUTOSAR Classic Platform 4.4.0 | architecture, system-to-ECU workflow, CAN data path, PduR, CanIf, CanDrv, conditional routes and observation navigation |
| Focused AUTOSAR COM semantics | eariver/Research_AUTOSAR_CP_Documents @ fc05fc7824d56b1a34eaf42e3d50150ff70a789d; docs/knowledge/management-ecu-can-signal-ipdu-autosar-semantic-depth.md | COM-004, COM-005, COM-006, COM-008, COM-009 and COM-010 semantic closure |
| Vector/MICROSAR COM procedure | eariver/Research_Vector_Documents @ 138dba4d76bc9cf7fadec1ee818aa7e6b9db4b70; docs/knowledge/management-ecu-com-vector-procedure.md | reviewed DaVinci Configurator Classic 6.3.10 product maturity and COM-016 generic subprocedures |
| Project input control | docs/projects/2026-09-06_management-ecu-can-signal-ipdu-communication-engineering/references/project/can-signal-ipdu-communication-project-input-baseline.yaml | unresolved project-owned input register; not technical authority |

The detailed entry paths, blob SHAs, sections and locators are in the Reference
Index and the two YAML matrices.

## 3. Task-level procedure availability

| Task | Primary availability | Project input blocker | Project design blocker | Execution-evidence blocker |
|---|---|---|---|---|
| COM-001 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-002 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-003 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-004 | PARTIAL_PROCEDURE_AVAILABLE | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-005 | PARTIAL_PROCEDURE_AVAILABLE | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-006 | SURFACE_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-007 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-008 | SURFACE_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-009 | NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-010 | PARTIAL_PROCEDURE_AVAILABLE | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-011 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-012 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-013 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-014 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-015 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-016 | PARTIAL_PROCEDURE_AVAILABLE | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-017 | WORKFLOW_ONLY | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |
| COM-018 | EXECUTION_EVIDENCE_REQUIRED | PROJECT_INPUT_REQUIRED | PROJECT_DESIGN_REQUIRED | EXECUTION_EVIDENCE_REQUIRED |

Primary availability counts:

- WORKFLOW_ONLY: 10
- PARTIAL_PROCEDURE_AVAILABLE: 4
- SURFACE_ONLY: 2
- NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE: 1
- EXACT_PROCEDURE_AVAILABLE: 0
- EXECUTION_EVIDENCE_REQUIRED: 1
- total: 18

The fixed Vector-reviewed subset remains:

- partial: COM-004, COM-005, COM-010, COM-016;
- surface only: COM-006, COM-008;
- no explicit reviewed procedure: COM-009.

## 4. COM-016 exact subprocedures

The aggregate COM-016 row remains PARTIAL_PROCEDURE_AVAILABLE. The following
generic product subprocedures are retained separately from the aggregate:

    dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
    dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
    dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"

The reviewed CLI context provides tool-process exit-code semantics. These
generic procedures do not prove COM-specific diagnostics, generated-file
manifest, compile/link result, runtime communication, verdict or coverage.

## 5. Project-input blockers

The project baseline remains UNRESOLVED_PROJECT_INPUT. No concrete value was
selected for:

- SW-C, port, interface, data-element, direction or multiplicity;
- System Description, ECU Extract, cluster, channel, ISignal or mapping;
- COM Signal, GroupSignal, SignalGroup, I-PDU or I-PDU Group;
- bit position, size, length, byte order, representation, scaling, init,
  invalid or substitution value;
- transfer property, Tx mode, repetition, period, offset, minimum delay,
  update/filter/invalid/timeout/notification/deadline policy;
- PduR source/destination route, gateway role or transport-protocol branch;
- CanIf PDU/controller bindings, CanDrv/controller/mailbox strategy;
- CAN/CAN FD choice, frame ID, DLC, channel or bus timing;
- product versions, MICROSAR packages, compiler/linker/build/target;
- observation point, stimulus, expected frame/value, threshold, verdict or
  coverage requirement.

## 6. Project-design blockers

Project design is required to decide:

- the application-to-RTE and System Description-to-ECU mapping;
- COM object ownership, layout and normal shadow-buffer versus array branch;
- Tx/Rx processing, data-quality, timeout and I-PDU Group policy;
- whether PduR route, CanTp, IpduM, SecOC, E2E/transformer or gatewaying is
  present;
- CanIf/CanDrv/controller responsibilities and CAN/CAN FD frame model;
- toolchain/build ownership and observation architecture;
- acceptance criteria and physical-target correlation requirements.

These design decisions are not made by this package.

## 7. Execution-evidence blockers

The package contains no actual:

- validation or generation run;
- generated artifact inventory or artifact inspection;
- compile/link result, binary or deployment identity;
- runtime SWC/COM/PduR/CanIf/CanDrv trace;
- observed CAN frame, timing or state;
- requirement comparison, verdict or coverage.

COM-018 therefore remains EXECUTION_EVIDENCE_REQUIRED. Configuration, validation,
generation, build success, TxConfirmation or a raw CAN trace does not by itself
close runtime communication, requirement satisfaction or coverage.

## 8. Retained documentation-scope negatives

The reviewed Vector authority does not establish a complete explicit procedure
for:

- COM Signal/GroupSignal/SignalGroup-to-product-object mapping;
- complete signal packing/layout/endianness field editing;
- transfer property, Tx mode, repetition or cyclic timing fields;
- Rx update-bit, filter, invalid, timeout or notification fields;
- COM deadline monitoring or COM I-PDU Group ownership/mapping;
- COM main-function/time-base configuration;
- COM-specific validation diagnostics or generated-file manifest;
- compiler/linker command/result, binary identity or deployment;
- runtime CAN communication, trace, verdict or coverage procedure.

These are documentation-scope negatives, not claims that the product lacks the
capability.

## 9. Conditional-route guard

CanTp, IpduM, SecOC, E2E/transformers and gatewaying are not inserted into a
Management ECU route. They remain conditional until explicit accepted project
evidence establishes the route. COM signal gatewaying remains distinct from
PduR I-PDU routing.

## 10. Semantic boundaries

The package preserves:

- application data element != Sender/Receiver port != COM Signal != SignalGroup/GroupSignal != I-PDU;
- System Description != ECU Extract != ECUC configuration != generated artifact != runtime state != observed CAN frame;
- COM != PduR != CanIf != CanDrv;
- COM signal gatewaying != PduR I-PDU routing;
- transfer property != Tx mode != repetition != configured timing;
- update-bit != filter != invalid handling != timeout handling;
- COM I-PDU Group control != ComM mode != CanSM state != physical bus state;
- configured callback != executed callback != application consumption;
- COM time base != OS Task schedule != measured CAN timing;
- configuration != validation != generation != compile/link != runtime trace;
- runtime observation != requirement != verdict != coverage;
- VECU/SIL behavior != physical-target CAN behavior.

## 11. Validation disposition

Before commit, the following are required to PASS:

- both YAML matrices contain exactly 18 unique task rows;
- no duplicate or extra task exists;
- availability counts total 18;
- fixed Vector classifications are preserved;
- supported claims have exact authority tuples;
- project-input, project-design and execution blockers are separate;
- conditional route boundaries and documentation negatives remain visible;
- only the nine allowlisted output paths are changed.

This report is a compilation handoff. Sol must independently review the fixed
head before any Publication工程.
