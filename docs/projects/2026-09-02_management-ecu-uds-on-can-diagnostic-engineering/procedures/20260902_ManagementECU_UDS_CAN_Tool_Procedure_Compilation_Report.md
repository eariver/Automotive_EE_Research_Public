# Management ECU UDS on CAN Tool Procedure Compilation Report

Date: 2026-09-02

## 1. Objective and source restriction

This report compiles the strongest operational procedure detail already present in exact-pinned Reviewed Knowledge for `DTR-002` through `DTR-019`.

It does **not** design Management ECU diagnostic content. It does not choose DID/RID/DTC values, service inventory, session/security/NRC policy, P2/P2* timing, CAN identifiers, CanTp addressing, PduR routes, callback names, DEM event IDs, test vectors, or actual project releases.

Technical authority was restricted to the frozen locator-manifest tuples for:

- `eariver/Research_Vector_Documents@7a6821cd3f2ad677ca7069c9b114355e98f16842`;
- `eariver/Research_MathWorks_Documents` at the per-locator exact Phase 3/4/5 pins;
- `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d` / AUTOSAR Classic Platform 4.4.0;
- downstream canonical navigation fixed by the Starting SHA.

No current upstream HEAD, online vendor documentation, raw HELP, raw AUTOSAR PDF, observations, worklogs, or generic domain knowledge was used as technical authority.

## 2. Exact Starting SHA

```text
b911b70f36dd2d8808488b03232af8e2bc6b8cfa
```

Branch:

```text
work/luna-management-ecu-uds-can-tool-procedure-compilation-20260902
```

## 3. Classification summary

| Classification | Count |
|---|---:|
| `EXACT_PROCEDURE_AVAILABLE` | 1 |
| `PARTIAL_PROCEDURE_AVAILABLE` | 11 |
| `WORKFLOW_ONLY` | 5 |
| `NO_EXPLICIT_PROCEDURE` | 0 |
| `PROJECT_INPUT_REQUIRED` | 1 |
| `UNRESOLVED_AUTHORITY` | 0 |
| **Total** | **18** |

The result is deliberately conservative. A named product object or general workflow does not become an exact procedure unless the frozen Reviewed Knowledge provides an explicit reproducible operation or sequence.

## 4. DTR-002 through DTR-019 summary

| Task | Primary tool | Classification | Strongest explicit procedure surface |
|---|---|---|---|
| DTR-002 | CANdela Studio | `WORKFLOW_ONLY` | CDDT Template → CDD Document → Variant → diagnostic classes/services/data/DID/DTC object model |
| DTR-003 | CANdela Studio | `PARTIAL_PROCEDURE_AVAILABLE` | ODX 2.0.1/2.1.0/2.2.0 export; complete/DTC-only/selected-element modes |
| DTR-004 | DaVinci Developer Classic | `PARTIAL_PROCEDURE_AVAILABLE` | AUTOSAR XML import/export; selected component-type SWC-description export |
| DTR-005 | AUTOSAR Blockset | `PARTIAL_PROCEDURE_AVAILABLE` | `arxml.importer`, `createComponentAsModel`, `updateModel`, `updateAUTOSARProperties` |
| DTR-006 | Simulink / Stateflow | `WORKFLOW_ONLY` | State/chart/transition/event behavior and AUTOSAR diagnostic service simulation roles |
| DTR-007 | AUTOSAR Blockset | `WORKFLOW_ONLY` | Code Mappings / AUTOSAR Dictionary / AUTOSAR Component Designer named surfaces |
| DTR-008 | Simulink Test / Simulink | `PARTIAL_PROCEDURE_AVAILABLE` | Test Manager hierarchy, test harness, Normal/model execution, separate result/coverage identities |
| DTR-009 | Embedded Coder | `PARTIAL_PROCEDURE_AVAILABLE` | Generate-code-only boundary; generated C/H/ARXML/report; `codebuild`/report APIs |
| DTR-010 | SIL workflow | `PARTIAL_PROCEDURE_AVAILABLE` | Software-in-the-loop execution mode and equivalence-test workflow |
| DTR-011 | Configurator / MICROSAR | `WORKFLOW_ONLY` | Configurator BSW configuration role + AUTOSAR DCM/DEM ownership |
| DTR-012 | Configurator / MICROSAR | `WORKFLOW_ONLY` | Production RTE/BSW configuration/generation ownership |
| DTR-013 | Configurator / MICROSAR | `PROJECT_INPUT_REQUIRED` | AUTOSAR ownership path DCM↔PduR↔CanTp↔CanIf↔CanDrv; project values remain TBD |
| DTR-014 | Configurator / project build | `PARTIAL_PROCEDURE_AVAILABLE` | `dvcfg-b project generate`; named CI/build routes |
| DTR-015 | vVIRTUALtarget | `PARTIAL_PROCEDURE_AVAILABLE` | Integration use case; VttMake update/build/package; DPA/DVJSON/VTTJSON route |
| DTR-016 | CANoe | `PARTIAL_PROCEDURE_AVAILABLE` | Communication Setup `Add VTT model`; Diagnostics/ISO TP Configuration |
| DTR-017 | CANoe.DiVa | `PARTIAL_PROCEDURE_AVAILABLE` | Project Configuration: ECU Information, CANoe Environment, Additional Resources |
| DTR-018 | CANoe.DiVa | `PARTIAL_PROCEDURE_AVAILABLE` | `diva-make.exe diva.yaml [options]`; generated test specification/Test Module/Test Unit |
| DTR-019 | CANoe + DiVa | `EXACT_PROCEDURE_AVAILABLE` | `Diagnostics & XCP | Test | Import DiVa Project` → Assigned Bus → Diagnostics/ISO TP → ECU Qualifier → Test Module/Test Unit → measurement → report |

