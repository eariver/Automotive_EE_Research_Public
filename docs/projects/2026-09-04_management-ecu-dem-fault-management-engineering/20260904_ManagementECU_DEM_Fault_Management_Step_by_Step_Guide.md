# Management ECU DEM Fault Management — Step-by-Step Guide

Status: **Luna compile proposal; project execution and Sol maturity pending**

This guide is a procedure-oriented index of the current reviewed surfaces. It does not create Management ECU values and it does not assert that a project run has occurred. Authority tags resolve to exact repository/commit/path tuples in `20260904_ManagementECU_DEM_Fault_Management_Reference_Index.yaml`.

## Gate 0 — establish the project boundary

### DFM-000 — fix project baseline

1. Read the pinned authority registry and record each exact repository, commit, release scope and path.
2. Collect the project-controlled tool releases, AUTOSAR schema/profile, diagnostic inventory, monitor/reporting contract, policies, integration interfaces and acceptance records.
3. Mark every absent category `TBD`/`PROJECT_INPUTS_NOT_YET_SUPPLIED`; do not copy examples from an authority into the project baseline.

Output: an approved or explicitly incomplete project baseline.  
Exit/handoff: unresolved project categories remain blockers for project-specific configuration and execution.  
Availability: `PROJECT_INPUT_REQUIRED`.  
Authority: `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922] [MW-PROC-2FB]`

### DFM-001 — allocate ownership

1. Start with the reviewed ownership map.
2. Assign the Application monitor/result, DEM event/DTC/memory state, DCM request/response service processing, FiM permission/inhibition, NvM persistence support and verification evidence to separate layers.
3. Record project-specific responsibility and interface decisions only after the project architecture is supplied.

Output: a typed responsibility map.  
Exit/handoff: no DCM, FiM or NvM assignment absorbs DEM diagnostic ownership.  
Availability: `WORKFLOW_ONLY`.  
Authority: `[AUTOSAR-OWN-938] [AUTOSAR-DCM-938] [AUTOSAR-FIM-938]`

## Gate 1 — define the Application route

### DFM-002 — define monitor behavior

1. Approve the nominal Application model/component identity and its design ownership.
2. Define the project monitor algorithm, detection condition, preconditions and pass/fail/result policy.
3. If modeled faults are used, keep fault definition, enable/activation/trigger selection and simulated effect as separate records.
4. Write the explicit intent for any later DEM report; do not use a Fault Analyzer fault as a DEM event.

Output: approved monitor design and model-level stimulus/result contract.  
Exit/handoff: reporting and model verification may proceed only from this project design.  
Availability: `PROJECT_DESIGN_REQUIRED`.  
Authority: `[MW-MODEL-2FB] [MW-FAULT-2FB] [MW-PROC-2FB]`

### DFM-003 — establish the Application-to-DEM reporting contract

1. Start from the project monitor result, not from a DTC response.
2. Record the reviewed `Dem_SetEventStatus` semantic boundary.
3. Identify the project Application interface, runnable/callback, Event identity and production RTE binding.
4. Use the bounded Vector service-port/component-connection integration surface only as a route marker; require project generated/RTE artifacts to prove the mapping.

