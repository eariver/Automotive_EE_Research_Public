# Management ECU CAN Signal / I-PDU Communication
# State and Evidence Model

Date: 2026-09-06
Status: LUNA_CURRENT_PACKAGE_COMPILATION_PROPOSAL

## Authority and purpose

This model is compiled from:

- A-PRIMARY: eariver/Research_AUTOSAR_CP_Documents @
  8c67ddc4cc6ce4bba1881a879b933cf2b751d733, AUTOSAR Classic Platform 4.4.0;
- A-COM: eariver/Research_AUTOSAR_CP_Documents @
  fc05fc7824d56b1a34eaf42e3d50150ff70a789d,
  docs/knowledge/management-ecu-can-signal-ipdu-autosar-semantic-depth.md;
- V-COM: eariver/Research_Vector_Documents @
  138dba4d76bc9cf7fadec1ee818aa7e6b9db4b70,
  docs/knowledge/management-ecu-com-vector-procedure.md.

It defines evidence separation for the current package. It does not contain a
configured Management ECU route or an execution result.

## 1. Required state chain

    project communication requirement / application intent
        -> System Description / ECU Extract / SWC-RTE communication contract
        -> COM / PduR / CanIf / CanDrv configuration
        -> validation result
        -> generated artifact
        -> compile/link result
        -> runtime SWC/COM/lower-layer trace
        -> observed CAN frame/timing/state behavior
        -> requirement comparison
        -> verdict
        -> coverage

Every arrow is a handoff to a separate state/evidence layer. No upstream state
is proof of the downstream state.

## 2. State definitions

| State ID | State / artifact | What may be asserted | What may not be asserted without the next layer |
|---|---|---|---|
| S0 | Requirement and application intent | The project has supplied a communication need or intent | No COM object, route, timing or bus value |
| S1 | System Description / ECU Extract / SWC-RTE contract | Model/work-product identity and accepted mapping inputs | No ECUC value, generated artifact or runtime access |
| S2 | COM / PduR / CanIf / CanDrv configuration | Explicitly accepted configuration values and ownership | No validation success, generation success or runtime behavior |
| S3 | Validation result | A particular project validation run and its recorded result | No generated output, build, bus or verdict |
| S4 | Generated artifact | A particular generated source/configuration artifact and provenance | No compile/link result or runtime behavior |
| S5 | Compile/link result | A particular build result and binary/image identity | No runtime communication or physical bus result |
| S6 | Runtime SWC/COM/lower-layer trace | Observed software execution at named project observation points | No physical CAN frame or requirement verdict by itself |
| S7 | Observed CAN frame/timing/state | Captured bus/controller observation with timestamp and source | No requirement satisfaction, verdict or coverage by itself |
| S8 | Requirement comparison | Measurement-to-requirement comparison using explicit criteria | No approval unless the decision rule is supplied |
| S9 | Verdict | Decision from an accepted comparison rule | No coverage claim unless coverage evidence exists |
| S10 | Coverage | Measured scope, executed cases and result accounting | No new project values or retroactive proof of unobserved layers |

## 3. Artifact identity boundaries

The following are separate identity domains:

- application data element;
- Sender/Receiver port/interface and Connector;
- System Template signal identity;
- COM Signal, GroupSignal and SignalGroup;
- COM I-PDU;
- PduR route;
- CanIf PDU abstraction;
- CAN controller/driver execution;
- observed CAN frame.

Likewise, System Description, ECU Extract, ECU Configuration Values, generated
artifact, runtime state and observed frame are not synonyms. ARXML may be a
representation format; it does not erase semantic work-product boundaries.

## 4. COM state separation

### 4.1 Signal group alternatives

The focused COM authority supports two conditional group-access branches:

    normal shadow-buffer realization
    XOR
    configured UINT8-array realization

The array alternative uses the source-defined array APIs and does not allocate
the normal group shadow buffer for that configured group. Neither branch is a
Management ECU default.

### 4.2 Transmission states

Keep these independent:

    ComTransferProperty
    != ComTxModeMode / TMS selector
    != repetition count/period
    != periodic offset/period
    != ComTxTimeBase
    != OS Task schedule
    != observed bus timing

