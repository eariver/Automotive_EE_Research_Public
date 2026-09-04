# Management ECU DEM Fault Management — Execution Reference Guide

Status: **Luna compile proposal; execution is project-input-first**

This guide identifies the reviewed product-local routes and the evidence each route can produce. It is not an execution log. All authority tags resolve to exact tuples in the Reference Index.

## Route overview

| Route | Product identity in reviewed authority | Reviewed operation | Project gate | Evidence boundary |
|---|---|---|---|---|
| Semantic/configuration | DaVinci Configurator Classic 6.3.10 / MICROSAR DEM | bounded Diagnostics Editor/integration surfaces; Dem/NvM assistant mapping; `dvcfg-b project validate`; `dvcfg-b project generate` | project package, schema, DEM data and policy | generated BSW/RTE is not runtime evidence |
| Virtual runtime | vVIRTUALtarget 10-family Integration + CANoe 20.2.1 | generated BSW/RTE/Application -> Integration SUT representation -> build/package -> CANoe load/configuration -> bounded stimulus | Integration artifacts, diagnostic context, stimulus and acceptance | tester response is not internal DEM/NvM proof |
| DTC test generation | CANoe.DiVa 20 | DTC Test Configuration -> selection/stimulation/coverage -> `diva-make.exe diva.yaml [options]` | diagnostic description, DTC rows, qualifier/variant, stimulus, expected result | generated test is not execution/result |
| DTC test execution | CANoe 20.2.1 | DiVa import -> Test Module/Test Unit -> re-import/recompile where applicable -> compile/execute -> trace/result/report | actual CANoe configuration and generated project | result/report do not prove internal DEM state |
| Model verification | MathWorks R2025b / MATLAB 25.2 | Simulink Test definition -> model execution -> results/report; coverage separate | project model, vectors, criteria and coverage policy | model/SIL result is not DEM runtime |
| Generated-code verification | MathWorks R2025b / MATLAB 25.2 | generated source -> SIL/PIL scope -> host/target execution -> logged result/equivalence | generated scope, toolchain, signals, tolerances | SIL/PIL is not production VECU/DEM runtime |

Vector identity and route scope: `[VECTOR-DEM-D922]`  
MathWorks product identity and lifecycle: `[MW-PROC-2FB] [MW-MIL-SIL-2FB] [MW-TEST-2FB] [MW-COVERAGE-2FB]`

## V1 — Configurator / MICROSAR DEM realization

The standard-side checklist is the AUTOSAR semantic-depth supplement. The Vector surface is independently bounded; a container name or ECUC class does not locate a Vector GUI object. `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922]`

### Input gate

Require, from the project:

- actual selected Configurator/MICROSAR release and package;
- AUTOSAR schema/profile;
- Event/DTC inventory and mapping/combination decisions;
- monitor-to-DEM reporting contract;
- debounce ownership and values;
- operation-cycle physical meaning;
- enable/storage conditions;
- memory, event-data and persistence decisions;
- validation/generation configuration and acceptance rules.

No item may be supplied from an AUTOSAR example, vendor sample or generic assumption.

### Execution sequence

1. Open the project Configurator package and identify the project-selected DEM root/configuration set.
2. Walk the semantic checklist: reporting boundary; debounce/predebounce; operation cycle; enable condition; storage condition; monitor/event/UDS-DTC status; callback timing; Event-to-DTC relation; event combination; event memory; priority/displacement/storage trigger; freeze-frame/extended data/data elements; aging; AUTOSAR DEM indicator healing; ClearDTC behavior; DEM/NvM mapping.
3. For each area, record the project object, the applicable/not-applicable/unresolved decision and the page-local reviewed evidence. Do not infer missing object mappings from AUTOSAR names.
4. Inspect the Dem/NvM Event Memory Blocks Assistant only as a bounded mapping surface.
5. Run `dvcfg-b project validate` and retain the validation result.
6. Run `dvcfg-b project generate` and retain generated BSW/RTE artifacts and reports.
7. Mark the generated configuration boundary and hand off only the generated package/artifact set to the Integration route.

### V1 exit criteria

- semantic decisions are separate and project-approved;
- validation/generation results are retained;
- generated BSW/RTE identity is explicit;
- the assistant is not used as evidence of complete DEM configuration;
- no runtime or tester conclusion is drawn from static/generated configuration.

Proposed availability for the Configurator task: `PARTIAL_PROCEDURE_AVAILABLE`. Detailed object-by-object DEM mapping remains a documentation-scope gap in the exact reviewed root. `[VECTOR-DEM-D922]`

## V2 — vVIRTUALtarget Integration / CANoe runtime

### Input gate

Require a project-generated Integration package, SUT-DLL/build inputs, CANoe diagnostic description and network context, qualifier/variant/addressing, an authorized bounded fault/condition stimulus, expected observable response and acceptance criteria. The actual project runtime is not performed by this compilation. `[VECTOR-DEM-D922]`

### Canonical sequence