Output: monitor result -> DEM event report -> generated/RTE identity trace.  
Exit/handoff: move to debounce and condition decisions only when the reporting boundary is typed.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[AUTOSAR-SEM-4EFF] [AUTOSAR-OWN-938] [VECTOR-DEM-D922]`

## Gate 2 — apply the AUTOSAR semantic checklist and bounded Vector route

The following tasks use the AUTOSAR semantic-depth checklist as standard-side authority and the exact Vector supplement as independent realization authority. Container names do not identify a Vector GUI location. The current Configurator evidence is deliberately bounded. `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922]`

### DFM-004 — debounce/predebounce

1. Decide whether the project monitor design owns monitor-internal/predebounce or DEM owns configured counter/time debounce.
2. For a DEM-internal route, record class, thresholds, increment/decrement, jump, reset/freeze and FDC decisions.
3. For a monitor-internal route, record the qualified report boundary and any allowed FDC behavior.
4. Mark the exact Configurator mapping as unresolved where no page-local operation proves it.

Output: route decision and qualification evidence plan.  
Exit/handoff: qualification remains separate from monitor result and monitor status.  
Availability: `NO_EXPLICIT_PROCEDURE`.  
Authority: `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922]`

### DFM-005 — operation cycle, enable condition and storage condition

1. Name each project-used operation cycle only after its physical/application meaning is approved.
2. Record restart/qualification behavior for the cycle.
3. Record enable-condition gating of report acceptance separately from storage-condition gating of event-memory update/storage.
4. Do not write `ignition cycle` as a default mapping.

Output: separate cycle/enable/storage decision record.  
Exit/handoff: status tracing can use only the project-approved bindings.  
Availability: `NO_EXPLICIT_PROCEDURE`.  
Authority: `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922]`

### DFM-006 — status evolution

1. Capture the monitor result/report input.
2. Capture qualification/debounce state if the project instrumentation exposes it.
3. Capture monitor status, event-level UDS status and DTC status as separate evidence layers.
4. Record synchronous/asynchronous processing and callback notification timing where the project route exposes them.
5. Do not treat one status-byte view, callback or tester response as evidence of all layers.

Output: a layered transition/evidence record.  
Exit/handoff: Event/DTC and memory configuration can be evaluated without collapsing status identities.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[AUTOSAR-SEM-4EFF] [AUTOSAR-OWN-938] [VECTOR-DEM-D922]`

### DFM-007 — Event-to-DTC relation

1. Create separate project records for Event identity and DTC identity.
2. Record the Event-to-DTC relation and any event-combination mode as independent decisions.
3. Trace how the selected combination affects status aggregation and memory/data representation.
4. Require project mapping and numbers; do not infer one Event per DTC or any DTC format.

Output: approved relation/combination decision.  
Exit/handoff: memory and event-data choices can reference the approved relation without merging identities.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[AUTOSAR-SEM-4EFF] [AUTOSAR-OWN-938] [VECTOR-DEM-D922]`

### DFM-008 — event/fault-memory lifecycle

1. Record destination memory, storage trigger and entry allocation/update/removal rules.
2. Record project capacity, priority, overflow and displacement policy.
3. Use the Dem/NvM Event Memory Blocks Assistant only to record its bounded association surface.
4. Capture a runtime event-memory entry separately from its NvM representation and DCM response.

Output: memory lifecycle decision and persistence association.  
Exit/handoff: event-related data and NvM closure remain separate work products.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[AUTOSAR-SEM-4EFF] [AUTOSAR-OWN-938] [VECTOR-DEM-D922]`

### DFM-009 — event-related data

1. Define project-owned snapshot/freeze-frame, pre-storage and extended-data records.
2. Record data-element identity, provider/source, size and capture/update trigger.
3. Configure the selected definitions only after the project data decision exists.
4. Treat a DCM data response as observation of a response path, not proof of the underlying definition or event-memory entry.

Output: data-definition/configuration trace and, later, captured-record evidence.  
Exit/handoff: lifecycle discrimination and persistence may use the approved data ownership.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922]`

### DFM-010 — pass, aging, indicator healing and ClearDTC

1. Define monitor pass as a monitor/report result.
2. Define aging using its own project cycles, counters and conditions.
3. Use `AUTOSAR DEM indicator healing` only for the reviewed 4.4.0 indicator/healing semantics; define any broader project policy separately.
4. Treat ClearDTC as a diagnostic-memory/status operation with its own permissions and conditions.
5. Capture each operation and result separately.

Output: distinct lifecycle evidence map.  
Exit/handoff: DCM service integration can reference ClearDTC without converting it to pass, aging or healing.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[AUTOSAR-SEM-4EFF] [AUTOSAR-DCM-938] [VECTOR-DEM-D922]`

### DFM-013 — DEM/NvM persistence

1. Record the DEM persistence reference edge and the project NvM block descriptor.
2. Record allocation/content responsibility and read/write/startup/shutdown/recovery strategy.
3. Record error/status handling so NvM request/storage state is distinguishable from DEM/DTC state.
4. Require generated/integrated configuration evidence showing that the reference and descriptor resolve consistently.

