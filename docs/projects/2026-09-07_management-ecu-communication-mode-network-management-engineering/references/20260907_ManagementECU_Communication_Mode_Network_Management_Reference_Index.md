# Management ECU Communication Mode & Network Management
# Reference Index

Date: 2026-09-07 JST
Status: LUNA_CURRENT_PACKAGE_COMPILED_PROPOSAL

## Load-bearing exact authority tuples

- BASELINE_ACCEPTED: eariver/Automotive_EE_Engineering_Knowledge@56f753e5f605f7441b957490c36080f067bb0807
  Accepted review, report, baseline YAML and gap backlog; historical and read-only.
- AUTOSAR_FOCUSED_CNM: eariver/Research_AUTOSAR_CP_Documents@a7d063d4fb020e565497388c2c6cea5c2605a1ed
  docs/knowledge/management-ecu-communication-mode-network-management-autosar-semantic-depth.md
  and the Sol review checkpoint.
- VECTOR_FOCUSED_CNM: eariver/Research_Vector_Documents@9b1e1a1fb172cb43466b89f07a1c22f9a8e00990
  docs/knowledge/management-ecu-communication-mode-network-management-vector-procedure.md
  and the Sol review checkpoint.
- AUTOSAR_RETAINED_BASELINE: eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d
  Older exact context explicitly accepted by the baseline; not floating.

## Baseline artifacts consumed read-only

- checkpoints/2026-09-07_sol-communication-mode-network-management-baseline-review.md
- 20260907_ManagementECU_Communication_Mode_Network_Management_Baseline_Report.md
- baseline/20260907_ManagementECU_Communication_Mode_Network_Management_Baseline.yaml
- research/20260907_ManagementECU_Communication_Mode_Network_Management_Research_Gap_Backlog.yaml

## Reviewed overlay locators

AUTOSAR section 1 and A1 decisions: ComM user/request/channel and aggregation.
Section 2 and A2 decisions: channel modes, Silent Communication,
CommunicationAllowed, inhibition and limitation. Section 3 and A3 decisions:
CanSM request/main-function/lower-layer/bus-off. Section 4: CanNm
request/release/passive-start with GC10 Car Wakeup reused. Section 5 and A4:
BswM arbitration, action ordering, PDU-group switching and application-
availability separation. Section 6: task-level closure.

Vector section 3: Communication Users CRUD/channel connect. Section 4:
ComMPncID Counting Mode and NM_MESSAGE/PNC_VECTOR. Section 5: CanSM/CanNm
bounded negatives. Section 6: BswM Communication Control. Section 7:
generic validate/generate/schema commands and CNM-016 limitation. Section 8:
final ten-slice classifications.

## Source-policy boundary

No raw licensed Vector HELP, raw AUTOSAR PDF, private Drive bytes, Web/current
vendor page or floating main/branch head was copied or used as new evidence.
No project-specific value is present.
