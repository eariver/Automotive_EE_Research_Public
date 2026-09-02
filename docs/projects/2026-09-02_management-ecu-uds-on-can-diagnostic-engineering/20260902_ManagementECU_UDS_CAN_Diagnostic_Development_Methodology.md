# Management ECU — UDS on CAN Diagnostic Development Methodology

**Date:** 2026-09-02  
**Protocol scope:** UDS on CAN  
**Canonical application implementation route:** DaVinci Developer Classic + AUTOSAR Blockset + Simulink/Stateflow + Embedded Coder

## 1. Purpose

This methodology defines how diagnostic specification, Application SWC engineering, AUTOSAR diagnostic BSW configuration, VECU construction and diagnostic verification are separated and connected for a Management ECU.

It is a process/ownership methodology. It does not define concrete DID numbers, routine identifiers, DTCs, diagnostic addresses, NRC policy, session/security matrix or timing values.

## 2. Lifecycle decomposition

The canonical lifecycle is:

```text
DIA-D0  Project diagnostic/tool/network baseline
DIA-D1  Diagnostic requirement decomposition
DIA-D2  CANdela diagnostic specification authoring
DIA-D3  Diagnostic responsibility allocation
DIA-D4  Application SWC contract engineering
DIA-D5  Application SWC behavior + AUTOSAR mapping
DIA-D6  MIL / production-intent generation / SIL
DIA-D7  Diagnostic BSW and UDS-on-CAN integration
DIA-D8  Integrated ECU build/reconciliation
DIA-D9  Lv3 VECU construction
DIA-D10 CANoe runtime integration
DIA-D11 CANoe.DiVa test design/generation
DIA-D12 CANoe/DiVa execution and end-to-end evidence reconciliation
```

The phases are engineering ownership boundaries, not claims that each phase maps to one GUI dialog or one AUTOSAR module.

## 3. Diagnostic specification ownership — CANdela Studio

CANdela Studio owns the project diagnostic specification model in this methodology.

Typical specification identities include:

- Variant/ECU diagnostic description;
- diagnostic services and service parameters;
- DID definitions and data semantics;
- RoutineControl definitions;
- DTC/fault-memory related diagnostic description;
- diagnostic sessions and security/access-related specification;
- request/response data structure and expected diagnostic semantics.

Native CANdela template/document identities are distinct:

```text
CDDT template != CDD document != Variant != Service/Data Object/DTC objects
```

CANdela diagnostic specification does **not** own:

- Application SWC implementation logic;
- DCM service runtime implementation;
- DEM event/DTC memory runtime implementation;
- PduR/CanTp/CanIf/Can transport implementation;
- generated Application SWC C code;
- VECU packaging;
- DiVa test result or CANoe runtime verdict.

## 4. CANdela interchange boundary

CDD is a native CANdela diagnostic description and is a reviewed input format for downstream Vector diagnostic consumers. ODX export/import is also a reviewed bounded interchange route.

However:

```text
CANdela CDD/ODX export
  != lossless CANdela round-trip
  != proof that one export subset is the universal DiVa producer contract
  != AUTOSAR ECU configuration
```

The exact project handoff format (CDD, PDX/ODX or another reviewed supported route) must be project-baselined.

## 5. Diagnostic responsibility decomposition

Every diagnostic requirement shall be allocated before implementation. At minimum classify each requirement into one or more of the following ownership domains.

### 5.1 Diagnostic specification domain

Owned by CANdela/project diagnostic design:

- service availability and externally visible service semantics;
- DID/RID/DTC description identities;
- session/security/access preconditions;
- request/response parameter semantics;
- externally visible negative/positive behavior expected by project specification.

### 5.2 Application SWC domain

Owned by Application SWC contract/behavior where the diagnostic service needs application behavior:

- provide/read application data for a DID;
- execute project-specific RoutineControl behavior;
- apply application state/permission checks;
- accept/produce application-side diagnostic operation results;
- report project monitor/fault information through the defined AUTOSAR/application interface;
- coordinate application-specific diagnostic/fault policy that is not DCM/DEM-owned.

### 5.3 DCM domain

DCM owns ECU-local diagnostic communication/service processing in the AUTOSAR Classic layer, including the reviewed service/session/security/request-response responsibilities. DCM receives/transmits diagnostic payloads through PduR and consumes other BSW/application services where configured.

Do not move DCM responsibilities into the Application SWC merely because the service ultimately calls application logic.

### 5.4 DEM domain

DEM owns diagnostic-event status processing, DTC/UDS status derivation, event/fault-memory management and DTC-related services/data used by DCM and other clients.

```text
Application monitor result -> DEM event/status processing
DCM DTC service -> DEM data/service access
```

This does not make DCM the owner of fault memory and does not make DEM the owner of tester-facing request dispatch.

### 5.5 UDS-on-CAN transport domain

