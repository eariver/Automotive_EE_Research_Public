# Management ECU CAN Signal / I-PDU Communication
# Step-by-Step Engineering Guide

Date: 2026-09-06
Status: LUNA_CURRENT_PACKAGE_COMPILATION_PROPOSAL
Scope: COM-001 through COM-018 only

## How to use this guide

This is a project-navigation guide compiled from exact-pinned Sol-reviewed
authority. It is not a configuration recipe containing Management ECU values.
At every step, use an accepted project artifact or leave the field unresolved.
Do not turn an AUTOSAR object name into a vendor GUI field, product command,
generated filename or runtime claim.

The governing authority tuples are:

- A-PRIMARY: eariver/Research_AUTOSAR_CP_Documents @
  8c67ddc4cc6ce4bba1881a879b933cf2b751d733, AUTOSAR Classic Platform 4.4.0.
- A-COM: eariver/Research_AUTOSAR_CP_Documents @
  fc05fc7824d56b1a34eaf42e3d50150ff70a789d,
  docs/knowledge/management-ecu-can-signal-ipdu-autosar-semantic-depth.md.
- V-COM: eariver/Research_Vector_Documents @
  138dba4d76bc9cf7fadec1ee818aa7e6b9db4b70,
  docs/knowledge/management-ecu-com-vector-procedure.md.

## Step 0 — Establish control state

1. Confirm the execution branch and exact Starting SHA in the terminal
   checkpoint.
2. Read the project Scope, authority pins and project-input baseline.
3. Confirm that generic AUTOSAR COM and Vector/MICROSAR research is closed.
4. Create no new branch and do not modify authority, baseline, knowledge,
   prompt or sibling-project files.

Input state: current project controls and unresolved project-input register.  
Output state: a source-bounded work session with no selected project values.  
Exit: authority and write scope are fixed.

## Step 1 — Establish the application and RTE contract

### COM-002 — Sender/Receiver to RTE boundary

Identify the accepted SenderReceiverInterface, VariableDataPrototype,
P-Port/R-Port and Connector model elements. Classify each access as the
explicit DataSendPoint/DataReceivePoint form or the implicit
DataReadAccess/DataWriteAccess form. Preserve the reviewed category constraint
and snapshot/write-back distinction.

Input: accepted SW-C/RTE contract.  
Operation: map only supplied model identities and access category.  
Output: application-to-RTE access map, not a COM object or generated API.  
Exit: each access is accepted, category-valid, or explicitly blocked.  
Handoff: system/ECU mapping and separately established COM identity.

## Step 2 — Establish the system-to-ECU work products

### COM-003 — System Description, ECU Extract and ECU configuration

Identify the system-side communication model and the targeted ECU view. Use the
ECU Extract as the ECU-specific system-side input and keep ECU Configuration
Values as the actual per-ECU configuration work product. System Extract and ECU
System Description remain supported refinement lanes, not mandatory steps for
every project.

Input: accepted System Description and ECU Extract, if supplied.  
Operation: record source work-product roles and explicit mappings.  
Output: ECU-specific configuration input boundary.  
Exit: one target ECU and the relevant communication subset are accepted, or
missing identity remains PROJECT_INPUT_REQUIRED.  
Handoff: COM Signal/I-PDU mapping and configuration preparation.

## Step 3 — Establish the data-plane architecture

### COM-001 — CAN communication architecture

Use the reviewed minimal non-TP navigation:

    RTE-facing signal interaction
    -> COM signal-oriented processing and I-PDU packing
    -> PduR configured I-PDU forwarding
    -> CanIf CAN-hardware-independent abstraction
    -> CanDrv controller access
    -> CAN controller and physical bus observation

Classify ownership before selecting any route. CanTp, IpduM, SecOC,
E2E/transformers and gatewaying are conditional.  

Input: accepted application/system/ECU model and route responsibility.  
Operation: decompose layers and mark optional branches.  
Output: project-neutral data-plane map.  
Exit: all route identities are supplied or remain blocked.  
Handoff: COM, PduR, CanIf and CanDrv-specific tasks.

## Step 4 — Establish COM object and representation semantics

### COM-004 — Signal and SignalGroup ownership

Keep ComSignal, ComGroupSignal, ComSignalGroup and ComIPdu as distinct
containers. Resolve foreign System Template references only when accepted
System Template/project evidence is available. Choose neither a group access
alternative nor a concrete identity by default.

