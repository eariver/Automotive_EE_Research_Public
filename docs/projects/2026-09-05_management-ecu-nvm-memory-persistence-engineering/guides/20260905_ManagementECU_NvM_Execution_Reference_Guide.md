# Management ECU NvM / Memory Persistence
# Execution Reference Guide

Status: `LUNA_CURRENT_PACKAGE_COMPILE_PROPOSAL`  
Date: 2026-09-05

This guide defines the evidence to collect when the project later executes the
NvM package. It is not an execution report and contains no Management ECU
configuration value, result, verdict or coverage claim.

## 1. Preconditions

Execution must not begin as a claim of project closure until the project has
supplied the applicable inputs from
`references/project/nvm-memory-persistence-project-input-baseline.yaml`:

- application/NvData/RTE ownership and mapping;
- NvM block identities, lengths, management type and synchronization;
- integrity, default/recovery, change/write and protection policy;
- lifecycle actions and timing;
- MemIf `DeviceIndex`, Fee/Ea branch and logical mapping;
- Fls/Eep device, physical layout and endurance assumptions;
- toolchain, compiler/linker, target/VECU and test runner;
- stimuli, expected data, reset/power-loss scenarios, acceptance criteria and
  coverage definition.

Any missing value remains `PROJECT_INPUT_REQUIRED` or
`PROJECT_DESIGN_REQUIRED`; do not replace it with a default.

## 2. Evidence object schema

Record one evidence object per observation or artifact. A minimum record is:

```yaml
evidence_id: <project-assigned-id>
task_id: <one-of-NVM-001-through-NVM-018>
evidence_layer: <intent|contract|configuration|validation|generation|build|link|nvm_request|lower_job|media_reread|reset_power_cycle|interruption|execution_result|verdict|coverage>
owner_layer: <owning-project-layer>
artifact_or_observation: <exact path, log, trace or observation reference>
source_or_input: <project input or exact reviewed authority tuple>
scope: <block, branch, scenario or test scope>
result: <recorded value, status or reference; never inferred>
timestamp_or_run: <project run identity>
predecessor_evidence: [<evidence ids>]
promotion_claim: <narrow claim supported by this object>
not_proven: <adjacent claim intentionally not made>
```

The `task_id` field must be selected from the fixed 18-task set. A record with
no project run identity is not execution evidence.

## 3. Ordered execution trace

### 3.1 Intent and contract

Capture the approved persistence intent and the Application/NvData/RTE contract
separately. Record the owning SWC/BSW consumer, data element/port and runnable
or callback only when supplied by the project.

Do not use an NvM block ID as a substitute for application meaning or an ARXML
contract.

### 3.2 Configuration

Capture the configured NvM logical block, object identities, synchronization,
management type, integrity, change/write, protection and lower-memory references
as project artifacts. Keep Native/Redundant/Dataset and all optional mechanisms
conditional.

The following identities must remain distinct:

```text
RAM block != NV block != optional ROM/default block != Administrative block
permanent RAM != temporary RAM != explicit-sync mirror
changed state != CRC comparison != WriteAll selection != explicit WriteBlock != job priority
write protection != write once != block lock
```

### 3.3 Generic project validation and generation

For the reviewed DaVinci Configurator Classic 6.3.10 generic project boundary,
record the exact command, project path, BSW package, tool version, exit status,
logs and output directory for:

```shell
dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
```

These commands are exact generic product procedures. Their success supports a
generic validation/generation claim only. It does not close the NvM-specific
object/diagnostic mapping or prove compile, link, runtime or persistence.

### 3.4 Compile and link

Capture the actual compiler/linker command or build-run identity, input
configuration/generated artifacts, warnings/errors, output binary/package,
symbol/map information and exit status. Do not substitute a generated folder
for a compiled or linked artifact.

### 3.5 Runtime NvM request

Capture the request API, block identity, request acceptance time, pending state,
terminal NvM result and any callback/notification. Record `NVM_REQ_*` in the NvM
layer only.

