# Management ECU — UDS on CAN Diagnostic Development Step-by-Step Guide

**Date:** 2026-09-02  
**Scope:** CANdela specification -> Application SWC / AUTOSAR diagnostic BSW -> Lv3 VECU -> CANoe.DiVa/CANoe verification

Each step is read as:

```text
Input -> read first -> primary tool -> action -> output -> completion criteria -> next step
```

Exact GUI/API procedure is not inferred unless later procedure compilation confirms it.

## Step 0 — Fix project baselines

**Input:** project tool/network constraints.  
**Primary control:** project configuration management.

Record:

- actual CANdela, DaVinci, MATLAB/Simulink, Configurator/MICROSAR, vVIRTUALtarget, CANoe/DiVa releases;
- AUTOSAR schema/release used by the project;
- UDS-on-CAN network/addressing baseline;
- diagnostic requirement baseline.

**Output:** `references/project/*.yaml`.  
**Complete when:** actual releases/network inputs are explicit or intentionally marked `TBD_PROJECT_DECISION`.

## Step 1 — Allocate diagnostic requirements

For each requirement determine whether it belongs to:

- diagnostic specification;
- Application SWC;
- DCM;
- DEM;
- UDS-on-CAN transport;
- VECU/runtime integration;
- diagnostic test policy.

Do not assume every UDS service requires an Application SWC callback.

**Output:** requirement/responsibility allocation.  
**Complete when:** no requirement is unintentionally unowned and cross-layer dependencies are explicit.

## Step 2 — Author the diagnostic specification in CANdela Studio

Define the externally visible diagnostic model required by the accepted project requirements, including applicable service/data/DID/Routine/DTC/session/security structures.

Read the CANdela authoring and specialization locators first.

Do not encode DCM/DEM implementation detail merely to make the specification resemble the BSW configuration.

**Output:** controlled CANdela diagnostic document/specification revision.  
**Complete when:** externally visible diagnostic semantics needed by the project are reviewable and versioned.

## Step 3 — Fix the diagnostic-description handoff

Select the project-approved downstream description route supported by the toolchain, for example native CDD consumer use or a bounded ODX/PDX route where applicable.

Record:

- source CANdela revision;
- format/profile/version;
- export selection/scope;
- known information-loss or unsupported-content warnings.

Do not claim lossless round-trip identity.

**Output:** controlled diagnostic description handoff artifact.  
**Complete when:** downstream consumer and exact input revision/profile are traceable.

## Step 4 — Define the Application SWC diagnostic contract

**Primary tool:** DaVinci Developer Classic.

Only for diagnostic requirements that need application behavior, define/confirm:

- SWC identity;
- ports/interfaces;
- client/server operation or sender/receiver data contract;
- runnables/events;
- datatypes;
- RTE-access/PIM/calibration identities as applicable.

**Output:** AUTOSAR SWC contract ARXML.  
**Complete when:** application-facing diagnostic contract is fixed without absorbing DCM/DEM ownership.

## Step 5 — Import the contract into the MathWorks AUTOSAR model

**Primary tool:** AUTOSAR Blockset; supporting tool: Simulink.

Import/create/update the Simulink AUTOSAR representation from the controlled SWC ARXML and inspect component/port/interface/runnable/mapping identity.

**Output:** traceable Simulink AUTOSAR component model scaffold.  
**Complete when:** the model representation is tied to a specific contract ARXML revision and differences are recorded.

## Step 6 — Implement Application SWC diagnostic behavior

**Primary tools:** Simulink / Stateflow.

Implement only project-allocated application behavior such as:

- DID application-data preparation;
- Routine application function;
- application state/precondition behavior;
- application fault/monitor behavior;
- application-specific result generation.

Do not implement DCM session/security/service dispatch or DEM event-memory semantics inside the SWC.

**Output:** diagnostic application behavior model.  
**Complete when:** accepted application requirements are implemented against the fixed contract.

## Step 7 — Review AUTOSAR mapping

**Primary tool:** AUTOSAR Blockset.

Review/model mappings needed for the application diagnostic interface:

- ports/data;
- operations/functions/runnables;
- PIM/calibration where applicable.

**Output:** mapping configuration/review record.  
**Complete when:** no unexplained mapping remains before verification/generation.

## Step 8 — Perform MIL

Verify application behavior independently of production DCM/DEM/CanTp integration.

Cover requirement-relevant nominal, boundary, state/precondition, invalid-input and monitor/fault cases.

Keep test definition, verdict, result and coverage separate.

**Output:** MIL test/result/trace evidence.  
**Complete when:** accepted application diagnostic behavior has explicit model-level evidence.

## Step 9 — Generate production-intent Application SWC implementation

**Primary tool:** Embedded Coder.

Generate and version separately:

- C/H;
- implementation ARXML;
- code-generation report/metadata.

Generation is not compile/link or production RTE generation.

**Output:** generated application implementation package.  
**Complete when:** outputs are traceable to model/mapping/tool/configuration identity.

## Step 10 — Perform SIL

Execute generated implementation in SIL identity and retain a result independent from MIL.

**Output:** SIL evidence and MIL/SIL correspondence.  
**Complete when:** required generated-code behavior has explicit SIL evidence.

## Step 11 — Configure DCM/DEM ownership in production BSW

**Primary tool:** DaVinci Configurator Classic / MICROSAR.

