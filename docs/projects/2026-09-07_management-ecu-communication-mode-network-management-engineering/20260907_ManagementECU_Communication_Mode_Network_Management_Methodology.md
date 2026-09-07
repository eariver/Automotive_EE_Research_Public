# Management ECU Communication Mode & Network Management
# Methodology

Date: 2026-09-07 JST
Status: LUNA_CURRENT_PACKAGE_COMPILED_PROPOSAL
Authority mode: exact-pinned Sol-reviewed compilation only

## Purpose

Compile the accepted CNM baseline with reviewed semantic and product overlays. This
is a reasoning and handoff method, not an executed Management ECU configuration.
AUTOSAR semantics, Vector procedure, project input/design and execution evidence
are independent dimensions.

## Layered engineering flow

1. Accept only project-supplied application or BSW communication demand; do not
   call it a ComM user or channel without project mapping.
2. Keep ComMUser/request identity and valid request categories separate from
   COMM_SILENT_COMMUNICATION, a channel/synchronization state rather than a
   user-request value.
3. Keep stored request, user-channel relationships, channel target and BusSM
   actual/current indication separate; a target may differ temporarily.
4. Keep ComM/Nm requests separate from CanSM main-function processing, CanIf
   indication, controller/transceiver completion and physical bus observation.
5. Keep ComM -> Nm -> BusNm request separate from BusNm -> Nm -> ComM feedback.
   Nm adaptation is not CanNm protocol state, and CanNm request/release/passive
   start is not EcuM validation.
6. Treat BswM mode indications as arbitration inputs. Rule evaluation and action
   lists are separate from ComM/CanSM/Nm/CanNm and EcuM lifecycle ownership.
7. Treat BswMPduGroupSwitch and COM I-PDU Group processing as a control handoff,
   not application availability, ComM mode, CanSM state or physical bus.
8. Only after project design exists can validation, generation, artifact,
   compile/link, runtime, requirement, verdict and coverage be evidenced.

## Authority overlay method

Read the accepted baseline as historical context. Apply the a7d063d4 AUTOSAR
overlay only at bounded focused depth and reuse the fixed 9b1e1a1f Vector
classification without reopening HELP research. Retain older exact AUTOSAR
context only where already accepted by the baseline. Missing product procedure is
a bounded negative, not a capability absence claim.

## Handoff phases

| Phase | Exit question | Handoff |
|---|---|---|
| Scope/ownership | Are plane owners and boundaries named? | requirements/architecture |
| Demand/user/channel | Are demand, user, request, channel and target distinct? | ComM mapping/design |
| ComM policy/mode | Are request/release/indication/limitation separate? | ComM policy owner |
| CanSM/lower layer | Are processing, indication, bus-off and wakeup separate? | CanSM/wakeup design |
| Nm/CanNm/PNC | Are adaptation, protocol, identity and aggregation separate? | NM/PNC policy owner |
| BswM/COM handoff | Are arbitration, action, group and availability separate? | BswM/COM/application |
| Product workflow | Is product support distinguished from generic workflow? | tool/package authority |
| Project design | Are values, ownership and criteria supplied? | execution plan |
| Evidence | Are artifact, build, runtime, verdict and coverage planes present? | verification owner |

This package is ready for Sol fixed-head review only.