1. Start with configured/generated DEM/RTE/BSW and Application artifacts.
2. Use **vVIRTUALtarget Integration** to create the Integration SUT representation.
3. Build/package the representation and retain package/build provenance.
4. In CANoe, use the reviewed node/component loading surface to add/select the SUT representation.
5. Apply project diagnostic configuration, including only project-supplied network and addressing information.
6. Apply the bounded project stimulus or condition sequence.
7. Observe the tester-facing diagnostic response and trace.
8. Record the execution result separately from the response.
9. If the project requires internal DEM debounce, event-memory or NvM evidence, activate the authorized project instrumentation bridge and record its symbol/bridge identity. If none exists, record `RUNTIME_OBSERVABILITY_GAP`.

### V2 evidence ledger

| Evidence item | May establish | Does not establish |
|---|---|---|
| Integration SUT representation | loaded virtual-SUT artifact identity | successful DEM configuration or runtime state |
| build/package record | produced package and build state | tester response or internal state |
| CANoe load/configuration | consumer configuration state | internal DEM state |
| fault/condition stimulus | input/test setup | monitor result, event report or DTC status |
| tester-visible DTC response | DCM-facing observation | DEM debounce, event-memory entry or NvM representation |
| instrumentation record | selected internal observation route | correctness unless project acceptance evaluates it |
| execution result | runtime outcome for the executed setup | universal project or cross-product contract |

The canonical route is Integration. BSW Emulation, `vttsut` or an `Add VTT model` alternative is not substituted for the Management ECU route. `[VECTOR-DEM-D922]`

## V3 — CANoe.DiVa / CANoe test evidence

### Input gate

Require a selected diagnostic description, DTC Test Configuration scope, ECU/variant/qualifier and addressing context, project DTC rows, authorized generic stimulation/system conditions, expected status transitions, tolerances and acceptance criteria. `[VECTOR-DEM-D922]`

### Product-local generation sequence

1. Select the diagnostic description and project DTC rows in the DiVa DTC Test Configuration.
2. Configure only project-authorized stimulation, coverage model and expectations.
3. Run `diva-make.exe diva.yaml [options]`.
4. Retain generated test specification/module/unit artifacts and generation diagnostics.

### Product-local CANoe sequence

1. Import the generated project through `Diagnostics & XCP | Test | Import DiVa Project`.
2. Use the project Assigned Bus or manual Diagnostics/ISO TP setup.
3. Check ECU qualifier equality between generated DiVa content and CANoe configuration.
4. Select the generated Test Module/Test Unit.
5. Re-import/recompile the Test Unit where applicable, then compile the Test Configuration.
6. Execute the selected test.
7. Retain Test Trace, execution result/verdict and report as separate artifacts.

### V3 exit criteria

- generated definition is retained separately from CANoe execution;
- execution result/verdict is retained separately from report;
- tester response is not called internal DEM state;
- product-local routes are evaluated independently;
- the negative remains that no one universal cross-product Test Unit package/build/runtime contract is established by reviewed documentation.

DiVa generation is not CANoe execution, execution result, report or DEM internal state. `[VECTOR-DEM-D922]`

## MathWorks supporting verification routes

### Model-level route

The reviewed R2025b route is: create/open TestFile/TestSuite/TestCase, bind the project model/harness and inputs, run model execution, inspect the result hierarchy, export results/reports and evaluate coverage separately. Model/fault simulation evidence supports monitor verification but does not become DEM runtime state. `[MW-PROC-2FB] [MW-TEST-2FB] [MW-FAULT-2FB] [MW-COVERAGE-2FB]`

### Generated-code/SIL route

The reviewed route starts from generated-code prerequisites, selects top-model or Model-block SIL/PIL scope, runs host SIL or target/ISS PIL as configured, inspects logged outputs, and optionally compares model and generated-code results under project criteria/tolerances. The result is not a VECU/CANoe/production DEM execution result. `[MW-PROC-2FB] [MW-MIL-SIL-2FB]`

## Evidence ownership and failure triage

When a route fails, classify the failure before proposing a cause:

1. project input/design missing;
2. static configuration invalid;
3. generated configuration/artifact unavailable;
4. package/build/load failure;
5. diagnostic transport/service failure;
6. bounded runtime response mismatch;
7. internal instrumentation unavailable;
8. test definition/generation/import/execution failure;
9. verdict/report/coverage interpretation issue.

Do not skip directly from a tester-visible symptom to an internal DEM conclusion. The state model and exact project evidence are required. `[AUTOSAR-SEM-4EFF] [AUTOSAR-DCM-938] [VECTOR-DEM-D922] [MW-TEST-2FB] [MW-COVERAGE-2FB]`

## Reusable closure checklist

- [ ] Project baseline is supplied or explicitly TBD.
- [ ] Monitor design and reporting contract are approved.
- [ ] DEM semantic decisions are independently recorded.
- [ ] Configurator validation/generation artifacts are retained.
- [ ] Integration package and CANoe load evidence are retained.
- [ ] Runtime stimulus and tester observation are authorized and identified.
- [ ] Internal observability gap is recorded or project instrumentation evidence exists.
- [ ] DiVa generation and CANoe execution artifacts are separate.
- [ ] Result, verdict, coverage and report identities are separate.
- [ ] Exact reviewed authority tuple is attached to every technical assertion.
- [ ] No project value has been inferred.
