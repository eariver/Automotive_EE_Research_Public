# Management ECU UDS on CAN — Procedure Authority Expansion Addendum

Date: 2026-09-03 JST

Status: **SOL-REVIEWED DOWNSTREAM SYNTHESIS**

This addendum updates the procedure-readiness view of the 2026-09-02 diagnostic engineering package after targeted Vector and MathWorks authority expansion. It does not replace the Methodology, Step-by-Step Guide, Tool/Task Matrix, or the original Luna procedure compilation. It is the human-readable companion to `procedures/procedure-authority-expansion-overlay.yaml`.

## Reviewed upstream pins

Vector:

- repository: `eariver/Research_Vector_Documents`
- Luna terminal: `da8a8f3d5c9f159f964130d7e248ddf938732ce1`
- Sol-reviewed ending SHA: `bcbe4e5b57aa144bfa5cb3d5e86f2a1e5a1274ee`
- reviewed supplement: `docs/knowledge/management-ecu-uds-can-vector-procedure-authority-expansion.md`

MathWorks:

- repository: `eariver/Research_MathWorks_Documents`
- release boundary: R2025b / MATLAB 25.2
- Luna terminal: `f01fbd660d0704449dd094fd8baeec674d0ee585`
- Sol-reviewed ending SHA: `2fb38fe40d87a9cb8e7a22f7fe4a1a6a04354187`
- reviewed supplement: `docs/knowledge/management-ecu-uds-can-mathworks-procedure-authority-expansion.md`

Resolve these through `references/procedure-authority-expansion-pins.yaml`.

## Final procedure maturity

| Classification | Count |
|---|---:|
| EXACT_PROCEDURE_AVAILABLE | 11 |
| PARTIAL_PROCEDURE_AVAILABLE | 5 |
| WORKFLOW_ONLY | 1 |
| PROJECT_INPUT_REQUIRED | 1 |
| UNRESOLVED_AUTHORITY | 0 |
| Total | 18 |

The eleven exact bounded tasks are:

`DTR-002`, `DTR-004`, `DTR-005`, `DTR-007`, `DTR-008`, `DTR-009`, `DTR-010`, `DTR-015`, `DTR-016`, `DTR-018`, `DTR-019`.

Exact means that a bounded operation sequence is source-explicit at the reviewed product/release scope. It does **not** mean that Management ECU project values, actual execution results, interoperability or production acceptance have already been established.

## Updated intent-first route

### CANdela diagnostic authoring — DTR-002

Classification: `EXACT_PROCEDURE_AVAILABLE`.

Use CANdela Studio 25 SP1 bounded authoring surfaces for supported interfaces, service/event objects and DEXT/data-exchange operations. The actual DID/RID/DTC/session/security values, variants and acceptance criteria remain project-owned.

### CANdela export/handoff — DTR-003

Classification: `PARTIAL_PROCEDURE_AVAILABLE`.

ODX export modes, PDX packaging, compliance checking and warning/error surfaces are explicit. The retained documentation-scope negative remains: no one universal mandatory CANdela Studio 25 SP1 export subset has been established as the formal DiVa 20 producer contract. Do not convert a supported export mode into a universal handoff rule.

### DaVinci Developer Application SWC contract — DTR-004

Classification: `EXACT_PROCEDURE_AVAILABLE` at 4.18 SP3-family scope.

Use the reviewed component/port/runnable/diagnostic-port, ARXML import/export and consistency-check routes. The diagnostic-port assistant is heuristic and cannot choose canonical application architecture. `.67` remains a source-root label, not an independently elevated compatibility claim.

### AUTOSAR Blockset ARXML import/update — DTR-005

Classification: `EXACT_PROCEDURE_AVAILABLE` at MathWorks R2025b.

Canonical bounded route:

```text
arxml.importer(...)
  -> discover component/composition
  -> createComponentAsModel / importFromARXML
  -> updateModel when mapped-component ARXML changes
  -> updateAUTOSARProperties for shared definitions
  -> updateArchitecturalData for Architectural Data dictionary changes
  -> autosar.api.validateModel / Code Mappings Validate
```

Keep mapped-component update, shared-definition update and Architectural Data update distinct. Source ARXML, imported representation and generated implementation ARXML remain separate artifacts.

### Application diagnostic behavior — DTR-006

Classification: `WORKFLOW_ONLY`.

This is intentionally **project design first**. Simulink/Stateflow procedure cannot determine Management ECU behavior, session-dependent policy, callback semantics or application fault policy. Implement only after those project decisions exist.

### AUTOSAR mapping — DTR-007

Classification: `EXACT_PROCEDURE_AVAILABLE` at MathWorks R2025b.

Canonical bounded route:

```text
Apps > AUTOSAR Component Designer
  -> Code Interface > AUTOSAR Dictionary
  -> define/inspect AUTOSAR contract-side elements
  -> Code Mappings editor
  -> map Functions / Inports-Outports / Parameters / Data Stores-Signals-States / Data Transfers / Function Callers
  -> Update
  -> Validate
```

Programmatic mapping/property APIs are also reviewed. Mapping completion is not generation, compile/link, RTE integration or runtime evidence.

### MIL / Simulink Test — DTR-008

Classification: `EXACT_PROCEDURE_AVAILABLE` at MathWorks R2025b.

Canonical bounded route:

```text
Test Manager
  -> TestFile / TestSuite / TestCase
  -> assign project model + project-owned inputs/criteria/harness/iterations
  -> Run
  -> ResultSet/result hierarchy
  -> export result data
  -> generate report
  -> inspect coverage separately if required
```

Test definition, execution result, report and coverage remain separate. Test vector, expected value, tolerance and acceptance are project inputs.

