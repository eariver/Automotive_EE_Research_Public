# Management ECU CAN Signal / I-PDU Communication
# Execution Reference Guide

Date: 2026-09-06
Status: LUNA_CURRENT_PACKAGE_COMPILATION_PROPOSAL
Use: downstream engineering navigation after Sol-reviewed package compilation

## 1. Authority fence

Use only the following exact-pinned Reviewed Knowledge for static technical
claims:

| ID | Exact tuple | Scope |
|---|---|---|
| A-PRIMARY | eariver/Research_AUTOSAR_CP_Documents @ 8c67ddc4cc6ce4bba1881a879b933cf2b751d733 | AUTOSAR Classic Platform 4.4.0 architecture, work products, CAN path and layer ownership |
| A-COM | eariver/Research_AUTOSAR_CP_Documents @ fc05fc7824d56b1a34eaf42e3d50150ff70a789d; docs/knowledge/management-ecu-can-signal-ipdu-autosar-semantic-depth.md | Focused COM semantic depth and later product checklist |
| V-COM | eariver/Research_Vector_Documents @ 138dba4d76bc9cf7fadec1ee818aa7e6b9db4b70; docs/knowledge/management-ecu-com-vector-procedure.md | Sol-reviewed DaVinci Configurator Classic 6.3.10 procedure maturity |

Do not reopen generic AUTOSAR or Vector research in this guide. Do not use raw
PDF, raw HELP, current vendor documentation, Web, floating branch heads or
generic model knowledge as a technical authority.

## 2. Package navigation

Use the package in this order:

1. confirm the project communication intent and the application/RTE contract;
2. identify the System Description and ECU Extract work-product roles;
3. separate COM, PduR, CanIf and CanDrv ownership;
4. resolve only project-supplied COM object and layout values;
5. classify Tx/Rx/group/timeout decisions independently;
6. decide whether conditional CanTp, IpduM, SecOC, E2E/transformer or gateway
   branches are actually established;
7. validate and generate only after an accepted project configuration exists;
8. retain build, runtime, bus, requirement, verdict and coverage as separate
   evidence layers.

The package's current state is a proposal. It does not configure or execute an
ECU.

## 3. Task handoff reference

| Task | Start with | Activity | Output / next handoff |
|---|---|---|---|
| COM-001 | reviewed CAN data-plane and ownership model | decompose the route and mark conditional branches | project-neutral architecture map |
| COM-002 | SW-C ports/interfaces/connectors and S/R access | classify explicit versus implicit RTE-facing access | application-to-RTE access map |
| COM-003 | System Description and ECU Extract roles | preserve system, ECU Extract and ECU Configuration Values separation | ECU-specific input boundary |
| COM-004 | COM object and foreign-reference semantics | distinguish Signal, GroupSignal, SignalGroup and I-PDU; choose no default group branch | COM object register |
| COM-005 | signal-to-I-PDU mapping and COM placement terms | resolve only supplied type, size, position, endianness and length | layout/representation register |
| COM-006 | transfer property, Tx mode/TMS and repetition distinctions | record each Tx behavior dimension separately | Tx behavior checklist |
| COM-007 | non-TP COM to PduR to CanIf to CanDrv navigation | correlate request, forwarding, confirmation and bus observation separately | Tx evidence chain |
| COM-008 | Rx indication and immediate/deferred processing | keep COM unpacking and application consumption separate | Rx delivery map |
| COM-009 | update-bit, filter, invalid and notification semantics | record independent data-quality policies | Rx data-quality register |
| COM-010 | first/subsequent timeout and monitoring control | separate timer state, timeout action and observed timing | deadline/timeout evidence plan |
| COM-011 | COM I-PDU Group start/stop boundary | do not map group control to ComM/CanSM without evidence | group-control design |
| COM-012 | PduR IF/TP boundary | classify route class and conditional gateway/TP role | PduR routing register |
| COM-013 | CanIf abstraction | keep PDU/controller abstraction separate from driver/hardware | CanIf mapping register |
| COM-014 | CanDrv and CanTrcv ownership | keep controller access, transceiver mode and physical frame separate | hardware boundary |
| COM-015 | CAN/CAN FD topology and frame model | obtain project frame, payload and bus values | frame/bus input register |
| COM-016 | exact generic product subprocedures | validate, generate and generate-schema only for an accepted project; retain aggregate partial | package/build handoff |
| COM-017 | reviewed configure-and-trace navigation | design project observation points without inventing tools/stimuli | observation plan |
| COM-018 | state/evidence chain | execute and correlate all evidence layers, then compare to requirements | verdict/coverage package |