Input: accepted System Template and COM object references.  
Operation: map explicit references and retain object-level identity.  
Output: COM object map with conditional normal shadow-buffer or UINT8-array
access branch.  
Exit: object identity, group access choice and linkage are accepted, or
PROJECT_INPUT_REQUIRED remains.  
Handoff: packing and position.

### COM-005 — Packing, representation and positioning

Keep ComBitPosition, ComBitSize, ComSignalType, ComSignalLength and
ComSignalEndianness as separate configuration dimensions. A dynamic-length
branch is conditional. Do not select bit position, length, byte order or frame
payload from an example.

Input: accepted ISignal-to-I-PDU and Pdu-to-Frame mapping plus COM objects.  
Operation: reconcile only supplied placement and representation values.  
Output: mapping/layout input set, not an observed payload.  
Exit: all positions and representation choices have project support.  
Handoff: Tx/Rx behavior and CAN frame configuration.

## Step 5 — Establish transmit behavior

### COM-006 — Transfer, Tx mode and repetition

Keep ComTransferProperty distinct from ComTxModeMode, TMS/filter selection,
repetition count/period and cyclic offset/period. A configured value is not a
measured bus timing result.

Input: accepted I-PDU direction and Tx policy.  
Operation: classify each behavior dimension independently.  
Output: Tx behavior configuration checklist with no default mode or timing.  
Exit: all choices are accepted or remain blocked.  
Handoff: Tx request/confirmation and measurement.

### COM-007 — Tx request, forwarding and confirmation

Trace the layer ownership of a transmit request through COM, PduR, CanIf and
CanDrv. Keep COM request, COM processing completion, lower-layer forwarding,
physical transmission and TxConfirmation separate. The reviewed architecture is
not a universal synchronous API sequence.

Input: accepted route and interface bindings.  
Operation: assign evidence labels to each layer.  
Output: layer-separated Tx handoff model.  
Exit: route and confirmation bindings are explicit, or blocked.  
Handoff: lower-layer observation and runtime evidence.

## Step 6 — Establish receive and data-quality behavior

### COM-008 — Rx indication and application delivery

Classify Com_RxIndication and COM immediate/deferred processing separately from
RTE/SWC consumption. In the deferred case retain indication, internal copy,
Com_MainFunctionRx processing and later receive access as separate stages.

Input: accepted Rx I-PDU and delivery contract.  
Operation: map lower-layer indication to COM processing and RTE access.  
Output: project-neutral Rx path.  
Exit: application delivery and consumption evidence are separately defined.  
Handoff: update, invalid, timeout and observation tasks.

### COM-009 — Update, invalid, substitution and notification

Treat update-bit state, receiver filter outcome, invalid-value action,
initialization/substitution value and notification contract as separate
decisions. Do not infer callback identity or application validity.

Input: accepted Rx policy and callback contract.  
Operation: record independent policy dimensions.  
Output: data-quality decision register.  
Exit: semantic and project policy are accepted, or remain blocked.  
Handoff: timeout interaction and runtime evidence.

### COM-010 — Deadline and timeout

Keep ComFirstTimeout, ComTimeout, monitoring enablement, timer state,
ComRxDataTimeoutAction, ComTimeoutSubstitutionValue and notification separate.
A timeout callback or software state is not a physical timing observation.

Input: accepted I-PDU Group and timeout policy.  
Operation: define monitor state and expected evidence layers.  
Output: deadline/timeout configuration and verification checklist.  
Exit: values, action and evidence source are accepted, or blocked.  
Handoff: I-PDU Group control, measurement and verdict.

### COM-011 — I-PDU Group control

Keep COM-owned I-PDU Group start/stop and deadline-monitoring control separate
from ComM mode, CanSM state, controller state, transceiver state and physical
bus availability. Do not choose an external owner from the COM semantic
authority alone.

Input: accepted COM group identity and lifecycle design.  
Operation: record COM control contract and independent mode-plane interaction.  
Output: group-control design boundary.  
Exit: group state ownership and interaction are accepted, or blocked.  
Handoff: COM configuration and runtime group-state evidence.

## Step 7 — Establish routing and CAN hardware boundaries

### COM-012 — PduR IF/TP routing

Classify every supplied route as communication-interface, transport-protocol or
unestablished. PduR IF and TP gatewaying use different API/buffering semantics;
PduR does not provide generic IF-to-TP conversion. Signal-level COM gatewaying
is distinct from transparent PduR I-PDU routing.

