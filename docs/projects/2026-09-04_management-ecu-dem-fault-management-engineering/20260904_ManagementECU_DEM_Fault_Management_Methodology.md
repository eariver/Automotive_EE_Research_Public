# Management ECU DEM Fault Management — Compilation Methodology

Status: **Luna compile proposal; Sol final maturity pending**  
Date: 2026-09-04

## Purpose and scope

This package organizes the current Management ECU DEM fault-management engineering route from project baseline through Application design, DEM configuration, persistence, DCM/FiM ownership, virtual runtime, diagnostic test evidence and end-to-end handoff. It is a synthesis-by-organization unit, not a new technical research unit. The package does not reopen the completed AUTOSAR semantic-depth Luna unit.

The machine-readable matrices contain one record for each of the twenty project tasks. The same typed chain is usable in both directions:

```text
engineering intent -> lifecycle -> task -> owner/tool -> reviewed reference
-> operation -> input -> output/state -> exit condition -> handoff
```

and:

```text
observed symptom -> owning state/layer -> configuration/runtime evidence
-> upstream cause candidate -> next evidence request
```

## Authority and provenance method

Technical statements are tagged by authority IDs resolved to full repository/commit/path tuples in the Reference Index. The primary current pins are:

| Authority | Exact reviewed tuple | Use |
|---|---|---|
| AUTOSAR DEM semantic depth | `eariver/Research_AUTOSAR_CP_Documents@4eff43bdc4a99f3219104c2b16994a539e0b08eb:docs/knowledge/management-ecu-dem-autosar-semantic-depth.md` | DEM semantic checklist and state distinctions |
| Vector DEM procedure/runtime/test | `eariver/Research_Vector_Documents@d922812a20ed1e9669fff45f26aa17791254ae65:docs/knowledge/management-ecu-dem-vector-procedure-runtime-test.md` | Configurator, Integration/CANoe and DiVa/CANoe reviewed boundaries |
| MathWorks R2025b | `eariver/Research_MathWorks_Documents@2fb38fe40d87a9cb8e7a22f7fe4a1a6a04354187` with the pinned paths in the Reference Index | model, ARXML, MIL/SIL, test, coverage and fault lifecycle |

The package also identifies the three supporting AUTOSAR CP 4.4.0 exact pins listed in `authority-pins.yaml` for the already-reviewed ownership and DCM/FiM workflow surfaces. They are not floating upstream sources and are not new research. No Web page, current vendor page, raw HELP or raw AUTOSAR PDF was used.

## Compilation rules

1. Keep standard semantic authority separate from vendor realization. AUTOSAR class/container terminology is a semantic checklist; it does not name or locate a Vector GUI object. `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922]`
2. Treat every availability label as a Luna proposal. Sol owns final acceptance, maturity and any terminal classification.
3. Treat project values and project design as inputs, not as gaps to be filled with examples. The project input baseline is currently `PROJECT_INPUTS_NOT_YET_SUPPLIED`.
4. Preserve artifact identity at each handoff: configuration, generated configuration, runtime state, tester response, test definition, execution, verdict, coverage and report are separate unless an exact authority relates them.
5. Record the strongest reviewed operation even when its project execution is blocked. A workflow or product-local route is not an executed project result.
6. Keep independent safe frontiers open. Configurator mapping ambiguity does not block product-local runtime/test organization; a runtime internal-observability gap does not block tester-facing DiVa/CANoe procedure organization; the universal Test Unit negative does not block product-local generation or import/execution.

## Semantic non-collapse contract

The following relations are mandatory package invariants:

```text
fault condition
!= monitor algorithm / implementation
!= monitor result
!= DEM event report
!= debounce / qualification
!= monitor status
!= event UDS status
!= DTC status
!= DTC identity
!= event-memory entry
!= NvM representation
!= DCM tester response
!= test definition
!= execution
!= verdict
!= report
```

Also retain:

- `Event != DTC`;
- `DEM != DCM`, `DEM != FiM`, and `DEM != NvM`;
- `enable condition != storage condition`;
- `operation cycle != ignition cycle by default`;
- `ClearDTC != monitor pass != aging != AUTOSAR DEM indicator healing`;
- `configuration != generated configuration != runtime state != tester response`;
- `verdict != coverage`.

The AUTOSAR semantic supplement specifically requires two debounce routes: DEM-internal debounce and monitor-internal/predebounce. The project monitor design and project inputs must choose ownership and values. It also requires an explicit physical meaning for every operation cycle, separate evidence for monitor/event/UDS-DTC status and callback timing, and independent decisions for Event-to-DTC relation, event combination, event-memory representation and event-related-data ownership. `[AUTOSAR-SEM-4EFF]`

## Availability proposal policy

Only these labels are used in the matrices:

- `EXACT_PROCEDURE_AVAILABLE` — a reviewed operation sequence is explicit at the relevant abstraction, while project values may still be needed;
- `PARTIAL_PROCEDURE_AVAILABLE` — a bounded operation or route exists, but important object mapping, project binding or evidence closure is missing;
- `WORKFLOW_ONLY` — ownership or composable lifecycle is reviewed without a complete executable procedure;
- `NO_EXPLICIT_PROCEDURE` — the semantic surface is reviewed, but no complete reviewed product operation is available;
- `PROJECT_INPUT_REQUIRED` — the baseline itself is the blocking input;
- `PROJECT_DESIGN_REQUIRED` — an approved project design decision must precede meaningful procedure selection.

These are proposals, not Sol maturity decisions.

## Evidence and handoff method

Each task record names its input artifact/state and output artifact/state. Exit conditions are evidence conditions, not assumptions. Project-specific identities such as Event ID, DTC format, cycle binding, threshold, memory layout, diagnostic addressing, stimulus, expected transition and acceptance criteria remain blank/TBD until supplied.

For runtime and test routes, the package distinguishes product-local procedure availability from project execution availability. The reviewed vVIRTUALtarget route is:

```text
configured/generated BSW/RTE + Application
 -> vVIRTUALtarget Integration representation
 -> build/package
 -> CANoe load/configuration
 -> authorized stimulus
 -> tester-visible observation
```

The canonical route is Integration; BSW Emulation is not substituted. A tester-visible response is not proof of internal DEM debounce, event-memory entry or NvM representation. Internal evidence needs a project-specific instrumentation bridge. `[VECTOR-DEM-D922]`

The reviewed DiVa route is likewise split into selected diagnostic description and DTC test configuration, generation, CANoe import/re-import/recompile, execution, result and report. No universal cross-product Test Unit package/build/runtime contract is established, but the DiVa generation route and CANoe product-local import/execution route remain valid independently. `[VECTOR-DEM-D922]`

For model verification, MathWorks R2025b keeps model execution, generated code, host SIL, test definitions, execution results, verdicts, coverage and reports distinct. The package therefore does not turn MIL/SIL evidence or coverage into DEM runtime evidence. `[MW-PROC-2FB] [MW-MIL-SIL-2FB] [MW-TEST-2FB] [MW-COVERAGE-2FB]`

## Validation contract

Before commit, validation must show:

- the Tool / Task / Reference Matrix contains each task identifier exactly once;
- the Procedure Coverage Matrix contains each task identifier exactly once;
- availability counts sum to 20 and use only the allowed labels;
- every technical claim resolves to an exact reviewed authority tuple;
- project-input and project-design blockers remain explicit;
- no new technical evidence or source family was introduced;
- only the nine allowlisted paths are changed;
- the non-collapse contract, Configurator bounded gap, internal DEM observability gap and universal Test Unit documentation negative remain visible.

Validation is a gate for commit and push. This package does not claim actual project configuration, vVIRTUALtarget/CANoe execution, DiVa generation or test result/report completion.
