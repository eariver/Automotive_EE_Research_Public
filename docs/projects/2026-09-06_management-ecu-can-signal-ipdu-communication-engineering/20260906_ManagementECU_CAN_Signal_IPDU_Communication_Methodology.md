# Management ECU CAN Signal / I-PDU Communication
# Current Engineering Package Compilation Methodology

Date: 2026-09-06
Status: LUNA_CURRENT_PACKAGE_COMPILATION_PROPOSAL
Execution repository: eariver/Automotive_EE_Engineering_Knowledge
Execution branch: work/luna-management-ecu-can-signal-ipdu-current-package-compilation-20260906
Exact Starting SHA: 4df6a57dfa233ed803578ac9802117d13f6564ff

## 1. Mission and scope

This package compiles the current Management ECU CAN Signal / I-PDU Communication
engineering baseline for exactly COM-001 through COM-018. It is downstream
compilation from already Sol-reviewed authority. It is not a new AUTOSAR study,
Vector/MICROSAR HELP study, Web study, project design, generated-code inspection or
runtime execution.

The package preserves a navigation-ready engineering baseline. It does not accept
any Management ECU signal, frame, I-PDU, route, timing, toolchain, runtime result,
verdict or coverage value unless that value is supplied by an explicit project
input or execution artifact.

## 2. Authority model

Technical claims are bounded to the following exact-pinned Sol-reviewed authority
tuples. The project-input baseline is a control input, not technical authority.

| ID | Authority tuple | Use |
|---|---|---|
| A-PRIMARY | eariver/Research_AUTOSAR_CP_Documents @ 8c67ddc4cc6ce4bba1881a879b933cf2b751d733; AUTOSAR Classic Platform 4.4.0; reviewed entries under docs/knowledge/ | Architecture, work-product, CAN data-path, PduR, CanIf, CanDrv and observation navigation |
| A-COM | eariver/Research_AUTOSAR_CP_Documents @ fc05fc7824d56b1a34eaf42e3d50150ff70a789d; docs/knowledge/management-ecu-can-signal-ipdu-autosar-semantic-depth.md; AUTOSAR CP 4.4.0 / R18-10 | COM Signal, packing, Tx, Rx, invalid/timeout and I-PDU Group semantic depth |
| V-COM | eariver/Research_Vector_Documents @ 138dba4d76bc9cf7fadec1ee818aa7e6b9db4b70; docs/knowledge/management-ecu-com-vector-procedure.md; DaVinci Configurator Classic 6.3.10 | Fixed product-procedure maturity and exact generic validation/generation subprocedures |
| P-INPUT | docs/projects/2026-09-06_management-ecu-can-signal-ipdu-communication-engineering/references/project/can-signal-ipdu-communication-project-input-baseline.yaml; status UNRESOLVED_PROJECT_INPUT | Project-owned input register only; never used to invent values |

The exact entry paths, blob SHAs, section locators and requirement IDs are
recorded in the Reference Index and repeated in both machine-readable matrices.

## 3. Compilation dimensions

Every task is represented across independent dimensions:

1. engineering intent;
2. lifecycle phase;
3. owner and layer;
4. tool or product surface;
5. exact reviewed authority tuple;
6. strongest reviewed workflow or procedure;
7. primary procedure availability;
8. project input blocker;
9. project design blocker;
10. execution-evidence blocker;
11. input artifact/state;
12. operation/activity;
13. output artifact/state;
14. exit condition;
15. next handoff;
16. retained boundary or documentation negative;
17. evidence needed for the next promotion.

Procedure availability and closure blockers are intentionally orthogonal. A
reviewed workflow can coexist with unresolved project input and execution
evidence. A product surface can remain partial without downgrading an independent
AUTOSAR architecture boundary.

## 4. Primary procedure-availability vocabulary

Only these primary labels are used:

- EXACT_PROCEDURE_AVAILABLE
- PARTIAL_PROCEDURE_AVAILABLE
- SURFACE_ONLY
- NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE
- WORKFLOW_ONLY
- EXECUTION_EVIDENCE_REQUIRED

The fixed product maturity is preserved:

- COM-004: PARTIAL_PROCEDURE_AVAILABLE
- COM-005: PARTIAL_PROCEDURE_AVAILABLE
- COM-006: SURFACE_ONLY
- COM-008: SURFACE_ONLY
- COM-009: NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE
- COM-010: PARTIAL_PROCEDURE_AVAILABLE
- COM-016: PARTIAL_PROCEDURE_AVAILABLE

The exact generic validation, generation, schema-generation and CLI status
subprocedures remain visible inside COM-016. They do not promote the aggregate
COM-016 row to exact.

## 5. Layered engineering method

### 5.1 Contract and system mapping

Start with the application Sender/Receiver contract and RTE-facing access.
Keep application data elements, ports/interfaces/connectors, System Template
identities, ECU Extract and ECU Configuration Values separate. Use the accepted
System Description to ECU Extract to ECU configuration navigation only as a
work-product flow. Do not create project object names from examples.

### 5.2 COM semantics

For COM Signal, GroupSignal, SignalGroup and I-PDU, use the focused COM authority
for object identities and conditional branches. Preserve normal shadow-buffer
group access versus configured UINT8-array group access as a conditional
alternative. Keep COM placement/representation, transfer property, Tx mode,
repetition, cyclic timing, update-bit, filter, invalid handling, timeout handling
and notification as separate dimensions.

### 5.3 Lower-layer ownership

Use the reviewed minimal non-TP path as architecture navigation:

    RTE-facing signal interaction
    -> COM signal-oriented processing and I-PDU packing
    -> PduR configured I-PDU forwarding
    -> CanIf hardware-independent abstraction
    -> CanDrv controller access
    -> CAN controller and physical bus

This is not a universal synchronous API trace and is not a configured Management
ECU route. PduR IF routing, PduR TP routing, COM signal gatewaying, CanTp,
IpduM, SecOC and transformers remain separate or conditional.

### 5.4 Procedure and evidence boundary

The Vector authority supplies product-level maturity only where it was reviewed.
For COM-016, exact generic validation, generation, schema generation and CLI
status context are retained. Generic success is not COM-specific artifact proof,
compile/link proof, runtime proof, requirement satisfaction, verdict or coverage.

The package records configuration, validation, generation, compile/link, runtime
trace, observed frame/timing, requirement comparison, verdict and coverage as
separate evidence layers.

## 6. Non-collapse invariants

The following are package invariants:

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

CanTp, IpduM, SecOC, E2E/transformers and gatewaying are conditional routes.
They are not inserted into a concrete Management ECU route without accepted
project evidence.

## 7. Promotion model

The package is ready for Sol fixed-head review when:

- both machine-readable matrices contain exactly the 18 required task identities;
- each task has exact-pinned authority or an explicit boundary-only authority;
- the fixed Vector classifications are unchanged;
- project input, project design and execution evidence are distinct fields;
- all unresolved Management ECU values remain unresolved;
- conditional routes remain conditional;
- documentation-scope negatives remain explicit;
- only the nine allowlisted outputs are changed.

Future promotion requires project-owned communication model and configuration
inputs, design decisions, validation/generation artifacts, compile/link evidence,
layer-correlated runtime observations, explicit requirements, verdict criteria and
coverage records. Final maturity is determined by Sol after fixed-head review.

## 8. Closed research status

Generic AUTOSAR COM semantic research and generic Vector/MICROSAR COM procedure
research are closed at the pinned reviewed scope. This compilation does not
reopen those units and does not use raw/current/floating sources.
