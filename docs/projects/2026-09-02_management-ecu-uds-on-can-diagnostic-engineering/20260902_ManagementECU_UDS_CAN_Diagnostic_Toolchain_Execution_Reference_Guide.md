# Management ECU — UDS on CAN Diagnostic Toolchain Execution & Reference Guide

**Date:** 2026-09-02  
**Task-navigation companion:** `20260902_ManagementECU_UDS_CAN_Diagnostic_Tool_Task_Reference_Matrix.yaml`  
**Procedure-maturity companion:** `procedures/procedure-coverage-matrix.yaml`

## 1. Purpose

Start from what you want to do, then resolve:

```text
engineering intent
 -> lifecycle phase
 -> primary tool
 -> required project input
 -> exact Reviewed Knowledge locator
 -> supported operation
 -> procedure maturity
 -> output artifact/state
 -> exit condition
 -> next task
```

This Guide does not invent Management ECU diagnostic content.

## 2. Start here by intent

| Intent | Task | Primary tool |
|---|---|---|
| Fix project tool/schema baseline | DTR-000 | Project CM |
| Allocate diagnostic ownership | DTR-001 | Engineering review |
| Author UDS diagnostic specification | DTR-002 | CANdela Studio |
| Export/fix diagnostic-description handoff | DTR-003 | CANdela Studio |
| Define diagnostic Application SWC contract | DTR-004 | DaVinci Developer Classic |
| Import SWC ARXML into MathWorks model | DTR-005 | AUTOSAR Blockset |
| Implement DID/Routine/application diagnostic behavior | DTR-006 | Simulink / Stateflow |
| Review AUTOSAR mapping | DTR-007 | AUTOSAR Blockset |
| Verify application behavior at MIL | DTR-008 | Simulink / test environment |
| Generate C/H/implementation ARXML | DTR-009 | Embedded Coder |
| Verify generated implementation at SIL | DTR-010 | MathWorks SIL |
| Configure DCM/DEM | DTR-011 | DaVinci Configurator / MICROSAR |
| Integrate DCM/DEM with Application SWC/RTE | DTR-012 | Configurator / MICROSAR |
| Configure UDS-on-CAN transport | DTR-013 | Configurator / MICROSAR |
| Reconcile/build integrated ECU software | DTR-014 | Configurator / project build |
| Build Lv3 VECU | DTR-015 | vVIRTUALtarget |
| Integrate VECU + diagnostics in CANoe | DTR-016 | CANoe |
| Create DiVa project | DTR-017 | CANoe.DiVa |
| Generate diagnostic tests | DTR-018 | CANoe.DiVa |
| Execute generated tests against VECU | DTR-019 | CANoe + DiVa |
| End-to-end trace closure | DTR-020 | Engineering review |

For `DTR-002` through `DTR-019`, resolve the accepted procedure classification and tool-family file through `procedures/procedure-coverage-matrix.yaml` before executing the task.

## 3. Whole toolchain

```text
Project Diagnostic Requirements
        |
        v
CANdela Studio
  diagnostic specification
        |
        +------------------------------+
        |                              |
        v                              v
Application involvement?          BSW/test realization
        |                              |
        v                              |
DaVinci Developer                    |
  SWC contract ARXML                  |
        |                              |
        v                              |
AUTOSAR Blockset                      |
        v                              |
Simulink / Stateflow                  |
        v                              |
MIL -> Embedded Coder -> SIL          |
        |                              |
        +-------------+----------------+
                      v
          DaVinci Configurator / MICROSAR
          DCM + DEM + RTE + PduR/CanTp/CanIf/Can
                      |
                      v
              Integrated ECU software
                      |
                      v
                vVIRTUALtarget
                      |
                      v
                  Lv3 VECU
                      |
                      v
                    CANoe
                      ^
                      |
CANdela description -> CANoe.DiVa -> generated tests
                      |
                      +-> CANoe execution/results
```

The arrows are engineering handoffs. They do not claim automatic synchronization between every tool.

## 4. CANdela Studio — when to use it

Use CANdela for the externally visible diagnostic specification.

Read first:

- `V-DIAG-001` diagnostic authoring model;
- `V-DIAG-002` CDD/CDDT identity;
- `V-DIAG-003` when ODX exchange is considered;
- `V-DIAG-004` when DiVa is the consumer.