The configured CAN diagnostic transport branch is separated from service semantics:

```text
DCM
  <-> PduR network-independent boundary
       <-> configured CanTp CAN transport branch
            <-> CanIf
                 <-> Can Driver / CAN controller
```

This is an ownership/navigation view, not one universal runtime call sequence. PduR routes, CanTp performs CAN transport segmentation/reassembly/flow control where configured, CanIf owns CAN-hardware-independent integration, and CanDrv owns CAN controller hardware access.

## 6. Application SWC contract — DaVinci Developer Classic

DaVinci Developer Classic remains the canonical owner for AUTOSAR Application SWC software-design contract objects.

For diagnostic-facing Application SWCs this includes, as applicable:

- SWC/component identity;
- P/R ports and service/data interfaces;
- client/server operations or sender/receiver data paths;
- RunnableEntity and RTEEvent identities;
- application/implementation datatype relations;
- RTE access points;
- PIM/calibration identities where required.

The contract is exported as a controlled AUTOSAR SWC description for the MathWorks implementation flow.

Do not independently re-author the same contract in Simulink.

## 7. Application behavior — AUTOSAR Blockset + Simulink/Stateflow

AUTOSAR Blockset imports/represents the AUTOSAR SWC contract and manages the model-to-AUTOSAR mapping layer. Simulink/Stateflow owns the executable application behavior model.

Typical diagnostic application behavior includes:

- read/prepare DID application data;
- execute RoutineControl application function;
- enforce application-specific state/precondition logic;
- map application outcomes to the contract result expected by the integration layer;
- monitor/report application faults according to project requirements.

Important:

```text
Application result != actual UDS response encoding by DCM
Application fault policy != DEM event-memory semantics
Stateflow behavior != generated implementation
```

## 8. Diagnostic application callbacks and service integration

The project must explicitly define how configured DCM diagnostic operations reach Application SWC behavior. This may involve AUTOSAR RTE/client-server/data access or configured diagnostic interfaces supported by the project/toolchain.

The methodology does not invent callback names, operation signatures or generated API names before the project diagnostic extract/ARXML/tool configuration is available.

A required review item is always:

```text
CANdela externally visible diagnostic element
  <-> DCM/DEM configuration identity
  <-> Application SWC operation/data/event identity where applicable
```

## 9. Diagnostic BSW configuration — DaVinci Configurator Classic / MICROSAR

Configurator/MICROSAR owns production ECU configuration/generation for the diagnostic BSW and communication path.

Configuration scope can include:

- DCM service/session/security/configuration objects;
- DEM events/DTCs/event memory and DCM-facing DEM relations;
- RTE/application operation/data integration required by diagnostics;
- PduR diagnostic routing;
- CanTp channels/connections/addressing/timing according to the project UDS-on-CAN network design;
- CanIf/CAN lower communication configuration;
- required OS/task/runtime integration;
- production RTE/BSW source generation.

CANdela data is a diagnostic specification input. It is not itself production ECU-C/BSW configuration.

The existing Reviewed Knowledge does not establish one universal direct CANdela -> Configurator automatic synchronization contract. Any project import/generation route must be explicitly verified before use.

## 10. DCM/DEM non-collapse rules

### 10.1 DCM

Owns service/session/security/request-response processing and the PduR diagnostic payload boundary.

### 10.2 DEM

Owns event/DTC/status/fault-memory semantics and operations.

### 10.3 Application SWC

Owns project application data/function behavior and project fault-monitor/application policy allocated to it.

Therefore:

```text
DID read callback behavior != DCM service ownership
Routine implementation != RoutineControl protocol ownership
monitor result != DEM event memory
DTC service 0x19/0x14 processing in DCM != DEM data ownership
```

## 11. UDS-on-CAN network baseline

Before production diagnostic integration the project shall fix at least:

- CAN/CAN FD use for this route;
- request/response CAN identifiers or addressing objects;
- physical/functional addressing policy;
- CanTp addressing format and connection identities;
- configured UDS/CanTp timing values;
- PduR routing identities;
- applicable CAN network/controller/channel identity.

Values are `PROJECT_INPUT_REQUIRED`; AUTOSAR/Vector authority explains module roles but does not supply Management ECU values.

## 12. Model-level verification

Application diagnostic behavior shall be tested before production BSW/VECU testing.

MIL evidence can cover:

- DID data behavior;
- Routine application behavior;
- application preconditions/state transitions;
- monitor/fault reporting behavior;
- boundary/error cases at the Application SWC contract.

MIL does not prove DCM/DEM/CanTp integration.

## 13. Production-intent generation and SIL

Embedded Coder generates production-intent Application SWC implementation artifacts from the mapped model.

Keep identities separate:

```text
Simulink/Stateflow source model
!= generated C/H
!= implementation ARXML
!= compiled/linked ECU software
!= production RTE/BSW
```

