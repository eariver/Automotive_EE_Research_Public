# Management ECU CAN Signal & I-PDU Communication Project Scope

Date: 2026-09-06

## 1. Objective

Build a bounded, source-explicit engineering baseline for Management ECU AUTOSAR Classic CAN signal and I-PDU communication while preserving the distinction between application communication semantics, RTE-facing access, system/ECU communication mapping, COM processing, PduR routing, CanIf abstraction, CanDrv hardware realization and observed CAN/CAN FD runtime evidence.

This baseline is a decomposition/navigation artifact. It does not claim project-specific signal correctness, communication timing, generated correctness, bus-load feasibility, target transmission behavior, deadline satisfaction or safety sufficiency.

## 2. In scope

- Application Sender/Receiver communication boundary and RTE-facing runtime access at reviewed depth.
- System Description, ECU Extract and ECU Configuration Values as distinct work products.
- CAN topology and ISignal/I-PDU/frame mapping semantics where reviewed authority supports them.
- COM Signal and SignalGroup ownership and interaction at reviewed depth.
- COM I-PDU packing/unpacking and Tx/Rx processing only where exact-reviewed authority supports the claim.
- Tx transfer/trigger/repetition/confirmation semantics only where exact-reviewed authority supports them.
- Rx indication, update/invalid/notification and timeout/deadline monitoring semantics only where exact-reviewed authority supports them.
- COM I-PDU Group control only where exact-reviewed authority supports it.
- PduR communication-interface routing and IF/TP separation.
- CanIf CAN-hardware-independent L-PDU/control abstraction.
- CanDrv/controller/hardware ownership boundary.
- CAN/CAN FD frame/configuration boundary at reviewed depth.
- configuration/generation/build/tool-procedure availability as a separate maturity axis.
- runtime observation, measurement, requirement, verdict and coverage as distinct evidence layers.

## 3. Out of scope for this baseline

- invention of Management ECU signal, SignalGroup, I-PDU, PduR route, CanIf PDU, frame, controller or channel identities;
- invention of CAN IDs, frame formats, DLCs, signal bit positions, endianness, scaling, update-bit policy, invalid values, transfer properties, periods, repetitions or timeout values;
- invention of DaVinci Developer/Configurator Classic or MICROSAR GUI/CLI procedure without reviewed product/release authority;
- treating CanTp as a mandatory stage in every CAN route;
- treating IpduM, SecOC or E2E/transformer stages as universally present;
- assuming the Management ECU is a gateway;
- ComM/CanSM/Nm/CanNm/PNC/wakeup/sleep state-machine design;
- generated configuration acceptance without generation/build evidence;
- physical-target runtime claims from static configuration or VECU/SIL behavior;
- timing/verdict/coverage claims without observed evidence and explicit requirements.

## 4. Canonical engineering chain

Use this navigation model without collapsing adjacent artifacts:

```text
Application data semantics
-> Sender/Receiver port/interface
-> RTE-facing access
-> System Description communication model
-> ECU Extract
-> ECU Configuration Values
-> COM Signal / SignalGroup
-> COM I-PDU processing
-> PduR IF routing
-> CanIf PDU/control abstraction
-> CanDrv controller/hardware access
-> CAN controller / CAN or CAN FD frame
-> physical bus observation
-> requirement comparison
-> verdict
-> coverage
```

Conditional branches such as CanTp, IpduM, SecOC and transformer/E2E processing are inserted only when separately established for a concrete route.

## 5. Mandatory task set

The first Luna baseline compilation must contain exactly these 18 task identities and must not add a nineteenth task.

- `COM-001` CAN communication architecture, ownership and data-path baseline
- `COM-002` Application Sender/Receiver interface to RTE communication boundary
- `COM-003` System Description / ECU Extract / ECU-specific communication mapping
- `COM-004` COM Signal / SignalGroup semantics and ownership
- `COM-005` Signal-to-I-PDU packing, representation and positioning boundary
- `COM-006` Tx transfer property, transmission mode, trigger and repetition semantics
- `COM-007` Tx request, lower-layer forwarding and confirmation path
- `COM-008` Rx indication, unpacking and application delivery path
- `COM-009` update, invalid, substitution and notification semantics
- `COM-010` deadline monitoring and timeout handling boundary
- `COM-011` COM I-PDU Group start/stop/control boundary
- `COM-012` PduR communication-interface routing and IF/TP separation
- `COM-013` CanIf Tx/Rx PDU and CAN hardware-abstraction boundary
- `COM-014` CanDrv/controller/hardware transmission-reception boundary
- `COM-015` CAN/CAN FD frame, payload-length and configuration boundary
- `COM-016` communication configuration, validation, generation, compile/link and vendor-procedure availability
- `COM-017` communication measurement and observation points from SW-C to bus
- `COM-018` runtime execution evidence, requirement verdict and coverage