Typical work objects:

```text
Template / Document / Variant
Diagnostic Classes / Instances / Services
Data Types / Data Objects
DID
DTC / fault-memory description
session/security-related diagnostic description
```

Do not turn CANdela into the owner of DCM/DEM runtime semantics.

Procedure maturity:

- `DTR-002`: `WORKFLOW_ONLY` — object/lifecycle model is reviewed, exact authoring menu sequence is not.
- `DTR-003`: `PARTIAL_PROCEDURE_AVAILABLE` — ODX versions and complete/DTC-only/selected-element export modes are reviewed; exact full GUI workflow and a mandatory DiVa export subset are not.

Use `procedures/candela-studio.yaml` for the compiled operation boundary.

## 5. CANdela handoff — important boundary

The reviewed corpus supports real CDD/ODX diagnostic-description consumer routes, including DiVa and CANoe.

But it does **not** establish:

```text
one mandatory CANdela 25 SP1 export subset
    == universal DiVa 20 producer contract
```

and it does not establish one universal CANdela -> Configurator 6.3.10 automatic synchronization contract.

Therefore the project must fix the actual handoff and then reconcile specification-to-implementation identities.

## 6. Decide whether an Application SWC is involved

Before opening Developer/Simulink, ask whether the diagnostic element requires application behavior.

Examples that may require application involvement:

- read/prepare an application DID value;
- execute a project-specific routine;
- evaluate an application operating-state condition;
- report an application monitor/fault state.

Examples that remain BSW-owned at protocol/event-memory level:

- DCM service/session/security/request-response processing;
- DEM event/DTC/status/fault-memory management;
- CanTp segmentation/reassembly;
- lower CAN routing/hardware abstraction.

## 7. DaVinci Developer Classic — Application SWC contract

Task: `DTR-004`.

Read:

- `V-DIAG-010`, `V-DIAG-011`;
- `AS-DIAG-007`, `AS-DIAG-008`;
- `DS-DIAG-004`.

Own here:

```text
SWC identity
P/R ports / service or data interfaces
operations/data types
RunnableEntity / RTEEvent contract
RTE-access-facing objects
PIM/calibration identities where applicable
```

Then export a controlled SWC ARXML description.

Compiled maturity: `PARTIAL_PROCEDURE_AVAILABLE`. AUTOSAR XML import/export and selected component-type software-component-description export are reviewed, but exact object-creation/edit/export clicks are not. See `procedures/davinci-developer-classic.yaml`.

## 8. AUTOSAR Blockset / Simulink / Stateflow

### Import/model scaffold — DTR-005

Read `MW-DIAG-001`, `MW-DIAG-002`.

```text
SWC ARXML
 -> import/create/update
 -> Simulink AUTOSAR representation
```

The two artifacts are not identical.

Compiled maturity: `PARTIAL_PROCEDURE_AVAILABLE`. Frozen R2025b authority explicitly names:

```text
arxml.importer
createComponentAsModel
updateModel
updateAUTOSARProperties
```

Use `procedures/autosar-blockset.yaml`. The explicit API names do not by themselves make the whole project import/update procedure exact; schema/profile, arguments and post-import repair remain project/context dependent.

### Behavior — DTR-006

Use Simulink/Stateflow for application diagnostic behavior only.

```text
Application result != UDS response encoding by DCM
Application monitor result != DEM event memory
Stateflow source != generated implementation
```

Compiled maturity: `WORKFLOW_ONLY`. Use `procedures/simulink-stateflow.yaml`.

### Mapping — DTR-007

Review the model-to-AUTOSAR associations needed by the fixed Application SWC contract.

Named reviewed surfaces include Code Mappings, AUTOSAR Dictionary and AUTOSAR Component Designer. The task remains `WORKFLOW_ONLY` because the project-specific mapping operation sequence is not compiled. See `procedures/autosar-blockset.yaml`.

## 9. MIL / Embedded Coder / SIL

### MIL — DTR-008

Tests Application SWC behavior before production BSW/VECU integration.

Read `MW-DIAG-006..010` as applicable.

