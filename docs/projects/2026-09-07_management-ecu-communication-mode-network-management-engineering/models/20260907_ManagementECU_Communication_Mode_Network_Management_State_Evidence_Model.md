# Management ECU Communication Mode & Network Management
# State and Evidence Model

Date: 2026-09-07 JST
Status: LUNA_CURRENT_PACKAGE_COMPILED_PROPOSAL

This model uses the accepted baseline at 56f753e5f605f7441b957490c36080f067bb0807,
the AUTOSAR overlay at a7d063d4fb020e565497388c2c6cea5c2605a1ed and the Vector
overlay at 9b1e1a1fb172cb43466b89f07a1c22f9a8e00990. It contains no configured
value or runtime result.

## Non-automatic evidence chain

    project demand / requirement
      -> ComM user and valid user request
      -> stored request
      -> user/channel relationship and aggregation
      -> channel target / ComM evaluation
      -> BusSM actual-mode indication
      -> CanSM request and CanSM_MainFunction processing
      -> CanIf/controller/transceiver indication
      -> Nm/CanNm request, notification and protocol state
      -> BswM arbitration/rule/action-list execution
      -> COM I-PDU Group control and COM processing state
      -> runtime network/wakeup/bus-off/application-availability observation
      -> requirement comparison -> verdict -> coverage

Every arrow is a separate handoff; no upstream state proves downstream state.

## State/evidence planes

| ID | Plane | May be asserted if supplied | Must not be inferred |
|---|---|---|---|
| S0 | Project demand/requirement | accepted demand and owner | ComM user, channel, route or runtime |
| S1 | ComM user/request | accepted ComMUser and request category | stored request, target or actual mode |
| S2 | Stored request and aggregation | accepted state and mapping | BusSM/CanSM mode or physical bus |
| S3 | Channel target/evaluation | target/state-machine artifact | lower-layer completion |
| S4 | BusSM actual indication | state handoff | controller/transceiver or physical completion |
| S5 | CanSM processing | request/main-function/transition evidence | NM state or recovered bus |
| S6 | Lower-layer indication | callback/status | physical recovery |
| S7 | Nm/CanNm request/protocol | request/release/passive-start evidence | ComM/CanSM/physical state |
| S8 | BswM arbitration/action | rule and action evidence | ownership or application availability |
| S9 | COM I-PDU Group | start/stop/initialization evidence | application readiness or bus state |
| S10 | Runtime observation | named observation with stimulus | requirement satisfaction/verdict/coverage |
| S11 | Requirement comparison | explicit criteria comparison | approval without decision rule |
| S12 | Verdict | accepted decision rule/result | coverage |
| S13 | Coverage | measured scope and accounting | unobserved-layer proof |

## Critical boundaries

COMM_SILENT_COMMUNICATION is not a user-requested mode. ComM request, stored
request, target and BusSM indication are not one state. CanSM request,
main-function processing, CanIf indication and physical completion are not one
state. CanSM_ControllerBusOff is not recovered-bus evidence. CanTrcv WUF/status,
CANSM_BSM_WUVALIDATION and EcuM_ValidateWakeupEvent are separate. CanNm
requested/released, operational and internal protocol states are separate.
PNC ID derivation, EIRA/ERA, ComM PNC state and selective wakeup are separate.
BswM action and BswMPduGroupSwitch are not application availability. COM I-PDU
Group state is not ComM mode, CanSM state or physical bus availability.

## Configuration-to-runtime boundary

    configuration -> validation -> generation -> generated artifact
      -> compile/link -> deployed binary -> runtime transition
      -> observation -> requirement comparison -> verdict -> coverage

No transition is automatic. This package asserts none of these execution results.
Dual CAN is not gateway responsibility, and PNC adoption is not gateway
responsibility.
