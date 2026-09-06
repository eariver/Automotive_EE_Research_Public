# Publication — Management ECU CAN Signal / I-PDU Communication Engineering

Date: 2026-09-06
Status: `SOL_REVIEWED_STAGED`

## Accepted private source

- Repository: `eariver/Automotive_EE_Engineering_Knowledge`
- Sol review branch: `work/sol-management-ecu-can-signal-ipdu-current-package-review-20260906`
- Accepted source HEAD: `42891e51c576527f5273ab6929c1498e94eb4346`
- Luna current-package terminal reviewed: `688cced77bd899222095757ce5b1f48f8112cb59`
- Sol verdict: `SOL_PACKAGE_REVIEW_PASS`

The private current package contains exactly `COM-001` through `COM-018` and was independently fixed-head reviewed before publication staging.

## Public staging branch

- Repository: `eariver/Automotive_EE_Research_Public`
- Branch: `publish/management-ecu-can-signal-ipdu-communication-engineering-20260906`
- Public base `main`: `183d9dc0ab120484e4018e530a33e5b291bd7baa`
- `main` merged: **false**

Publication staging does not modify public `main`. Merge requires separate explicit human approval.

## Current maturity

Primary task-level availability:

- `WORKFLOW_ONLY`: 10
- `PARTIAL_PROCEDURE_AVAILABLE`: 4
- `SURFACE_ONLY`: 2
- `NO_EXPLICIT_PROCEDURE_IN_REVIEWED_SOURCE`: 1
- `EXACT_PROCEDURE_AVAILABLE`: 0 at aggregate task level
- `EXECUTION_EVIDENCE_REQUIRED`: 1
- total: 18

Generic validation, generation, schema-generation and CLI subprocedures inside `COM-016` are exact at their reviewed product scope; aggregate `COM-016` remains partial.

## Remaining blockers

- `PROJECT_INPUT_REQUIRED`: all 18 tasks.
- `PROJECT_DESIGN_REQUIRED`: 17 tasks at current package classification level.
- Aggregate execution closure: `COM-018` remains `EXECUTION_EVIDENCE_REQUIRED`.

No Management ECU-specific signal/frame identity, position, length, transfer property, timing, route, CAN/CAN FD setting, build value, expected trace, verdict or coverage is introduced by publication.

## Reviewed authority

- Primary AUTOSAR architecture/workflow:
  `eariver/Research_AUTOSAR_CP_Documents@8c67ddc4cc6ce4bba1881a879b933cf2b751d733`
- Focused AUTOSAR COM semantic depth:
  `eariver/Research_AUTOSAR_CP_Documents@fc05fc7824d56b1a34eaf42e3d50150ff70a789d`
- Vector/MICROSAR COM procedure:
  `eariver/Research_Vector_Documents@138dba4d76bc9cf7fadec1ee818aa7e6b9db4b70`

Generic AUTOSAR COM semantic research and generic Vector/MICROSAR COM procedure research are closed at this reviewed scope.

## Publication bundle

The staged bundle contains 13 source-derived engineering artifacts plus 2 publication metadata files:

1. project README
2. Project Scope
3. Methodology
4. Step-by-Step Guide
5. Tool / Task / Reference Matrix
6. State & Evidence Model
7. Execution Reference Guide
8. Procedure Coverage Matrix
9. Reference Index
10. Current Package Compilation Report
11. Sol fixed-head review
12. authority pins
13. publication-safe unresolved project-input baseline
14. this Publication README
15. `publication-plan.yaml`

The two large YAML matrices were transferred from the accepted private fixed head in bounded line ranges because cross-repository Git blob reuse is not supported by GitHub. Their public Git blob IDs are therefore not used as private-byte identity claims; publication validation checks task cardinality, authority tuples, classifications, blockers and retained boundaries instead.

## Retained boundaries

- application data element != Sender/Receiver port/interface != COM Signal != GroupSignal/SignalGroup != I-PDU
- System Description != ECU Extract != ECUC configuration != generated artifact != runtime state != observed CAN frame
- COM != PduR != CanIf != CanDrv
- COM signal gatewaying != PduR I-PDU routing
- transfer property != Tx mode != repetition != configured timing
- update-bit != filter != invalid-value handling != timeout handling
- COM I-PDU Group control != ComM mode != CanSM state != physical bus state
- configured callback != executed callback != application consumption
- COM time base != OS Task schedule != measured CAN timing
- configuration != validation != generation != compile/link != runtime trace
- runtime observation != requirement != verdict != coverage
- VECU/SIL behavior != physical-target CAN/CAN FD behavior

CanTp, IpduM, SecOC, E2E/transformers and gatewaying remain conditional and are not inserted into a concrete route without accepted project evidence.

## Excluded from publication

- Luna prompts, plans, instructions, observations and worklogs
- internal baseline/research checkpoints and Luna terminal checkpoint
- historical baseline/research-gap artifacts not required for current consumption
- raw AUTOSAR/Vector source documents
- upstream canonical `docs/knowledge/**` bodies
- confidential/project-specific actual values
- invented values or runtime results

This branch is a publication staging branch. Public `main` remains unchanged until separately authorized.