## 5. Per-tool findings

### 5.1 CANdela Studio 25 SP1

The frozen CANdela Reviewed Knowledge is strong on **what is authored** and on the native artifact model:

```text
CDDT Template
  != CDD Document
  != Variant
  != Diagnostic Class / Instance / Service / Data Object / DID / DTC object
```

ODX export is operationally stronger than the authoring workflow because the reviewed source explicitly identifies supported ODX versions and the complete / DTC-only / selected-element export modes.

However, the corpus does not contain an exact menu/dialog sequence for creating each diagnostic object. It also does not establish one mandatory CANdela 25 SP1 export subset as the formal DiVa 20 producer contract.

Result:

- DTR-002: `WORKFLOW_ONLY`;
- DTR-003: `PARTIAL_PROCEDURE_AVAILABLE`.

### 5.2 DaVinci Developer Classic 4.18 SP3 family

Developer Reviewed Knowledge closes the software-design model and the SWC-description handoff:

- component types;
- ports/interfaces;
- runnables;
- application/implementation data types;
- RTE access operations;
- workspace persistence;
- AUTOSAR XML import/export;
- selected component type → software-component description export.

This is enough to define a bounded authoring/export workflow but not a click-by-click diagnostic-facing SWC procedure.

DTR-004 is therefore `PARTIAL_PROCEDURE_AVAILABLE`.

### 5.3 MathWorks R2025b

The MathWorks route contains several explicit APIs and execution modes.

#### ARXML import/update

Reviewed explicit operations include:

```text
arxml.importer
createComponentAsModel
updateModel
updateAUTOSARProperties
```

The distinction between initial import, changed Classic ARXML update, and shared-definition update is source-explicit. A complete project invocation, argument set, and post-import inspection script is not compiled, so DTR-005 remains `PARTIAL_PROCEDURE_AVAILABLE` rather than exact.

#### Behavior and mapping

Simulink/Stateflow and AUTOSAR mapping ownership is clear, but Management ECU behavior and contract-specific mapping are project-specific. DTR-006 and DTR-007 remain `WORKFLOW_ONLY`.

#### MIL

The reviewed test lifecycle names Test Manager, TestFile/TestSuite/TestCase, harnesses, execution lifecycle, result objects, requirement links, and coverage objects. For this corpus, `MIL` remains model-execution workflow terminology; the model-side execution in the reviewed MIL/SIL example is `Normal` mode.

DTR-008 is `PARTIAL_PROCEDURE_AVAILABLE`.

#### Code generation

The reviewed boundary is explicit:

```text
code generation != compile != link
```

AUTOSAR Classic generation produces C/H and ARXML; local RTE stubs are not production MICROSAR RTE. `Generate code only`, `codebuild`, and report-generation surfaces are explicit, but project generation configuration is not.

DTR-009 is `PARTIAL_PROCEDURE_AVAILABLE`.

