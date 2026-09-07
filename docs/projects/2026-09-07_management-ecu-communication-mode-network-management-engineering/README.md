# Management ECU Communication Mode & Network Management Engineering

## Purpose

This public package presents the Sol-reviewed current engineering authority for Management ECU Communication Mode & Network Management (CNM) in AUTOSAR Classic, with explicit separation between standards semantics, Vector/MICROSAR product-procedure availability, project-owned design/input, and execution evidence.

The package covers the fixed task population `CNM-001` through `CNM-018` and preserves the reviewed boundaries among ComM, CanSM, Nm, CanNm, EcuM, BswM, COM I-PDU Groups, wakeup/bus-off handling, PNC, product configuration workflow, and later runtime verification.

## Current state

Status: `SOL_REVIEWED_PUBLICATION_STAGED`

Accepted Private publication authority:

- repository: `eariver/Automotive_EE_Engineering_Knowledge`
- branch: `work/sol-management-ecu-communication-mode-network-management-current-package-review-20260907`
- accepted source HEAD: `a8dd173415716a895c9787e2bf8a5dea9fd3051c`
- accepted Luna current-package candidate: `136e5250efb7a932fc286e64405997fbce9fe801`
- baseline authority: `56f753e5f605f7441b957490c36080f067bb0807`

The fixed-head review verdict is `SOL_CURRENT_PACKAGE_REVIEW_PASS`.

## Reviewed upstream authority

Load-bearing authority is exact-pinned to:

- focused AUTOSAR semantic authority: `eariver/Research_AUTOSAR_CP_Documents@a7d063d4fb020e565497388c2c6cea5c2605a1ed`
- focused Vector/MICROSAR product-procedure authority: `eariver/Research_Vector_Documents@9b1e1a1fb172cb43466b89f07a1c22f9a8e00990`
- retained older AUTOSAR baseline context: `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d`

No floating `main` or floating branch is used as technical authority.

## Current package

Reader-facing reviewed artifacts in this publication branch include:

- `20260907_ManagementECU_Communication_Mode_Network_Management_Current_Package_Compilation_Report.md`
- `20260907_ManagementECU_Communication_Mode_Network_Management_Methodology.md`
- `20260907_ManagementECU_Communication_Mode_Network_Management_Step_by_Step_Guide.md`
- `guides/20260907_ManagementECU_Communication_Mode_Network_Management_Execution_Reference_Guide.md`
- `models/20260907_ManagementECU_Communication_Mode_Network_Management_State_Evidence_Model.md`
- `references/20260907_ManagementECU_Communication_Mode_Network_Management_Reference_Index.md`
- `20260907_ManagementECU_Communication_Mode_Network_Management_Sol_Review.md`
- `matrices/20260907_ManagementECU_Communication_Mode_Network_Management_Public_Coverage_Matrix.yaml`

The compact public matrix is a publication projection of the accepted 18-task status. The larger Private execution matrices and Luna checkpoint are intentionally not copied into the public package.

## Vector product-procedure summary

For the fixed ten-slice Vector/MICROSAR scope:

- `EXACT_PRODUCT_PROCEDURE_AVAILABLE`: 0
- `PARTIAL_PRODUCT_PROCEDURE_AVAILABLE`: 5
- `SURFACE_ONLY`: 1
- `NO_EXPLICIT_REVIEWED_PROCEDURE`: 4
- `OUTSIDE_AUTHORIZED_PRODUCT_SCOPE`: 0
- total: 10

The five partial tasks are `CNM-002`, `CNM-003`, `CNM-014`, `CNM-015`, and `CNM-016`. `CNM-004` is surface-only. `CNM-005`, `CNM-007`, `CNM-008`, and `CNM-011` have no explicit reviewed procedure in the authorized product documentation scope.

An unavailable page-local procedure is not a claim that the product lacks the capability.

## Mandatory non-collapse rules

Do not collapse:

- application/BSW communication demand != ComM user != ComM channel;
- ComM user request != stored request != channel target != BusSM actual-mode indication;
- `COMM_SILENT_COMMUNICATION` != user-requested communication mode;
- ComM mode != CanSM state != CanNm protocol state != physical bus availability;
- ComM -> Nm -> BusNm request != BusNm -> Nm -> ComM notification;
- CanSM request != main-function processing != CanIf indication != physical completion;
- bus-off callback != recovered bus;
- CanTrcv WUF/status != CanSM wakeup-validation phase != EcuM wakeup validation/result;
- CanNm requested/released state != operational mode != internal protocol state;
- PNC ID derivation != EIRA/ERA != ComM PNC state != selective wakeup;
- BswM action / `BswMPduGroupSwitch` != application availability;
- COM I-PDU Group state != ComM mode != CanSM state != physical bus availability;
- configuration != validation != generation != compile/link != runtime transition;
- runtime observation != requirement != verdict != coverage.

## Project-owned values

This package does not select Management ECU-specific ComM users/channels, communication-demand allocation, communication-mode/inhibition policy, Nm/CanNm adoption or timers, PNC mapping, gateway role, wakeup sources, controller/transceiver identity, bus-off recovery values, BswM rules/actions, COM I-PDU Group realization, application-availability criteria, target/runtime scope, timing thresholds, or acceptance criteria.

Dual CAN does not imply gateway responsibility. PNC adoption does not imply gateway responsibility.

## Execution boundary

No validation result, generation result, generated artifact, compile/link result, deployed binary, runtime transition, bus-off recovery result, wakeup result, application-availability result, timing measurement, requirement comparison, verdict, or coverage result is claimed by this publication.

## Publication policy

This topic is published on the dedicated branch:

`publish/management-ecu-communication-mode-network-management-engineering-20260907`

Public `main` is intentionally not merged by this publication workflow.