Compiled maturity: `PARTIAL_PROCEDURE_AVAILABLE`. Test Manager/TestFile/TestSuite/TestCase, harness identity and Normal/model execution are reviewed. `MIL` remains workflow terminology rather than a separate Simulink simulation-mode value. See `procedures/mil-sil.yaml`.

### Code generation — DTR-009

Generate and version C/H, implementation ARXML and reports.

```text
code generation != compile != link
MathWorks local RTE stub != production MICROSAR RTE
```

Compiled maturity: `PARTIAL_PROCEDURE_AVAILABLE`. `Generate code only`, `codebuild`, and `coder.report.generate` are source-explicit, but project configuration remains separate. See `procedures/embedded-coder.yaml`.

### SIL — DTR-010

Execute generated implementation separately from MIL.

```text
MIL PASS != SIL PASS != VECU diagnostic PASS
```

Compiled maturity: `PARTIAL_PROCEDURE_AVAILABLE`. Software-in-the-loop execution identity is explicit, but project-specific SIL configuration/launch remains partial. See `procedures/mil-sil.yaml`.

## 10. DCM — service/session/security owner

Read `AS-DIAG-001`.

AUTOSAR authority places ECU-local diagnostic service/message processing in DCM and identifies PduR as the network-independent diagnostic payload boundary.

DCM includes specification concepts for request/response flow, session/security state and service/subservice processing. These do not make DSL/DSD/DSP separate BSW modules.

Do not put DCM service ownership into the Application SWC.

## 11. DEM — event/DTC/fault-memory owner

Read `AS-DIAG-002`, `AS-DIAG-003`.

```text
Application monitor -> DEM event/status processing
DCM DTC service -> DEM query/clear/data services
```

DEM retains event/DTC/fault-memory ownership. DCM remains the tester-facing service processor.

## 12. Configurator / MICROSAR — production diagnostic BSW

Tasks: `DTR-011`, `DTR-012`, and `DTR-014`.

Read:

- `V-DIAG-012`, `V-DIAG-013`;
- `AS-DIAG-001..003`;
- `AS-DIAG-009`.

Configure the project-specific DCM/DEM/RTE/Application relations under actual MICROSAR/project versions.

Do not use the legacy Configurator diagnostic import statement as proof of a current direct CANdela integration contract.

Compiled maturity:

- `DTR-011`: `WORKFLOW_ONLY` — DCM/DEM ownership is strong, exact Configurator 6.3.10 object sequence is not compiled.
- `DTR-012`: `WORKFLOW_ONLY` — production RTE/application integration ownership is known, exact callback/data/event mapping sequence is not.
- `DTR-014`: `PARTIAL_PROCEDURE_AVAILABLE` — `dvcfg-b project generate` is an explicit reviewed generation route; full reconciliation/build remains project-specific.

Use `procedures/davinci-configurator-microsar.yaml` and, for ownership-layer detail, `procedures/diagnostic-bsw-uds-on-can.yaml`.

## 13. UDS on CAN transport

Task: `DTR-013`.

Read:

- `AS-DIAG-004` diagnostic transport branches;
- `AS-DIAG-005` CanTp path;
- `AS-DIAG-006` CAN hardware abstraction;
- `DS-PROJ-DIAG-003` actual network inputs.

Ownership view:

```text
DCM
  <-> PduR
       <-> CanTp   [configured CAN TP branch]
            <-> CanIf
                 <-> CanDrv/controller
```

Do not read this as a universal API sequence.

Compiled maturity: **`PROJECT_INPUT_REQUIRED`**. The authority closes the ownership structure, but execution cannot be instantiated until project CAN IDs/addressing, CanTp connections/timing, PduR routes, lower CAN identities and P2/P2* are accepted. See `procedures/diagnostic-bsw-uds-on-can.yaml`.

## 14. Integrated ECU reconciliation

Task: `DTR-014`.

Compare/trace at least:

```text
CANdela object/revision
DCM configuration identity
DEM event/DTC identity
Application SWC operation/data/runnable identity where applicable
PduR/CanTp/network identity
MathWorks generated application artifacts
production RTE/BSW generation/build baseline
```

Matching names alone are not semantic proof.

The explicit `dvcfg-b project generate` operation belongs only after the intended configuration is reconciled/validated; it is not proof that the specification-to-configuration reconciliation itself is automatic.

