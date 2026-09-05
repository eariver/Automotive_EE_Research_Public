# Management ECU NvM / Memory Persistence
# Step-by-Step Engineering Guide

Status: `LUNA_CURRENT_PACKAGE_COMPILE_PROPOSAL`  
Date: 2026-09-05

This guide is the ordered handoff from project intent to later execution
evidence. It does not assign Management ECU values and it does not report that
any step has already been executed on a target.

## 0. Freeze the authority and project-input boundary

Use only the exact pins in the Reference Index:

- AUTOSAR base: `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d`;
- focused NvM semantic depth: `eariver/Research_AUTOSAR_CP_Documents@d021e2471b8c76efc6af43f66c17d7ead68821cc`;
- Vector procedure: `eariver/Research_Vector_Documents@d7eb75af93ac82d155fe508681b7057802c3aa45`.

Read the project-input baseline before accepting any project field. Its status
is `UNRESOLVED_PROJECT_INPUT`. Do not derive a value from a standard term, an
example, a GUI label, a sibling ECU or a lower-layer branch.

## 1. Establish the persistence inventory — NVM-001

### Input

Project persistence intent, consumer ownership and the lifecycle context.

### Activity

Define the persistence scope at the logical NvM ownership boundary. Identify
which application or BSW consumer owns the meaning of a persistent datum, but do
not assign a block identifier, physical location or diagnostic ownership.

Use the reviewed logical NVRAM-block and memory-stack ownership model. Keep
BswM's lifecycle action context separate from NvM's multi-block execution and
result handling.

### Output and exit

Output is a persistence inventory and ownership boundary with unresolved values
explicitly marked. Exit when the project has an approved inventory or accepts a
generic-only handoff to the application contract and logical-block design.

### Handoff

Continue to the application/NvData/RTE boundary and logical NvM block model.

## 2. Define the application contract — NVM-002

### Input

Actual Application SWC ownership, NvData or service-port contract, RTE access,
runnable/callback mapping and read/write semantics.

### Activity

Map the application persistence intent to a project-approved NvData/ARXML/RTE
contract. Record the intended handoff to NvM without treating the mapping as an
NvM block configuration.

### Output and exit

Output is the project contract and an explicit handoff record. No SWC, port,
data element, runnable or callback is invented. This step cannot close from
generic AUTOSAR layering alone and remains `PROJECT_DESIGN_REQUIRED`.

### Handoff

Only after approval, proceed to block configuration. Keep application
semantics, contract, RTE access and NvM configuration as separate artifacts.

## 3. Define the NvM logical block — NVM-003 and NVM-004

### Input

Approved persistence inventory and project choices for block IDs, lengths,
management type, RAM/NV/ROM/default/Administrative objects and synchronization.

### Activity

Model mandatory NV, RAM and Administrative objects and the optional ROM object.
Treat Native, Redundant and Dataset as conditional NvM management types. Choose
implicit synchronization, temporary RAM or explicit synchronization only from
project design. If explicit synchronization is selected, model the NvM-internal
RAM mirror and copy callbacks as transient synchronization storage.

Where the DaVinci Configurator Classic 6.3.10 product surface is used, the
reviewed partial route is:

1. enter the Memory / Memory Blocks Editor;
2. use the product-local `Add Memory Partition` route and select a device;
3. use the product-local `Add Memory Block` route and select a partition;
4. treat the surface as a block/partition overview and bounded configuration
   surface only.

This route does not close Native/Redundant/Dataset, object identities, CRC,
callbacks, priorities, protection or lower-memory mapping.

### Output and exit

Output is the logical NvM configuration model and an unresolved-value list. Do
not map an NvM block to a Fee/Ea logical block or physical address at this step.

### Handoff

Pass the approved model to startup/shutdown lifecycle, request, integrity and
lower-stack slices.

## 4. Define startup and shutdown lifecycle — NVM-005 and NVM-008

### Input

Project BswM/EcuM mode handoff, participating blocks, timing, shutdown budget,
retention requirement and completion policy.

### Activity

Use the reviewed lifecycle workflow:

```text
startup:  BswM action -> NvM_ReadAll -> asynchronous NvM processing/results
shutdown: BswM action -> NvM_WriteAll -> asynchronous NvM processing/results
```

NvM owns multi-block execution, ordering, processing and result handling. The
workflow does not supply the Management ECU's mode timing or participating
block set.

### Output and exit

Output is a project lifecycle action design and a timing/observability plan.
Exit only when the project supplies the lifecycle policy; do not convert
`ReadAll` or `WriteAll` into a durability claim.

## 5. Define explicit request paths — NVM-006 and NVM-007

### Input

Project choice of explicit `ReadBlock`/`WriteBlock`, target block, RAM route,
callback/notification policy and lower-stack branch.

### Activity

For a read, track request acceptance, pending/result state, lower dispatch and
configured recovery handling. For a write, trace the logical request through
MemIf to the selected Fee/Ea branch and then the selected Fls/Eep device jobs.

Keep these separate:

```text
request acceptance
!= NvM request completion
!= lower job completion
!= persistent-data re-read
```

For Fee/Fls, use the reviewed logical-write to asynchronous Fls job trace. For
Ea/Eep, use the reviewed logical-write to asynchronous Eep job trace. These are
alternative routes; the package does not select either route.