SIL verifies generated implementation separately from MIL. SIL remains distinct from integrated VECU diagnostic behavior.

## 14. ECU integration and reconciliation

Before VECU construction, reconcile:

- CANdela diagnostic specification revision;
- DaVinci SWC contract revision;
- MathWorks model/mapping/generated artifacts;
- Configurator/MICROSAR DCM/DEM/communication configuration;
- diagnostic/application callback mapping;
- network/CanTp configuration;
- build/generation provenance.

No one artifact is treated as a substitute for all others.

## 15. Lv3 VECU construction — vVIRTUALtarget

vVIRTUALtarget is used after integrated ECU software/configuration is available. It owns the reviewed VECU build/package/execution role, not diagnostic specification authoring.

The VECU package must preserve its input provenance and distinguish virtual execution from MIL/SIL and physical ECU/HIL evidence.

## 16. CANoe diagnostic runtime integration

CANoe consumes the virtual ECU/runtime and diagnostic description/environment required for diagnostic communication and test execution.

The reviewed Vector route supports diagnostic description consumption and named DiVa integration surfaces.

CANoe runtime configuration is not the CANdela authoring source and is not the production ECU BSW configuration source.

## 17. CANoe.DiVa test design/generation

DiVa consumes supported diagnostic specification data plus ECU/Variant/environment resources and generates diagnostic test specifications/modules/units.

Generation can cover reviewed categories such as:

- service coverage;
- timing/format/content/plausibility;
- session/security behavior;
- valid/invalid requests;
- parameter validation;
- DTC stimulation/expectation;
- system conditions.

The exact generated cases depend on the diagnostic specification and project configuration.

## 18. DiVa -> CANoe execution

The named reviewed route includes DiVa project import into CANoe, bus/environment association, diagnostic configuration/qualifier alignment, selection of generated Test Module/Test Unit and execution/report access.

Keep separate:

```text
DiVa project/configuration
!= generated test specification
!= Test Module/Test Unit
!= CANoe execution state
!= test result/report
```

## 19. End-to-end diagnostic traceability

The desired trace chain is:

```text
Project diagnostic requirement
  -> CANdela diagnostic specification object
  -> DCM/DEM/transport configuration object(s)
  -> Application SWC contract/behavior object where applicable
  -> generated/integrated ECU artifact
  -> VECU build
  -> DiVa generated test intent
  -> CANoe execution result
```

Not every requirement necessarily passes through every node. For example, a pure DCM/DEM service may not require Application SWC behavior.

## 20. Change routing

### Diagnostic specification change

Start at CANdela/project diagnostic design, then perform impact analysis on BSW configuration, Application SWC contract/behavior and DiVa tests.

### Application-only behavior change

Start at Simulink/Stateflow, then repeat applicable MIL -> generation -> SIL -> integration/VECU regression without silently changing the CANdela specification.

### SWC interface/callback change

Start at DaVinci Developer contract governance, then re-export/re-import/update the model and Configurator integration.

### DCM/DEM/transport configuration change

Start at Configurator/MICROSAR/project integration governance; determine whether externally visible diagnostic behavior requires CANdela and DiVa regeneration.

### Diagnostic test policy change only

Start in DiVa/test engineering without rewriting the ECU diagnostic specification unless the change is actually a specification change.

## 21. Tool/version baseline

Reviewed evidence baselines currently include:

- CANdela Studio 25 SP1;
- CANoe.DiVa 20;
- CANoe 20.2.1;
- DaVinci Developer Classic 4.18 SP3 family;
- DaVinci Configurator Classic 6.3.10;
- vVIRTUALtarget 10 family;
- MathWorks R2025b Reviewed Knowledge;
- AUTOSAR Classic Platform 4.4.0 direct authority.

Actual project releases remain separate project inputs. Do not substitute reviewed evidence baselines for actual project compatibility decisions.

## 22. Definition of Done for methodology use

Before calling the diagnostic toolchain definition usable for a project:

- diagnostic requirement ownership is explicit;
- CANdela source diagnostic specification is version-fixed;
- Application SWC involvement is identified rather than assumed;
- DCM/DEM ownership is separated;
- UDS-on-CAN transport configuration is explicit;
- project tool/schema versions are fixed;
- Application SWC contract/behavior and diagnostic BSW relations are traceable;
- VECU input/build provenance is fixed;
- DiVa input specification/configuration is fixed;
- CANoe execution results are traceable to the generated test definition and diagnostic specification;
- all remaining procedure/detail gaps are explicit.

## 23. Canonical principle

For every diagnostic engineering task, first ask:

> Is this externally visible diagnostic specification, application behavior, diagnostic service processing, event/fault-memory processing, transport realization, virtual ECU realization, or test/evidence?

Only after that ownership decision should a tool be selected.