## 4. Exact generic product subprocedures

The following are retained from the already reviewed DaVinci Configurator
Classic 6.3.10 authority. They are generic product procedures, not
Management ECU COM-specific completion:

### 4.1 Project validation

    dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"

The reviewed success wording is Validation Successful. Validation checks
completeness, consistency and correctness. A successful validation is not
generation, compile/link, runtime communication or a verdict.

### 4.2 Project generation

    dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"

The reviewed success wording is Generation Successful. Generated BSW/RTE
source/configuration output is not a compile/link result or runtime trace.

### 4.3 Schema generation

    dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"

The reviewed schema output is /Output/Schema. Schema output is not a generated
COM artifact, binary or runtime result.

### 4.4 CLI status context

The reviewed CLI context distinguishes:

- exit code 0: successful execution;
- exit code 1: execution failure;
- exit code 2: usage error;
- exit code 130: user cancellation.

These are tool-process statuses, not communication verdicts.

## 5. Product surfaces and maturity boundaries

The reviewed product authority retains:

- Communications > PDUs navigation and PDU/PDU-group view/edit operations;
- generic Basic Editor/module/container configuration;
- bounded BswM Communication Control wording mentioning I-PDU Groups;
- generic validation, generation and schema generation commands;
- generic generated-output directories and CI/build handoff wording.

The following must not be inferred from a generic product surface:

- exact COM Signal or SignalGroup object mapping;
- exact transfer, Tx mode, repetition, timeout or notification field path;
- exact COM I-PDU Group ownership;
- COM main-function/time-base realization;
- generated COM filename or complete artifact manifest;
- compiler/linker command, binary identity or runtime behavior.

## 6. Project-input register

Before selecting any value, obtain explicit project input for:

- SW-C, port, interface, data-element and direction;
- System Description, ECU Extract, cluster/channel and ISignal mappings;
- COM Signal, GroupSignal, SignalGroup and I-PDU identities;
- signal type, size, length, position, byte order, scaling, init and invalid values;
- transfer property, Tx mode, repetition, minimum delay and timing;
- update/filter/invalid/timeout/notification/deadline policies;
- I-PDU Group start/stop and lifecycle policy;
- PduR source/destination route and gateway/TP decision;
- CanIf PDU/controller references and CanDrv/CanTrcv mapping;
- CAN/CAN FD selection, frame ID, DLC, channel and timing;
- product versions, generator, compiler/linker, build variant and target;
- observation points, stimuli, expected values/frames, acceptance criteria and
  coverage requirements.

An unresolved item remains PROJECT_INPUT_REQUIRED or PROJECT_DESIGN_REQUIRED.
No example or sibling ECU supplies a default.

## 7. Execution-evidence register

For project closure, record independently:

1. configured intent and accepted configuration;
2. validation command, exact project revision and result;
3. generated artifact inventory and provenance;
4. compile/link command, result and binary identity;
5. runtime SWC/COM/PduR/CanIf/CanDrv observation;
6. physical or approved-target CAN frame/timing/state observation;
7. requirement comparison;
8. verdict;
9. coverage scope and result.

COM-018 remains EXECUTION_EVIDENCE_REQUIRED until this chain is populated.
Configuration, generation, build success, TxConfirmation or a raw trace alone
does not prove durable communication, requirement satisfaction or coverage.

## 8. Conditional-route guard

Do not insert any of the following into a Management ECU route without explicit
accepted project evidence:

- CanTp transport-protocol segmentation/reassembly;
- IpduM multiplexing or Container PDU processing;
- SecOC PDU security;
- E2E or other transformers;
- COM signal gatewaying or transparent PduR gatewaying.

If a branch is established, record its owner, source configuration, generated
artifact and runtime evidence separately. COM signal gatewaying is not PduR
I-PDU routing, and dual CAN is not proof of gateway responsibility.

## 9. Completion gate

The package is ready for Sol fixed-head review when:

- both YAML matrices have exactly 18 unique task rows;
- classifications and counts match the fixed decisions;
- every supported claim has a pinned authority tuple;
- no project-specific value is present without explicit project input;
- blockers are split into input, design and execution evidence;
- all non-collapse boundaries and documentation negatives are visible;
- only the nine package outputs are changed.

This guide does not authorize publication or final maturity. Sol must independently
review the fixed head.