## 6. Hard semantic boundaries

The compilation must preserve all of the following.

1. Application data element != Sender/Receiver port/interface.
2. Sender/Receiver model element != runtime RTE access.
3. RTE access != COM Signal identity.
4. COM Signal != SignalGroup != I-PDU.
5. ISignal/System Template mapping != COM runtime buffer state.
6. System Description != ECU Extract != ECU Configuration Values.
7. COM signal gatewaying != PduR I-PDU routing.
8. PduR IF routing != PduR TP routing.
9. CanTp is conditional, not universally present.
10. CanIf PDU/control abstraction != CanDrv hardware ownership.
11. CanIf PDU identity != physical CAN frame observation.
12. CanDrv transmit request != successful physical transmission.
13. Tx request != TxConfirmation != bus observation.
14. configured transfer property/period/repetition != measured bus timing.
15. configured CAN ID/DLC/bit position != observed physical traffic.
16. IpduM/SecOC/E2E/transformer stages are conditional and must not be silently inserted.
17. data-plane communication != ComM/CanSM/Nm network-state management.
18. configuration != validation != generation != compile/link != deployment != runtime evidence.
19. measured communication behavior != communication requirement != verdict != coverage.
20. VECU/SIL communication behavior != physical-target CAN/CAN FD behavior.

## 7. Project-owned inputs that must not be invented

- Application SW-C, port, interface and data-element identities
- sender/receiver direction and multiplicity
- ISignal, ISignalGroup and mapping identities
- COM Signal and SignalGroup identities
- signal length, type, bit position, byte order and conversion/scaling policy
- invalid/substitution values and update-bit policy
- COM I-PDU identity, direction and payload length
- transfer property, transmission mode and trigger policy
- cyclic period, repetition count/period and minimum delay time
- deadline-monitoring/timeout values and timeout actions
- notification/callback identities
- COM I-PDU Group identities and start/stop policy
- PduR route/source/destination identities
- CanIf Tx/Rx PDU identities
- CAN controller/channel/transceiver identities
- CAN/CAN FD frame identity, CAN ID, addressing format and DLC/payload length
- controller/HTH/HRH/mailbox mapping where applicable
- bus baud-rate/data-rate and timing configuration
- tool versions and MICROSAR package/release
- generated artifacts, compiler/linker/build baseline and deployment image
- runtime instrumentation and CAN trace source
- test vectors, expected frames/timing, acceptance thresholds and verdict criteria
- coverage requirement and observed coverage

## 8. Authority use

Use only exact-pinned reviewed authority declared in `references/authority-pins.yaml` for technical claims during the first Luna compilation.

Do not use raw AUTOSAR PDFs, floating upstream heads, Web/current vendor documentation, generic model knowledge or sibling worklogs/prompts as technical authority in that unit.

The exact-pinned reviewed corpus supports a substantial CAN communication architecture/navigation baseline. Missing COM detail for a task must remain an explicit semantic-depth gap rather than being filled from model knowledge.

## 9. Special gap handling

- `COM-006`, `COM-009`, `COM-010` and `COM-011` must not be assumed complete merely because the high-level CAN data path is reviewed; classify exact depth from the pinned entries.
- `COM-012` must preserve communication-interface routing versus transport-protocol routing.
- `COM-016` exact Vector/MICROSAR procedure availability is independent of AUTOSAR semantic authority.
- `COM-017` a configured route is not an observation plan; identify safe observation layers without inventing project instrumentation.
- `COM-018` generation/build success, TxConfirmation and a raw CAN trace are not by themselves requirement verdict or coverage.

## 10. Completion criteria for baseline compilation

The first Luna unit is complete when it produces exactly four allowlisted outputs containing:

- one current baseline row for every `COM-001` through `COM-018`;
- exact-pinned provenance per supported row;
- explicit authority/procedure/project-input/execution gaps;
- preserved semantic boundaries;
- no invented Management ECU communication values;
- a future research-gap decomposition;
- a human-readable synthesis and completion checkpoint;
- validated task cardinality and write allowlist.

A local semantic-depth gap must not downgrade independent reviewed CAN architecture. Missing exact vendor procedure must not be replaced by an inferred tool procedure from AUTOSAR semantics.