Output: DEM semantic state -> NvM descriptor -> persistence job/state -> recovered DEM state trace.  
Exit/handoff: Configurator validation/generation may use the trace; DCM response remains a separate observation.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[AUTOSAR-SEM-4EFF] [AUTOSAR-OWN-938] [VECTOR-DEM-D922]`

### DFM-014 — DaVinci Configurator/MICROSAR DEM procedure

1. Establish the actual project release and package/schema inputs; the reviewed release identity is not a fabricated project value.
2. Use the Diagnostics Editor and bounded service-port/component-connection surfaces as applicable.
3. Walk the AUTOSAR checklist across Event/DTC, debounce, cycle/conditions, status/callback, combination, memory, data, aging/healing/ClearDTC and persistence decisions.
4. Inspect the Dem/NvM Event Memory Blocks Assistant only for its bounded mapping surface.
5. Run `dvcfg-b project validate`.
6. Run `dvcfg-b project generate`.
7. Inspect generated BSW/RTE sources and reports as generated artifacts, not runtime proof.
8. Mark each detailed semantic area applicable, not applicable or unresolved with page-local evidence; do not infer GUI structure from AUTOSAR ECUC names.

Output: validated/generated configuration boundary and explicit unresolved areas.  
Exit/handoff: only a project-generated package can enter the Integration runtime route.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[AUTOSAR-SEM-4EFF] [VECTOR-DEM-D922]`

## Gate 3 — tester service and consumer ownership

### DFM-011 — DCM <-> DEM service route

1. Receive the tester request through the project transport/PduR route.
2. Keep DCM request validation, session/security/condition checks and service processing in the DCM layer.
3. Use the reviewed DEM selection/query/clear operations for the DTC/fault-memory work.
4. Preserve asynchronous/`DEM_PENDING` states where applicable.
5. Map DEM results into the DCM/UDS response and transmit through PduR.

Output: request -> DCM processing -> DEM result -> response/transport evidence.  
Exit/handoff: do not use the response as proof of internal DEM state.  
Availability: `EXACT_PROCEDURE_AVAILABLE` at the reviewed generic workflow scope; project service values remain inputs.  
Authority: `[AUTOSAR-DCM-938] [AUTOSAR-OWN-938]`

### DFM-012 — FiM consumer route

1. Identify the source DEM monitor/status evidence.
2. Apply project FID/EventID/inhibition-mask relations.
3. Trace the FiM permission/inhibition calculation and consumer result.
4. Keep FiM notification/initialization behavior separate from DTC status and DCM service processing.

Output: DEM status -> FiM relation -> permission/inhibition evidence.  
Exit/handoff: persistence/runtime work can consume the typed source state without assigning ownership to FiM.  
Availability: `WORKFLOW_ONLY`.  
Authority: `[AUTOSAR-FIM-938] [AUTOSAR-OWN-938]`

## Gate 4 — model and generated monitor verification

### DFM-015 — model-level/MIL verification

1. Create/open a Simulink Test `TestFile`, `TestSuite` and project `TestCase`.
2. Associate the approved monitor model, project vectors, expected outputs, criteria, harness/callbacks and iterations.
3. Run the model-side execution scope.
4. Inspect the `ResultSet`/result hierarchy.
5. Export result data and generate result reports as separate steps.
6. Collect coverage as a parallel evidence stream when required.

Output: model execution result, model-level fault-effect evidence, verdict/report and coverage result.  
Exit/handoff: generated-code verification may use the approved model/test design; no DEM runtime conclusion is drawn.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[MW-PROC-2FB] [MW-TEST-2FB] [MW-COVERAGE-2FB] [MW-FAULT-2FB]`

### DFM-016 — generated monitor/SIL verification

1. Start from the project generated-code/AUTOSAR prerequisites.
2. Select top-model or Model-block SIL/PIL scope and configure logging/coverage/report options.
3. Run the project-approved SIL route using generated production source and the host execution contract.
4. Inspect logged outputs in Data Inspector.
5. If required, execute the model baseline and SIL leg with the same project stimulus and compare under explicit tolerances.
6. Keep generated source, host SIL process, execution result, equivalence result and coverage result separate.

Output: generated-code/SIL evidence.  
Exit/handoff: virtual runtime may proceed only from project integration inputs; SIL is not DEM/VECU evidence.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`.  
Authority: `[MW-PROC-2FB] [MW-MIL-SIL-2FB] [MW-TEST-2FB] [MW-COVERAGE-2FB]`

## Gate 5 — V2 runtime route

### DFM-017 — vVIRTUALtarget Integration / CANoe runtime