The software path may be represented as a boundary:

    COM send request / trigger condition
        -> COM processing
        -> PduR_ComTransmit
        -> lower-layer processing
        -> Com_TxConfirmation where applicable

Com_TxConfirmation is software-interface completion information, not proof of
physical CAN transmission.

### 4.3 Reception and data quality

Keep these independent:

    Com_RxIndication
    != immediate/deferred COM processing
    != update-bit state
    != receiver-filter result
    != invalid-value action
    != timeout action/substitution
    != notification callback
    != RTE/SWC consumption

An unset update-bit is not an invalid-value action and neither is a timeout.
Configured callback identity is not callback execution or application
consumption.

### 4.4 I-PDU Group and communication mode

COM I-PDU Group start/stop and deadline-monitoring control are distinct from
ComM target communication mode, CanSM actual CAN-network state, controller state,
transceiver state and physical bus availability. No external owner is selected
from the COM SWS alone.

## 5. Conditional route model

The minimal non-TP navigation is:

    RTE-facing signal interaction
        -> COM
        -> PduR
        -> CanIf
        -> CanDrv
        -> CAN controller / physical bus

Conditional stages are inserted only when accepted evidence establishes them:

| Conditional item | Boundary retained |
|---|---|
| CanTp | Segmentation/reassembly branch; not mandatory for each signal/I-PDU |
| IpduM | Multiplex/container processing; not a generic routing stage |
| SecOC | PDU security processing; separate from PduR routing and crypto service ownership |
| E2E / transformers | Conditional configured transformation/protection stage |
| COM signal gatewaying | Signal-level COM mapping, distinct from transparent PduR I-PDU routing |
| gateway responsibility | Project decision; dual CAN does not establish gatewaying |

## 6. Evidence record schema

Each evidence item should carry:

| Field | Required meaning |
|---|---|
| evidence_id | Stable project evidence identifier |
| task_id | One of the 18 package task identities |
| layer | Model, configuration, validation, generation, build, runtime, bus, comparison, verdict or coverage |
| source_artifact | Exact input or output artifact identity |
| source_revision | Exact commit, version or execution revision |
| observation_point | Named point only when supplied by project design |
| operation | Configuration operation or runtime activity |
| state_before / state_after | Separate states, not inferred transitions |
| timestamp | Required for execution/measurement evidence |
| correlation_key | Link to the upstream/downstream evidence item |
| acceptance_rule | Explicit project requirement or comparison rule |
| result | Observed result only; never a fabricated expected value |
| authority_tuple | Exact reviewed authority for static technical claims |

No evidence record may silently promote a configuration value into a measured
result or a raw trace into a verdict.

## 7. Promotion gates

| Gate | Required evidence | Boundary |
|---|---|---|
| G1 contract accepted | SW-C/RTE and system/ECU model inputs | Model is not COM configuration |
| G2 configuration accepted | COM/PduR/CanIf/CanDrv values and conditional-route decisions | Configuration is not validation |
| G3 validation passed | Actual validation run output | Validation is not generation |
| G4 generation completed | Exact generated artifact set | Generation is not build |
| G5 build completed | Compile/link result and binary identity | Build is not runtime |
| G6 runtime observed | Layer-correlated software records | Software trace is not physical bus proof |
| G7 bus correlated | Physical or approved target CAN observation | Observation is not verdict |
| G8 verdict accepted | Requirement comparison and decision rule | Verdict is not coverage |
| G9 coverage accepted | Coverage definition, executed scope and result accounting | No retroactive expansion of evidence |

COM-018 remains EXECUTION_EVIDENCE_REQUIRED until these gates are populated by
project artifacts and execution. VECU/SIL behavior does not automatically
establish physical-target CAN behavior.

## 8. Package closure state

Current package state:

- architecture and semantic authority: reviewed and available at pinned scope;
- product procedure maturity: preserved separately by task;
- project communication values/design: unresolved;
- generated artifact/build/runtime evidence: absent;
- requirement verdict/coverage: absent;
- final maturity: pending Sol fixed-head review.