Configure the project diagnostic BSW based on accepted diagnostic and AUTOSAR configuration inputs.

### DCM side

Configure applicable service/session/security/request-response and application integration objects.

### DEM side

Configure applicable event/DTC/status/event-memory relationships and DCM-facing data/service dependencies.

Keep DCM and DEM configuration/ownership distinct.

**Output:** versioned diagnostic BSW configuration.  
**Complete when:** each implemented diagnostic element has an explicit DCM/DEM/application ownership path.

## Step 12 — Configure UDS-on-CAN transport

Configure the UDS CAN transport/routing path according to the accepted project network baseline.

Engineering ownership view:

```text
DCM <-> PduR <-> configured CanTp branch <-> CanIf <-> CanDrv/controller
```

This is not a universal API sequence.

Fix project-specific:

- request/response/addressing identities;
- physical/functional addressing policy;
- CanTp connections/addressing/timing;
- PduR routing;
- CAN channel/controller/network identities.

**Output:** production UDS-on-CAN communication configuration.  
**Complete when:** tester payload can be traced from DCM/PduR through the configured CAN transport path without collapsing service and transport semantics.

## Step 13 — Reconcile specification, Application SWC and BSW

Create a controlled reconciliation record across:

- CANdela diagnostic object;
- DCM service/configuration identity;
- DEM event/DTC identity where applicable;
- Application SWC operation/data/runnable identity where applicable;
- transport/network identity;
- generated application artifacts.

Do not use matching names alone as proof of semantic equivalence.

**Output:** diagnostic implementation reconciliation record.  
**Complete when:** intended differences are explained and unresolved differences are explicit.

## Step 14 — Generate/build integrated ECU software

Validate Configurator/MICROSAR configuration and generate production RTE/BSW artifacts. Compile/link according to project build configuration.

Keep:

```text
MathWorks generated application code != integrated ECU binary/software image
```

**Output:** integrated ECU software/configuration artifact set.  
**Complete when:** build provenance and diagnostic integration inputs are fixed.

## Step 15 — Construct the Lv3 VECU

**Primary tool:** vVIRTUALtarget.

Use the reviewed Configurator/vVIRTUALtarget handoff appropriate to the actual project artifact set. Build/package the virtual ECU and preserve input/output version identity.

**Output:** versioned Lv3 VECU artifact.  
**Complete when:** VECU can be executed and traced to the integrated ECU source/configuration baseline.

## Step 16 — Integrate the VECU and diagnostic description in CANoe

**Primary tool:** CANoe.

Configure the virtual SUT/runtime environment and the diagnostic description/ISO-TP context needed to address the Management ECU diagnostic server.

Validate qualifier/variant/network/transport alignment against the same diagnostic specification/network baseline used for implementation.

**Output:** executable CANoe diagnostic/VECU environment.  
**Complete when:** the VECU is addressable through the intended UDS-on-CAN diagnostic route.

## Step 17 — Create/configure the CANoe.DiVa project

**Primary tool:** CANoe.DiVa.

Use the controlled diagnostic specification plus ECU/Variant/CANoe environment and any required project resources.

Configure the intended test scope rather than assuming all generated diagnostic tests are project-required.

**Output:** DiVa project/configuration.  
**Complete when:** input diagnostic specification revision, ECU/Variant and CANoe environment are fixed.

## Step 18 — Generate diagnostic tests in DiVa

Generate the applicable diagnostic test specification/modules/units from the diagnostic data and DiVa configuration.

Review generated coverage for relevant:

- services;
- sessions/security;
- timing/content/format/plausibility;
- valid/invalid requests;
- parameter checks;
- DTC tests/stimulation where applicable;
- system conditions.

**Output:** generated diagnostic test specification and executable test artifacts.  
**Complete when:** generated coverage is reviewed against the project diagnostic requirement set.

## Step 19 — Import/integrate DiVa tests into CANoe

Use the reviewed DiVa-to-CANoe integration route. Align bus assignment, diagnostics/ISO-TP configuration, ECU qualifier/variant and Test Module/Test Unit selection.

For Test Units, preserve the reviewed re-import/recompile lifecycle where applicable.

**Output:** CANoe test configuration with DiVa artifacts.  
**Complete when:** generated tests are bound to the intended Management ECU diagnostic runtime.

## Step 20 — Execute and collect evidence

Run the intended CANoe/DiVa diagnostic test set against the VECU.

Keep identities separate:

```text
specification != generated test != execution state != result != report
```

**Output:** diagnostic test results/reports and execution provenance.  
**Complete when:** each required diagnostic verification objective has an explicit result tied to the VECU/spec/test baseline.

## Step 21 — End-to-end reconciliation

Review the final trace chain:

```text
requirement
 -> CANdela object
 -> DCM/DEM/application/transport implementation identities
 -> integrated ECU/VECU
 -> DiVa generated test
 -> CANoe execution result
```

Retain gaps rather than manufacturing trace links.

## Definition of Done

The compiled engineering route is project-ready only when:

- tool/release baselines are fixed;
- diagnostic/network project inputs are accepted;
- CANdela specification is controlled;
- DCM/DEM/Application SWC ownership is explicit;
- UDS-on-CAN transport configuration is explicit;
- application MIL/SIL evidence exists where application behavior is involved;
- integrated ECU/VECU provenance is fixed;
- DiVa/CANoe test input/output identities are traceable;
- unresolved procedure details are explicitly classified.