## 15. vVIRTUALtarget

Task: `DTR-015`.

Read `V-DIAG-014`, `V-DIAG-015`.

Use the applicable reviewed Integration route for the actual DaVinci/MICROSAR artifact set. Do not flatten Integration and BSW Emulation into one generic vECU recipe.

Output is a versioned virtual ECU/SUT artifact, not a MIL/SIL result.

Compiled maturity: `PARTIAL_PROCEDURE_AVAILABLE`. VttMake/update/build/package and DPA/DVJSON/VTTJSON routes are explicit, while the complete selected-project artifact/version recipe remains partial. See `procedures/vvirtualtarget.yaml`.

## 16. CANoe diagnostic runtime

Task: `DTR-016`.

Read `V-DIAG-008`, `V-DIAG-015`.

Bring together:

- virtual SUT/VECU;
- diagnostic description;
- Diagnostics/ISO TP context;
- network/bus/node/qualifier/variant context.

CANoe is the runtime/integration/test consumer; it is not the diagnostic specification authoring source.

Compiled maturity: `PARTIAL_PROCEDURE_AVAILABLE`. Reviewed named surfaces include Communication Setup `Add VTT model` and Diagnostics/ISO TP Configuration. Full load/reload/version compatibility remains partial. See `procedures/canoe-diva.yaml`.

## 17. CANoe.DiVa test engineering

### Create project — DTR-017

Read `V-DIAG-004`, `V-DIAG-005`.

Inputs include supported diagnostic specification data, ECU/Variant context, CANoe Environment and project resources.

Compiled maturity: `PARTIAL_PROCEDURE_AVAILABLE`. Project Configuration, ECU Information, CANoe Environment and Additional Resources are reviewed named surfaces.

### Generate tests — DTR-018

Reviewed DiVa generation covers categories including service coverage, timing/format/content/plausibility, sessions/security, valid/invalid requests, parameter validation, DTC-related tests and system conditions.

Generation result is not execution evidence.

Compiled maturity: `PARTIAL_PROCEDURE_AVAILABLE`. The reviewed CLI entry point is:

```text
diva-make.exe diva.yaml [options]
```

This does not fix the project-specific option profile or generated-case selection. See `procedures/canoe-diva.yaml`.

## 18. DiVa -> CANoe execution — exact bounded procedure slice

Task: `DTR-019`.

Read `V-DIAG-006`, `V-DIAG-007`, `V-DIAG-009`.

This is the one task currently classified **`EXACT_PROCEDURE_AVAILABLE`** at the reviewed bounded scope. Two-sided Vector authority supports the following named sequence:

```text
Diagnostics & XCP | Test | Import DiVa Project
  -> Assigned Bus
  -> Diagnostics/ISO TP configuration
  -> ECU Qualifier matching
  -> Test Module/Test Unit selection
  -> if a DiVa Test Unit changed: re-import so CANoe recompiles it
  -> measurement / test execution
  -> report access
```

Project values such as the actual bus, qualifier, variant, addressing and selected test set still come from project configuration; `EXACT_PROCEDURE_AVAILABLE` does not mean those inputs are inferred.

Preserve:

```text
DiVa project
!= generated test specification
!= Test Module/Test Unit
!= CANoe execution state
!= result/report
```

Use `procedures/canoe-diva.yaml` for the compiled bounded procedure.

## 19. End-to-end closure

Task: `DTR-020`.

The desired trace is:

```text
Diagnostic requirement
 -> CANdela specification object
 -> implementation ownership
      -> DCM
      -> DEM
      -> Application SWC where applicable
      -> PduR/CanTp/CAN configuration
 -> integrated ECU software
 -> VECU
 -> DiVa generated test
 -> CANoe execution result
```

Not every requirement traverses every node. A trace link must reflect actual ownership, not a forced template.

## 20. Accepted procedure maturity

Procedure compilation source: Luna Ending SHA `3b5f2cdfc418e46cd2ad4a8509fc77ac50eacc12`, fixed-head reviewed and accepted by Sol.