`NVM_REQ_OK` is software request completion evidence. It is not durable-media,
power-loss, application-validity, verdict or coverage evidence.

### 3.6 Lower-memory job

Capture MemIf dispatch, `DeviceIndex` (only if the project supplies it), selected
Fee/Ea branch, lower logical result, Fls/Eep physical job, `MEMIF_JOB_*` result,
callbacks and relevant error/reporting surface.

Keep the following separate:

```text
NVM_REQ_* != MEMIF_JOB_*
NvM NVRAM block != Fee/Ea logical block
Fee/Ea logical block != Fls/Eep physical storage/address
```

The product-local word `device` and the `Ifp.json` Fee/Nvm example must not be
used to invent a project `MemIf DeviceIndex` or backend.

### 3.7 Persistent-data re-read

After the owning abstraction reports the relevant operation complete, capture a
separate re-read at the selected persistence interface. Record the exact scope,
data identity, read path, observed value/bytes and comparison rule.

A RAM observation is not a persistent-media re-read. A physical compare is
limited to the physical operation and range it checked.

### 3.8 Reset, power-cycle and interrupted operation

Execute only project-defined scenarios. Record power/reset stimulus, interruption
point, recovery path, pre/post values, lower status, NvM status and artifacts.

Software idle or `MEMIF_JOB_CANCELED` after a cancel does not prove that hardware
is quiescent or affected storage is valid. An observed result for one scenario
does not generalize to all power-loss modes.

### 3.9 Verdict and coverage

Evaluate the execution result against project-supplied acceptance criteria and
record verdict separately. Record the coverage definition, denominator,
achieved measure and exclusions separately.

```text
test definition != execution result != verdict != coverage
```

## 4. Branch-specific trace templates

### Fee/Fls branch

```text
NvM request
 -> MemIf dispatch
 -> Fee logical operation
 -> Fee_MainFunction/internal management
 -> Fls read/write/erase/compare/blank-check as required
 -> Fls completion/error notification
 -> Fee logical completion
 -> NvM result/notification
 -> persistent re-read
```

Do not infer Fee metadata, on-media format or a universal reorganization/garbage
collection sequence.

### Ea/Eep branch

```text
NvM request
 -> MemIf dispatch
 -> Ea logical operation
 -> Ea_MainFunction/internal management
 -> Eep read/write/erase/compare as required
 -> Eep completion/error callback
 -> Ea logical completion
 -> NvM result/notification
 -> persistent re-read
```

Do not infer a physical address encoding or external-device behavior not present
in the selected project authority.

## 5. Promotion gates

| Promotion | Minimum evidence | Still not proved automatically |
|---|---|---|
| Intent -> contract | Approved application/NvData/RTE mapping | NvM block configuration |
| Contract -> configuration | Project block/object/sync design | Generated artifact or runtime behavior |
| Configuration -> generated artifact | Validated project and generator output | Compile/link or runtime |
| Generated -> compiled/linked | Build inputs, logs, binary/package and success | Runtime request or persistence |
| NvM request -> lower job | Correlated request, dispatch and lower result | Persistent re-read or power-loss behavior |
| Lower job -> persistence observation | Re-read at the selected persistence interface | General durability or application validity |
| Scenario -> verdict | Defined criteria and reproducible execution result | Coverage unless separately measured |
| Verdict -> coverage claim | Explicit coverage definition and measure | A universal test or safety claim |

## 6. Stop conditions

Stop the claim at the narrowest missing layer when:

- a project value is missing;
- `MemIf DeviceIndex`, backend or physical layout is not supplied;
- the exact product object/diagnostic procedure is not documented;
- the build or link result is absent;
- only request/job success is available;
- the persistent re-read is absent;
- reset/power-loss/interruption evidence is absent;
- verdict criteria or coverage definition is absent.

The current Luna package reaches the reference/checklist frontier only. It
contains no project execution result and no durability, power-loss, verdict or
coverage claim.