#### SIL

SIL is explicit host-compiled generated-code execution. The source distinguishes SIL results from model/MIL results and from target/PIL/HIL execution.

DTR-010 is `PARTIAL_PROCEDURE_AVAILABLE`.

### 5.4 DaVinci Configurator Classic 6.3.10 / MICROSAR

This is the largest current procedure gap.

Reviewed Vector authority strongly establishes Configurator as the Classic AUTOSAR ECU configuration, validation and BSW/RTE generation tool. It also exposes automation/CLI surfaces, including:

```text
dvcfg-b project generate
```

AUTOSAR direct authority independently closes the ownership split:

```text
DCM = tester-facing diagnostic service/session/security/request-response processing
DEM = event/DTC/status/fault-memory ownership
PduR = network-independent transport/routing boundary
CanTp = configured CAN transport segmentation/reassembly/flow-control branch
CanIf = CAN-hardware-independent integration
CanDrv = controller hardware access
```

But the frozen Configurator Reviewed Knowledge does **not** provide a version-specific DCM/DEM configuration-object procedure, diagnostic callback/RTE mapping sequence, or Management-ECU-specific PduR/CanTp/CanIf/Can setup sequence.

Results:

- DTR-011: `WORKFLOW_ONLY`;
- DTR-012: `WORKFLOW_ONLY`;
- DTR-013: `PROJECT_INPUT_REQUIRED`;
- DTR-014: `PARTIAL_PROCEDURE_AVAILABLE` because source generation has an explicit CLI route.

### 5.5 vVIRTUALtarget 10 family

The reviewed corpus distinguishes **Integration** from **BSW Emulation** and provides explicit VttMake/DPA/DVJSON/VTTJSON/build/package surfaces. It does not close one complete artifact/version recipe across all Integration variants.

DTR-015 is `PARTIAL_PROCEDURE_AVAILABLE`.

### 5.6 CANoe 20.2.1

For virtual-SUT setup, the reviewed consumer route explicitly provides:

- Communication Setup → `Add VTT model`;
- Diagnostics/ISO TP Configuration;
- diagnostic-description consumer semantics;
- ECU qualifier/variant/network context.

The complete load/rebuild/version compatibility contract remains partial. Therefore DTR-016 is `PARTIAL_PROCEDURE_AVAILABLE`.

### 5.7 CANoe.DiVa 20

DiVa Reviewed Knowledge is strong for specification-driven project setup and generation.

Project Configuration explicitly includes:

- ECU Information;
- CANoe Environment;
- Additional Resources.

Generation includes the explicit CLI route:

```text
diva-make.exe diva.yaml [options]
```

The corpus also distinguishes Test Module and Test Unit behavior, including DiVa Test Unit re-import/recompile requirements in CANoe.

DTR-017 and DTR-018 are `PARTIAL_PROCEDURE_AVAILABLE` because the exact GUI sequence/options/project-specific generation scope remain incomplete.

### 5.8 DiVa → CANoe named execution route

This is the strongest bounded route in the compilation. Two-sided Vector evidence establishes the sequence:

```text
Diagnostics & XCP | Test | Import DiVa Project
  -> Assigned Bus
  -> Diagnostics/ISO TP configuration
  -> ECU Qualifier matching
  -> Test Module/Test Unit selection
  -> measurement/test execution
  -> report access
```

For Test Units changed by DiVa, re-import is required so CANoe recompiles the executable.

Within this bounded scope, no missing intermediate operational step needs to be invented. DTR-019 is therefore `EXACT_PROCEDURE_AVAILABLE`.

This exact classification does **not** claim that the full DiVa project serialization or cross-product version matrix is closed.

## 6. Retained bounded / negative findings

The following findings must remain explicit:

1. **No one mandatory CANdela 25 SP1 export subset for DiVa 20.** Format overlap and supported CDD/ODX routes are real; a universal producer subset is not established.
2. **No universal direct CANdela → Configurator 6.3.10 synchronization/import contract.** Legacy diagnostic import wording does not establish a current bridge.
3. **CDD/ODX is not a lossless CANdela round trip.** Events and selected content can be omitted or approximated; warnings/errors matter.
4. **DCM != DEM.** DCM owns tester-facing service processing; DEM owns event/DTC/fault memory.
5. **DCM service semantics != CanTp transport.** `DCM ↔ PduR ↔ CanTp ↔ CanIf ↔ CanDrv` is a configured ownership/navigation branch, not a universal runtime call sequence.
6. **Application SWC != production RTE/BSW.** MathWorks generated C/ARXML and local RTE stubs do not replace MICROSAR production RTE/BSW generation.
7. **MIL != SIL != VECU execution.** Each is a distinct execution/result identity.
8. **vVIRTUALtarget Integration != BSW Emulation.** Their prerequisites and artifact semantics differ.
9. **DiVa project != generated test != Test Module/Test Unit != CANoe execution result/report.**
10. **DiVa Test Unit re-import/recompile is product-specific.** It is not a universal Test Unit schema/build rule.

## 7. Project-input blockers

Execution-level work remains blocked wherever the project has not fixed its own values.

The current project baseline still has `TBD_PROJECT_DECISION` for, among other items:

- service/subfunction inventory;
- DID definitions;
- RoutineControl definitions;
- DTC/event model;
- sessions;
- security/access policy;
- NRC/application-result policy;
- P2/P2* timing;
- which diagnostic elements require Application SWC behavior;
- diagnostic test objectives;
- actual tool releases and AUTOSAR schema;
- CAN/CAN FD project choice;
- CAN network/channel/controller identity;
- physical/functional request/response addressing;
- CanTp addressing/connection/N-SDU/N-PDU/timing/flow-control configuration;
- PduR routes;
- CanIf/CAN lower-layer configuration;
- CANoe/DiVa network binding.

DTR-013 is classified `PROJECT_INPUT_REQUIRED` because these values are material to the actual Configurator transport configuration and are intentionally absent.

## 8. Procedure gaps requiring future authority work

The highest-value future procedure research targets are:

1. **Configurator/MICROSAR diagnostic configuration** — exact 6.3.10 DCM/DEM object and application callback/RTE mapping procedure.
2. **Configurator/MICROSAR UDS-on-CAN configuration** — exact PduR/CanTp/CanIf/Can configuration sequence once project values are fixed.
3. **CANdela authoring** — exact 25 SP1 menu/dialog sequence for creating/editing the relevant diagnostic objects and exporting selected handoff formats.
4. **Developer diagnostic-facing SWC authoring** — exact 4.18 SP3 object creation/export sequence.
5. **vVIRTUALtarget Integration** — complete artifact/version-specific recipe for the selected Management ECU Integration path.
6. **CANoe virtual-SUT configuration** — complete VTT model/diagnostic-description load/reload/version procedure.
7. **DiVa project/generation** — complete project creation/import configuration and CLI option profile for the selected diagnostic input route.

These are procedure-authority gaps, not evidence that the tools cannot perform the functions.

## 9. Immutable inputs / denylist

This compilation did not modify:

- the project Methodology;
- the Step-by-Step Guide;
- the Reference Index;
- the Tool/Task/Reference Matrix;
- the Execution & Reference Guide;
- any `references/**` file;
- canonical `docs/knowledge/**`;
- `inventory/**`;
- the upstream Vector, MathWorks, or AUTOSAR repositories.

Only the procedure compilation matrix, this report, and the terminal checkpoint are authorized outputs for this work unit.

## 10. Sol synthesis questions

The following are questions for Sol review; this compilation does not answer them.

1. Should DTR-019's exact named DiVa→CANoe route be promoted into the user-facing Execution Guide as the first truly reproducible procedure slice?
2. Should DTR-005 preserve individual MathWorks API names in the user-facing guide while remaining `PARTIAL_PROCEDURE_AVAILABLE` at whole-task level?
3. Should DTR-014 expose `dvcfg-b project generate` directly in the final guide, or keep it behind a release-compatibility guard until actual project Configurator/MICROSAR versions are fixed?
4. Should Configurator/MICROSAR DCM/DEM procedure research be the next dedicated authority-expansion unit, given that it is the largest gap between a known ownership model and an actionable engineering procedure?
5. Should DTR-013 remain blocked in the public matrix until a concrete Management ECU UDS-on-CAN network baseline is supplied, even if a later procedure-authority package closes the GUI sequence?
6. Should CANdela authoring and DiVa generation be split into separate public procedure families so that diagnostic specification authority cannot be mistaken for diagnostic test authority?