### Output and exit

Output is a request/state trace template. Exit when a project block, API route,
backend branch and expected evidence set are supplied. `NVM_REQ_OK` or
`MEMIF_JOB_OK` alone does not close the step.

## 6. Define recovery and integrity choices — NVM-009 and NVM-011

### Input

Project corruption/invalidity scenarios and choices for management type, CRC,
Static Block ID, write verification, ROM/default/init callback, retries and
recovery.

### Activity

Keep lower invalid/inconsistent reporting separate from NvM recovery/default
policy. Apply physical verification only to the physical operation it actually
checks. Do not select Native, Redundant, Dataset, CRC or defaults universally.

### Output and exit

Output is a conditional decision matrix and an evidence plan that distinguishes
lower result, NvM result and application-data state.

## 7. Define change, write and access policies — NVM-010 and NVM-012

### Input

Project write policy, changed-state ownership, priority/queue intent, RAM
ownership, protection/lock design and callback/concurrency design.

### Activity

Keep the following mechanisms separate:

```text
changed state
!= CRC comparison
!= WriteAll selection
!= explicit WriteBlock
!= job priority
```

The reviewed source explicitly supports `NvM_SetRamBlockStatus`,
`NvMSelectBlockForWriteAll`, CRC comparison mechanisms and priority-based
processing including source-defined immediate priority. `write-on-change` is a
project-facing umbrella only; no generic deferred counterpart is created.

Also keep these separate:

```text
write protection != write once != block lock
permanent RAM != temporary RAM != explicit-sync mirror
```

The exact Vector procedure review does not provide a complete product-local
operation sequence for these choices. Keep the product-procedure gap visible.

### Output and exit

Output is a project policy/design record with unresolved choices marked. No
threshold, timing, queue size, lock state or callback is supplied by this
package.

## 8. Define result and notification handling — NVM-013

### Input

API request records, NvM result policy, MemIf/lower-job observation, callback
mapping and diagnostic/error reporting design.

### Activity

Record each vocabulary at its owner:

- NvM `NVM_REQ_*` request state;
- MemIf `MEMIF_*` status/job result;
- Fee/Ea invalid/inconsistent/internal-management state;
- Fls/Eep physical job result;
- callback/notification;
- DET/DEM or other diagnostic classification, only where project-mapped.

Do not merge a failed lower job with a DET/DEM classification, and do not treat
a callback as proof of durable media or application validity.

## 9. Resolve the lower-memory route — NVM-014 through NVM-016

### Input

Project `MemIf DeviceIndex`, configured Fee/Ea instance, logical block IDs,
Fls/Eep device, physical addresses, sector/page/erase geometry and endurance
assumptions.

### Activity

Use the reviewed ownership path:

```text
NvM -> MemIf(DeviceIndex) -> Fee or Ea -> Fls or Eep -> physical memory
```

Treat Fee/Fls and Ea/Eep as alternatives. The Vector product surface provides
only bounded partition/device/block wording and the product-local `device`
label is not promoted to `MemIf DeviceIndex`. The `Ifp.json` Fee/Nvm mapping is
an example-only input artifact and must not choose the Management ECU backend.

For the selected route, correlate abstraction processing, lower main-function
activity, physical job acceptance, physical completion, callbacks and any
re-read. Keep logical consistency, physical verification and NvM result
separate.

### Output and exit

Output is a project-selected lower-stack mapping and trace plan. No current
project value is assigned in this package.

## 10. Validate and generate the project boundary — NVM-017

### Input

An actual DaVinci Configurator Classic 6.3.10 project, BSW package, selected
configuration and project toolchain baseline.

### Activity

The exact reviewed generic product commands are:

```shell
dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
```

Use the commands only for the generic project boundary. Record command,
version, inputs, output folder, exit status and logs. Do not represent a
successful generation as an NvM-specific diagnostic/constraint pass or a
compile/link/runtime result.

### Output and exit

Output is a validated/generated artifact record. The NvM object-by-object
configuration procedure, diagnostic remediation and generated-to-runtime
mapping remain bounded by the reviewed Vector authority.

## 11. Execute and verify persistence — NVM-018

### Input

Configured intent, generated artifact, compiler/linker baseline, target or
virtual environment, runtime stimulus, initial data, reset/power-loss scenarios,
acceptance criteria and coverage definition.

### Activity

Capture the following independently:

```text
configured intent
-> generated artifact
-> compile/link result
-> runtime NvM request
-> lower-memory job
-> persistent-data re-read
-> reset/power-cycle
-> interrupted-write/power-loss
-> verdict
-> coverage
```

The Execution Reference Guide supplies the record shape. A request/job success,
generated artifact or physical compare does not close the durable-persistence,
power-loss, application-validity, verdict or coverage claim.

### Output and exit

Output is an evidence package with separate layers and explicit scope. Exit
requires actual project execution evidence; this current package supplies none.

## 12. Final handoff

The current package is ready for Sol fixed-head review. Sol may finalize
procedure maturity, but no later review should erase the retained project-input,
documentation or execution boundaries. No upstream source is modified and no
new research is opened by this guide.