1. Assemble the configured/generated DEM/RTE/BSW and Application inputs.
2. Use the canonical vVIRTUALtarget **Integration** route to create the Integration SUT representation.
3. Build/package the SUT representation with project toolchain inputs.
4. In CANoe, load the SUT through the reviewed Configuration -> Components -> Add surface and apply the project diagnostic configuration.
5. Apply only project-authorized bounded fault/condition stimulus.
6. Observe tester-visible DTC behavior through the project diagnostic route.
7. If internal DEM debounce, event-memory or NvM state is required, use a project-specific instrumentation bridge; otherwise record an observability gap.

Output: package/load/configuration state, runtime response and independent execution evidence.  
Exit/handoff: V3 tester-facing research may continue even when internal DEM observability is unavailable.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`; actual execution is gated by project input.  
Authority: `[VECTOR-DEM-D922] [AUTOSAR-DCM-938] [AUTOSAR-SEM-4EFF]`

Do not substitute BSW Emulation, `vttsut` or an `Add VTT model` route for the Management ECU canonical Integration route. `[VECTOR-DEM-D922]`

## Gate 6 — V3 DiVa/CANoe test route

### DFM-018 — DiVa generation and CANoe execution

1. Select the project diagnostic description and project DTC rows in the DiVa DTC Test Configuration.
2. Configure only authorized stimulation, coverage model, expected status transitions and acceptance criteria.
3. Run `diva-make.exe diva.yaml [options]` and retain generation errors/output.
4. Import the generated project in CANoe through `Diagnostics & XCP | Test | Import DiVa Project`.
5. Ensure the project Assigned Bus or manual Diagnostics/ISO TP setup and ECU qualifier are consistent.
6. Select the generated Test Module/Test Unit; re-import/recompile where applicable.
7. Compile/execute the CANoe Test Configuration.
8. Capture Test Trace, execution result/verdict and report as separate artifacts.

Output: DiVa definition/generation artifact, CANoe imported test artifact, execution result/verdict and report.  
Exit/handoff: end-to-end closure can consume these artifacts only with project runtime and internal-state evidence as applicable.  
Availability: `PARTIAL_PROCEDURE_AVAILABLE`; actual generation/execution is gated by project input.  
Authority: `[VECTOR-DEM-D922] [AUTOSAR-DCM-938]`

The product-local DiVa generation route and product-local CANoe import/execution route remain valid independently. The reviewed documentation does not establish one universal cross-product Test Unit package/build/runtime contract. `[VECTOR-DEM-D922]`

## Gate 7 — end-to-end closure

### DFM-019 — evidence closure

1. Select one approved project requirement.
2. Link its project monitor design and result to the typed reporting contract.
3. Link generated configuration and runtime evidence to DEM event/status/DTC/memory states.
4. Link persistence evidence to the distinct NvM representation.
5. Link DCM response and FiM permission as consumer evidence, not as DEM ownership.
6. Link model/SIL and DiVa/CANoe definitions, execution results, verdicts, coverage and reports as separate evidence branches.
7. Record missing internal instrumentation and project artifacts as explicit gaps.
8. Do not declare closure until each edge has a project artifact and an exact authority tuple.

Output: typed end-to-end evidence bundle.  
Exit/handoff: Sol decides final maturity and the project decides acceptance.  
Availability: `WORKFLOW_ONLY`; project-specific closure is input/evidence required.  
Authority: `[AUTOSAR-SEM-4EFF] [AUTOSAR-OWN-938] [AUTOSAR-DCM-938] [AUTOSAR-FIM-938] [VECTOR-DEM-D922] [MW-PROC-2FB] [MW-TEST-2FB] [MW-MIL-SIL-2FB] [MW-COVERAGE-2FB]`

## Universal stop rules

- Never invent Event IDs/names, DTCs, mappings, algorithms, policies, thresholds, cycle meanings, conditions, memory settings, data contents, NvM IDs/layout/CRC, FiM relations, runnables/ports/callbacks, network addressing, variants, stimulus, expected transitions, test vectors, tolerances, acceptance criteria or actual project tool versions.
- Never treat configuration as generated configuration, generated configuration as runtime state, runtime response as internal state, or a verdict/report as coverage.
- A blocked project slice does not stop independent product-local research organization. The package records the blocker and continues the safe frontier.
