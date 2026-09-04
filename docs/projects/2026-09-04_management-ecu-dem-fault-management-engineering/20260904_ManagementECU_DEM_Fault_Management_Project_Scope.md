# Management ECU — DEM Fault Management Engineering — Project Scope

Date: 2026-09-04

Status: **SOL-DEFINED INITIAL SCOPE**

## Objective

Create a provenance-preserving, tool-oriented engineering reference for Management ECU DEM-centered fault management from monitor design through tester-visible DTC behavior and verification evidence.

The initial Luna unit is a **baseline compilation and research-gap decomposition**, not new vendor research.

## Task model

### DFM-000 — Fix project baseline

Intent: record actual project tool releases, AUTOSAR schema and project diagnostic/fault-management assumptions separately from reviewed vendor baselines.

Project blocked until real values exist.

### DFM-001 — Allocate fault-management ownership

Intent: classify each fault-management requirement across Application monitor, DEM, DCM, FiM, NvM and verification responsibilities.

### DFM-002 — Define Application monitor behavior

Intent: define what the Application detects and what constitutes monitor pass/fail/precondition behavior.

Project-design-first. Vendor documentation must not choose the Management ECU monitor algorithm.

### DFM-003 — Define Application-to-DEM reporting contract

Intent: identify the reviewed reporting boundary from Application/BSW monitor result to DEM DiagnosticEvent/event-status processing, including generated/RTE-facing identities where applicable.

### DFM-004 — Configure debounce/predebounce

Intent: determine what debounce mechanisms and configuration surfaces exist and what project values are required.

Do not invent thresholds or algorithm selection.

### DFM-005 — Configure operation-cycle / enabling / storage-condition boundaries

Intent: identify the state/configuration objects controlling whether monitoring/status/storage processing is active and how their lifecycles differ.

Do not assume one universal ignition-cycle mapping.

### DFM-006 — Trace event qualification and status evolution

Intent: trace monitor report -> DEM event processing -> monitor/UDS/DTC status semantics without collapsing the states.

### DFM-007 — Configure Event-to-DTC relation

Intent: identify Event/DTC ownership, mapping/combination boundaries and project inputs.

Do not invent DTC numbers or aggregation policy.

### DFM-008 — Configure event/fault-memory lifecycle

Intent: cover entry creation/update/removal, memory destinations, priority/displacement and persistence boundaries where authority exists.

### DFM-009 — Configure event-related data

Intent: cover freeze-frame/environmental and extended-data-style records, capture/update boundaries and project-owned data definitions.

### DFM-010 — Distinguish pass, healing, aging and clear-DTC

Intent: establish the lifecycle/state differences and identify configuration/verification evidence needed for each.

Do not treat them as synonyms.

### DFM-011 — Integrate DCM 0x19 / 0x14 with DEM

Intent: trace tester-facing ReadDTCInformation and ClearDiagnosticInformation service processing across DCM <-> DEM while preserving ownership.

### DFM-012 — Integrate FiM consumer behavior

Intent: trace DEM status to FiM function permission/inhibition without moving DEM ownership into FiM.

### DFM-013 — Integrate DEM persistence with NvM

Intent: identify DEM-owned semantic state versus NvM storage support, including Configurator persistence-assistant boundaries where reviewed.

### DFM-014 — Configure DEM in DaVinci Configurator / MICROSAR

Intent: obtain the strongest version-bounded GUI/CLI procedure for DEM event/DTC/status/memory/data configuration and validation/generation.

This is expected to be a major future Vector research target if the existing Reviewed Knowledge remains incomplete.

### DFM-015 — Verify monitor behavior at MIL

Intent: test Application monitor behavior and project-defined reporting intent at model level while keeping DEM runtime evidence separate.

### DFM-016 — Verify generated monitor behavior at SIL

Intent: verify generated monitor implementation separately from MIL, without claiming DEM/VECU integration evidence.

### DFM-017 — Verify DEM runtime in vVIRTUALtarget / CANoe

Intent: build a bounded virtual-SUT route for driving fault stimuli/monitor conditions and observing DEM/DCM behavior, using the canonical vVIRTUALtarget Integration route where applicable.

### DFM-018 — Generate/execute CANoe.DiVa DTC tests

Intent: identify bounded DiVa/CANoe procedures for DTC status/read/clear test generation and execution. Test generation != execution result.

### DFM-019 — End-to-end evidence closure

Intent: trace one project fault-management requirement through monitor design, event reporting, DEM configuration/state, persistence, DCM visibility and verification artifacts without collapsing identities.

## Required semantic chain

```text
fault condition
!= monitor implementation
!= monitor result
!= event report
!= debounce state
!= event qualification/status
!= DTC status
!= event-memory entry
!= persistent storage representation
!= DCM diagnostic response
!= test verdict/report
```

## Initial research questions for Luna baseline compilation

For each DFM task, determine only from exact-pinned Reviewed Knowledge:

1. What is already explicit and Sol-reviewed?
2. What is the strongest operation/API/GUI/workflow surface?
3. Which artifact/state identities are explicit?
4. Which inputs are necessarily project-owned?
5. Which boundaries/negatives must be retained?
6. Is additional upstream research actually required?
7. If research is required, which repository/product/release/source family should own it?
8. What evidence would be sufficient to promote the task to a stronger procedure maturity?

## Baseline maturity labels

The initial Luna unit may use only:

- `EXACT_PROCEDURE_AVAILABLE`
- `PARTIAL_PROCEDURE_AVAILABLE`
- `WORKFLOW_ONLY`
- `NO_EXPLICIT_PROCEDURE`
- `PROJECT_INPUT_REQUIRED`
- `PROJECT_DESIGN_REQUIRED`
- `UNRESOLVED_AUTHORITY`

Luna records evidence and proposes a classification; Sol makes the final accepted classification.

## Research disposition labels

- `NO_FURTHER_RESEARCH_REQUIRED`
- `RESEARCH_REQUIRED`
- `PROJECT_INPUT_REQUIRED_FIRST`
- `PROJECT_DESIGN_REQUIRED_FIRST`
- `RETAIN_DOCUMENTATION_SCOPE_NEGATIVE`
- `UNRESOLVED_SOURCE_POLICY`

## Expected future research families

The baseline compilation should evaluate, not automatically launch, the following candidate units:

1. **Vector Configurator/MICROSAR DEM procedure authority expansion** — complete event/DTC/debounce/memory/data/NvM relation and validation/generation surfaces.
2. **AUTOSAR CP 4.4.0 DEM semantic depth expansion** — only for semantic areas not already closed in current Reviewed Knowledge.
3. **MathWorks R2025b monitor/fault-stimulus verification procedure expansion** — monitor implementation/MIL/SIL/Fault Analyzer boundaries.
4. **Vector vVIRTUALtarget/CANoe/DiVa fault-management verification expansion** — virtual stimulus, DTC status/read/clear and result evidence.
5. **Application SWC / production RTE integration expansion** — only where the monitor-to-DEM reporting contract remains procedure-incomplete.

Do not combine source families merely to reduce work-unit count if doing so obscures ownership or release provenance.

## Publication target

The final project should be usable in two directions:

```text
engineering intent -> task -> tool -> exact reference -> operation -> artifact -> exit condition
```

and

```text
observed DTC/fault-memory symptom -> owning state/layer -> configuration/runtime evidence -> upstream cause
```