| Task | Maturity | Strongest reviewed surface |
|---|---|---|
| DTR-002 | `WORKFLOW_ONLY` | CANdela CDDT/CDD/Variant/service/data/DID/DTC object model |
| DTR-003 | `PARTIAL_PROCEDURE_AVAILABLE` | ODX supported versions + complete/DTC-only/selected-element export scope |
| DTR-004 | `PARTIAL_PROCEDURE_AVAILABLE` | Developer AUTOSAR XML / selected SWC-description export |
| DTR-005 | `PARTIAL_PROCEDURE_AVAILABLE` | `arxml.importer`, `createComponentAsModel`, `updateModel`, `updateAUTOSARProperties` |
| DTR-006 | `WORKFLOW_ONLY` | Simulink/Stateflow diagnostic application behavior boundary |
| DTR-007 | `WORKFLOW_ONLY` | Code Mappings / AUTOSAR Dictionary / Component Designer |
| DTR-008 | `PARTIAL_PROCEDURE_AVAILABLE` | Test Manager hierarchy + Normal/model execution |
| DTR-009 | `PARTIAL_PROCEDURE_AVAILABLE` | Generate code only / `codebuild` / code-generation report |
| DTR-010 | `PARTIAL_PROCEDURE_AVAILABLE` | SIL execution / equivalence-test workflow |
| DTR-011 | `WORKFLOW_ONLY` | Configurator BSW role + AUTOSAR DCM/DEM ownership |
| DTR-012 | `WORKFLOW_ONLY` | production diagnostic Application/RTE integration ownership |
| DTR-013 | `PROJECT_INPUT_REQUIRED` | AUTOSAR ownership path known; Management ECU network values TBD |
| DTR-014 | `PARTIAL_PROCEDURE_AVAILABLE` | `dvcfg-b project generate` + project build boundary |
| DTR-015 | `PARTIAL_PROCEDURE_AVAILABLE` | vVIRTUALtarget Integration + VttMake/update/build/package |
| DTR-016 | `PARTIAL_PROCEDURE_AVAILABLE` | CANoe `Add VTT model` + Diagnostics/ISO TP Configuration |
| DTR-017 | `PARTIAL_PROCEDURE_AVAILABLE` | DiVa Project Configuration / ECU Information / CANoe Environment / Additional Resources |
| DTR-018 | `PARTIAL_PROCEDURE_AVAILABLE` | `diva-make.exe diva.yaml [options]` |
| DTR-019 | `EXACT_PROCEDURE_AVAILABLE` | named DiVa→CANoe import/bind/execute/report sequence |

Counts:

```text
EXACT_PROCEDURE_AVAILABLE    1
PARTIAL_PROCEDURE_AVAILABLE 11
WORKFLOW_ONLY                5
NO_EXPLICIT_PROCEDURE        0
PROJECT_INPUT_REQUIRED       1
UNRESOLVED_AUTHORITY         0
```

Use `procedures/procedure-coverage-matrix.yaml` as the machine-readable maturity overlay. The original Tool/Task Matrix retains lifecycle/ownership navigation and is not reinterpreted by these maturity labels.

## 21. Highest-value remaining procedure gaps

The largest gap is **Configurator/MICROSAR diagnostic realization** rather than diagnostic ownership knowledge.

Priority gaps are:

1. exact Configurator 6.3.10 DCM/DEM object configuration sequence;
2. exact diagnostic Application SWC/RTE callback/data/event mapping sequence;
3. exact PduR/CanTp/CanIf/Can configuration sequence after Management ECU network inputs are supplied;
4. exact CANdela 25 SP1 object-authoring GUI sequence;
5. exact Developer 4.18 SP3 diagnostic-facing SWC authoring sequence;
6. complete selected vVIRTUALtarget Integration artifact/version recipe;
7. complete CANoe/VTT load/reload/version procedure;
8. complete DiVa project/generation option/profile and version matrix.

These are **procedure-authority gaps**, not capability-negative conclusions.

## 22. Stop rule

When a project-specific value is missing, stop at `PROJECT_INPUT_REQUIRED` rather than filling it from vendor, AUTOSAR or generic UDS knowledge.

When a GUI/API/CLI operation is not in exact-pinned Reviewed Knowledge, stop at the accepted procedure maturity instead of inventing a click sequence, command, callback name or project configuration object.