### Embedded Coder AUTOSAR generation — DTR-009

Classification: `EXACT_PROCEDURE_AVAILABLE` at MathWorks R2025b.

Canonical bounded route:

```text
mapped AUTOSAR model
  -> Generate Code / project-equivalent route
  -> generated C/C++ + ARXML + local RTE stub + code-generation report
  -> optional separate compile/link via slbuild/codebuild/project build
  -> downstream production integration remains separate
```

Code generation != compile != link. MathWorks local RTE stub != production MICROSAR RTE.

### SIL — DTR-010

Classification: `EXACT_PROCEDURE_AVAILABLE` at MathWorks R2025b.

Canonical bounded route:

```text
generated-code prerequisite
  -> SIL/PIL Manager
  -> select top-model or Model-block scope
  -> select SIL or PIL
  -> configure project-approved logging/options
  -> Run SIL/PIL
  -> Data Inspector
  -> if required, run model baseline and SIL leg with same project stimulus
  -> compare using explicit project criteria
```

SIL host execution != PIL target/ISS execution. Generic SIL success != model/SIL equivalence verdict. Equivalence != coverage.

### DCM/DEM configuration — DTR-011

Classification: `PARTIAL_PROCEDURE_AVAILABLE`.

Configurator 6.3.10 exposes Diagnostics Editor and the Dem/NvM Event Memory Blocks Assistant. This is sufficient for bounded persistence/object operations, but not a complete DCM service/session/security and complete DEM event/DTC object procedure.

### Application SWC / production RTE diagnostic integration — DTR-012

Classification: `PARTIAL_PROCEDURE_AVAILABLE`.

Service Ports / Component Connection Assistant is source-explicit and Configurator explicitly hands application-component editing to Developer. The project-specific callback/runnable to production RTE/DCM integration and generated interface identity remain incomplete.

### UDS-on-CAN lower transport configuration — DTR-013

Classification: `PROJECT_INPUT_REQUIRED`.

Do not proceed until Management ECU network inputs are fixed. In particular, do not invent CAN IDs, physical/functional addressing, N-SDU/N-PDU identities, CanTp timing, PduR route, CanIf/CAN channel/controller identity or P2/P2* values.

### Configurator validate/generate/reconciliation — DTR-014

Classification: `PARTIAL_PROCEDURE_AVAILABLE`.

Exact reviewed command surfaces include:

```text
dvcfg-b project validate -p=<DaVinciProject> -b=<BSWPackage>
dvcfg-b project generate -p=<DaVinciProject> -b=<BSWPackage>
```

Project reconciliation, compile/link/build and final artifact acceptance remain separate.

### vVIRTUALtarget — DTR-015

Classification: `EXACT_PROCEDURE_AVAILABLE` at vVIRTUALtarget 10-series scope.

Sol project decision: canonical route = **Integration**.

Use the reviewed DPA/DVJSON/VttMake Integration path, including bounded update/generation/build surfaces, to obtain the Integration SUT-DLL/simulation-package family. BSW Emulation remains a separate alternate route; do not substitute its `vttsut`/vmodule/vCDL/vCODM artifact family into the canonical Integration route.

Page-local 10 SP2 labels remain page-local; the full root is not promoted to root-wide 10 SP2 identity.

### CANoe virtual diagnostic runtime — DTR-016

Classification: `EXACT_PROCEDURE_AVAILABLE` at CANoe 20.2.1 scope.

Canonical project route:

```text
Integration SUT DLL
  -> CANoe node Configuration > Components > Add
  -> Diagnostics & XCP > Diagnostics/ISO TP Configuration
  -> bind project diagnostic description to the pre-existing Simulation Setup network
  -> configure/use ECU qualifier and required diagnostic windows
```

The BSW Emulation `Import VTT Model` path is retained as an alternate, non-canonical route. Project network/addressing/timing values remain DTR-013 inputs.

### DiVa project configuration — DTR-017

Classification: `PARTIAL_PROCEDURE_AVAILABLE`.

Project Configuration and its ECU Information, CANoe Environment and Additional Resources areas are explicit. Project creation values, persistence/validation state and external-resource acceptance remain project-specific.

### DiVa generation — DTR-018

Classification: `EXACT_PROCEDURE_AVAILABLE`.

Canonical bounded generation command:

```text
diva-make.exe diva.yaml [options]
```

Output/log/verbose/error surfaces and bounded test-configuration areas are reviewed. Test generation is not CANoe test execution.

### DiVa -> CANoe execution — DTR-019

Classification: `EXACT_PROCEDURE_AVAILABLE`, unchanged.

Retain the previously accepted bounded route:

```text
Diagnostics & XCP | Test | Import DiVa Project
  -> Assigned Bus
  -> Diagnostics/ISO TP
  -> ECU Qualifier
  -> Test Module/Test Unit
  -> re-import/recompile when required
  -> CANoe execution
  -> report
```

## Remaining reasons this is not an ECU-specific recipe

The package now has strong operation-level coverage, but it intentionally does not contain Management ECU project values or claimed execution results. The following still require actual project input/design/evidence:

- diagnostic object IDs and session/security/NRC policy;
- Application SWC diagnostic behavior;
- CAN/CanTp/PduR/CanIf concrete routing and timing;
- exact Application-to-RTE/DCM callback integration;
- complete DCM/DEM object configuration;
- actual compile/link/build toolchain and result;
- actual vVIRTUALtarget/CANoe load/run acceptance;
- actual DiVa test scope/result;
- actual MIL/SIL comparison verdict and coverage target.

This is intentional. Procedure authority identifies **how and where to work**; it does not manufacture the project design or evidence.
