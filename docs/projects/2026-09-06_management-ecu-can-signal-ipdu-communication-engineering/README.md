# Management ECU — CAN Signal & I-PDU Communication Engineering

Date: 2026-09-06

## Purpose

This project establishes a provenance-preserving engineering baseline for Management ECU AUTOSAR Classic CAN signal and I-PDU communication from Application SW-C/RTE-facing Sender/Receiver communication through COM, PduR, CanIf and CanDrv to CAN/CAN FD bus observation.

The project deliberately separates application communication semantics, System Description/ECU Extract communication mapping, COM signal/I-PDU processing, PduR routing, CanIf hardware-independent abstraction, CanDrv/controller realization, generated configuration/build artifacts and runtime bus evidence.

It is a decomposition and navigation artifact. It is not a claim that Management ECU-specific signals, I-PDUs, frames, transfer properties, timing values, routes, CAN identifiers, DLCs, controller mappings, generated configuration, runtime transmission behavior or bus timing have been validated.

## Current state

Status: `SOL_BASELINE_INITIALIZED`

No Luna baseline compilation has been executed yet. No Management ECU-specific communication object or value is accepted by this initialization.

Inherited downstream source:

- repository: `eariver/Automotive_EE_Engineering_Knowledge`
- branch: `work/management-ecu-os-rte-timing-scheduling-engineering-20260905`
- exact inherited head: `161a6cd36bda3ef59ab7ace3e0ef3c69e4e9fd2a`

Sol project branch:

- `work/management-ecu-can-signal-ipdu-communication-engineering-20260906`

Planned Luna execution branch:

- `work/luna-management-ecu-can-signal-ipdu-communication-baseline-compilation-20260906`

The exact Luna Starting SHA is the Sol initialization commit containing these control files. It must be supplied externally when the Luna unit is launched; this file does not self-pin that future commit.

## Primary authority

Technical compilation is source-bounded to exact-pinned Sol-reviewed authority in `references/authority-pins.yaml`.

Primary reviewed corpus:

- `eariver/Research_AUTOSAR_CP_Documents@8c67ddc4cc6ce4bba1881a879b933cf2b751d733`
- platform/release: AUTOSAR Classic 4.4.0

The reviewed corpus already provides explicit authority for:

- Sender/Receiver model/runtime separation;
- SW-C port/interface/connector versus runtime realization boundaries;
- System Description -> ECU Extract -> ECU Configuration navigation;
- CAN topology and signal/PDU/frame modeling boundaries;
- minimal non-TP CAN data path: RTE-facing signal interaction -> COM -> PduR -> CanIf -> CanDrv -> CAN hardware;
- PduR IF/TP routing separation;
- CanIf versus CanDrv/CanTrcv hardware ownership;
- conditional CanTp, IpduM, SecOC and transformer stages as non-universal branches;
- ComM/CanSM communication-state ownership as a separate plane from this data-path project.

The reviewed corpus does not by itself establish:

- Management ECU-specific communication object identities or values;
- complete COM configuration semantics for every COM-001..COM-018 task;
- exact project-specific DaVinci Developer/Configurator Classic or MICROSAR COM/PduR/CanIf/CanDrv procedure;
- generated/build correctness;
- physical CAN/CAN FD runtime transmission, timing, verdict or coverage evidence.

## Project control files

- `20260906_ManagementECU_CAN_Signal_IPDU_Communication_Project_Scope.md`
- `references/authority-pins.yaml`
- `references/project/can-signal-ipdu-communication-project-input-baseline.yaml`
- `luna/2026-09-06_can-signal-ipdu-communication-baseline-compilation-plan.md`
- `luna/2026-09-06_can-signal-ipdu-communication-baseline-compilation-instruction.md`
- `../../prompts/2026-09-06_luna-management-ecu-can-signal-ipdu-communication-baseline-compilation.md`

## Canonical navigation model

```text
Application SW-C data semantics
-> Sender/Receiver port/interface contract
-> RTE-facing communication access
-> System Description / ECU Extract communication mapping
-> COM Signal / SignalGroup
-> COM I-PDU packing / transmission / reception semantics
-> PduR communication-interface routing
-> CanIf L-PDU / controller-independent abstraction
-> CanDrv controller/hardware request
-> CAN controller / CAN or CAN FD frame
-> physical bus observation
-> requirement comparison
-> verdict / coverage
```

This is a navigation model, not a project-specific configured route.

## Non-collapse rules

Do not collapse:

- Application data element != R-Port/P-Port != COM Signal != SignalGroup != I-PDU;
- System Description mapping != ECU Extract != ECU Configuration Values != generated configuration;
- COM signal gatewaying != PduR I-PDU routing;
- PduR communication-interface route != transport-protocol route;
- CanIf Tx/Rx PDU identity != CAN frame identity != hardware mailbox/controller object;
- CanIf != CanDrv;
- Com_SendSignal request != COM processing completion != PduR forwarding != CanIf transmit request != CanDrv hardware request != TxConfirmation != observed bus frame;
- configured cycle/repetition/timeout value != measured bus timing;
- configured CAN ID/DLC/frame mapping != observed physical traffic;
- generation success != compile/link success != deployment success != runtime communication evidence;
- raw bus sample != requirement != verdict != coverage;
- VECU/SIL communication behavior != physical-target CAN/CAN FD behavior.

## Explicit project boundary

This project is the CAN signal/I-PDU **data plane**. It does not absorb the separate communication-state/network-management plane.

Out of this baseline except for retained boundary references:

- ComM;
- CanSM;
- Nm/CanNm;
- PNC;
- wakeup/sleep coordination;
- SecOC security design;
- E2E protection design;
- IpduM multiplexing design;
- diagnostic CanTp/UDS behavior already covered by the UDS topic;
- gateway responsibility unless the Management ECU is separately established as a gateway.

Unsupported points remain explicit gaps rather than inferred semantics, values or procedures.