Input: source/destination PDU identities and gateway/TP decision.  
Operation: classify route type and conditional branch.  
Output: PduR route register.  
Exit: route class and gateway responsibility are accepted, or blocked.  
Handoff: CanIf/CanDrv and execution evidence.

### COM-013 — CanIf abstraction

Keep CanIf Tx/Rx PDU and controller-independent control/data flow distinct from
CanDrv controller access and physical frame identity.

Input: accepted CanIf PDU/controller references.  
Operation: map only supplied upper/lower bindings.  
Output: CanIf ownership boundary.  
Exit: PDU/controller/HTH/HRH values are accepted or remain unresolved.  
Handoff: controller/hardware and frame configuration.

### COM-014 — CanDrv/controller/hardware

Keep CanDrv controller access and CanTrcv transceiver operation distinct. A
driver request or TxConfirmation is not proof of successful physical
transmission.

Input: accepted controller, driver, mailbox and transceiver design.  
Operation: record hardware ownership and evidence layers.  
Output: controller/hardware integration boundary.  
Exit: target mapping and physical observation plan are accepted or blocked.  
Handoff: CAN/CAN FD model and measurement.

### COM-015 — CAN/CAN FD frame and bus configuration

Use the reviewed topology/model terms without selecting a cluster, channel,
frame ID, DLC, CAN/CAN FD choice or bit timing. Configuration values belong to
the project input register.

Input: accepted CAN topology, frame and bus design.  
Operation: keep model configuration distinct from observed traffic.  
Output: frame/bus configuration checklist.  
Exit: all concrete values and physical channel responsibilities are accepted.  
Handoff: package validation, generation and physical evidence.

## Step 8 — Establish package, observation and evidence handoff

### COM-016 — Configuration, validation, generation and build

Use the reviewed Vector authority only as already classified. Retain aggregate
PARTIAL_PROCEDURE_AVAILABLE. The following generic subprocedures are exact but
do not close COM-specific artifacts or build/runtime evidence:

    dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
    dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
    dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"

Input: accepted ECU Configuration Values, product project and toolchain.  
Operation: keep configuration, validation, generation, compile/link and runtime
states separate.  
Output: package handoff and evidence ledger.  
Exit: actual project runs and artifacts are available, or blockers remain.  
Handoff: build owner and COM-018 execution evidence.

### COM-017 — Observation points

Define observation layers without inventing instrumentation:
RTE/application access, COM buffer/callback, PduR/CanIf, CanDrv/controller and
physical CAN trace. A configured route is not an observation plan.

Input: accepted verification architecture and tool/trace ownership.  
Operation: assign observation points and correlation keys.  
Output: observation plan with no claimed measurements.  
Exit: instruments, stimuli and trace source are accepted or blocked.  
Handoff: runtime execution and verdict.

### COM-018 — Runtime evidence, verdict and coverage

Collect independently:

    configured intent
    -> validation result
    -> generated artifact
    -> compile/link result
    -> runtime request/processing/forwarding
    -> observed CAN frame/timing/state
    -> requirement comparison
    -> verdict
    -> coverage

No earlier state proves a later state. VECU/SIL evidence does not automatically
prove physical-target CAN behavior.

Input: accepted stimuli, expected values/frames, requirements and evidence plan.  
Operation: execute and correlate each evidence layer.  
Output: execution package, verdict and coverage record.  
Exit: every required layer is traceable, or EXECUTION_EVIDENCE_REQUIRED remains.  
Handoff: Sol fixed-head review.

## Step 9 — Final validation before compilation commit

Confirm all of the following:

- exactly 18 task identities occur once in each YAML matrix;
- no nineteenth task, duplicate or extra row exists;
- primary availability counts sum to 18;
- fixed Vector classifications are unchanged;
- each supported technical claim points to an exact authority tuple;
- project input and project design blockers are distinct from procedure maturity;
- execution evidence is not inferred from configuration or generation;
- CanTp, IpduM, SecOC, E2E/transformers and gatewaying remain conditional;
- all required semantic boundaries are visible;
- only the nine allowlisted package paths are staged;
- no upstream repository, docs/knowledge path or control file is changed.

After PASS, create one bounded compilation commit on the existing branch,
push without force, read back the remote HEAD and stop for Sol review.
