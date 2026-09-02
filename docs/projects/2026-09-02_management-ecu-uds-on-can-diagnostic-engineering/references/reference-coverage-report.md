# Management ECU UDS on CAN — Reference Coverage Report

Date: 2026-09-02

## Result

The existing frozen Reviewed Knowledge is sufficient to compile an end-to-end **navigation/ownership methodology** for:

```text
CANdela diagnostic specification
 -> Application SWC contract/behavior where applicable
 -> DCM/DEM production diagnostic BSW
 -> UDS-on-CAN PduR/CanTp/CanIf/Can path
 -> integrated ECU software
 -> vVIRTUALtarget Lv3 VECU
 -> CANoe runtime
 -> CANoe.DiVa diagnostic test generation
 -> CANoe execution/result
```

This does not mean every version-specific GUI/API procedure is already closed.

## Technical locator inventory

- downstream canonical navigation: 7
- Vector Reviewed Knowledge locators: 15
- MathWorks Reviewed Knowledge locators: 10
- direct AUTOSAR Classic 4.4.0 locators: 9
- project-input records: 3

Technical locator total: **41**.

## Strongly reviewed routes

The current corpus already provides reviewed authority for:

- CANdela diagnostic authoring and native CDD/CDDT identity;
- bounded ODX exchange semantics;
- CANdela/DiVa supported diagnostic-description overlap;
- CANoe diagnostic description and ISO-TP consumer role;
- DaVinci Developer Application SWC software-design ownership;
- AUTOSAR Blockset ARXML/model representation and mapping lifecycle;
- Simulink/Stateflow source-behavior separation;
- Embedded Coder generation boundary;
- MIL/SIL/test/result/coverage identity;
- AUTOSAR DCM diagnostic service/session/security ownership;
- AUTOSAR DEM event/DTC/fault-memory ownership;
- DCM-to-DEM DTC service interaction;
- diagnostic transport separation with DCM using PduR and a configured CAN branch through CanTp to CanIf;
- CAN hardware abstraction across CanIf and CanDrv;
- Configurator/MICROSAR BSW/RTE configuration/generation role;
- vVIRTUALtarget virtual-ECU construction role;
- named vVIRTUALtarget-to-CANoe virtual-SUT consumer route;
- DiVa diagnostic-data-driven test generation;
- named DiVa-to-CANoe integration/execution route.

## Retained gaps

### DGAP-001 — CANdela -> DiVa producer subset

The reviewed sources establish overlapping CDD/ODX support but do not state that one particular CANdela Studio 25 SP1 export mode/subset is the mandatory formal producer contract for DiVa 20.

Disposition: `NO_EXPLICIT_MAPPING`.

### DGAP-002 — CANdela -> Configurator automatic synchronization

Configurator has production BSW/RTE configuration/generation authority and legacy diagnostic import material, but the frozen corpus does not establish one universal direct CANdela -> Configurator 6.3.10 diagnostic synchronization/import lifecycle.

Disposition: `NO_EXPLICIT_MAPPING`.

The methodology therefore requires explicit specification-to-implementation reconciliation instead of inventing a synchronization bridge.

### DGAP-003 — complete release compatibility matrix

The reviewed products are pinned at specific evidence baselines, but no single cross-product compatibility table proves every actual project version/profile combination.

Disposition: `NO_EXPLICIT_MAPPING` / project compatibility decision required.

## Project blockers intentionally retained

The corpus does not and must not provide Management ECU-specific:

- DID/RID/DTC values;
- service/subfunction inventory;
- session/security/NRC policy;
- P2/P2* or project CanTp timing;
- CAN identifiers/addressing;
- PduR/CanTp/CanIf configuration identities;
- DCM-to-Application callback mapping;
- DEM event/debounce/confirmation policy;
- calibration values;
- test vectors/expected results;
- actual tool releases/schema.

These remain in `references/project/*.yaml` as `TBD_PROJECT_DECISION`.

## Next work unit

The next bounded work should be **Tool Procedure Compilation**, not ECU diagnostic design.

For each DTR task, determine whether the frozen Reviewed Knowledge supports:

- exact GUI route;
- exact API/CLI operation;
- object/workflow-level operation only;
- partial procedure;
- project-input blocker;
- unresolved authority.

No current vendor Web, floating upstream HEAD, raw HELP or generic UDS knowledge should be used to fill procedure gaps unless a separate approved research unit is explicitly opened.