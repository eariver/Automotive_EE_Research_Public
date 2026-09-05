# Management ECU NvM Memory Persistence Project Scope

Date: 2026-09-05

## 1. Objective

Build a bounded, source-explicit engineering baseline for Management ECU persistent-memory behavior around AUTOSAR Classic NvM, preserving the full ownership chain from application-facing persistent data through lower memory abstraction and physical memory jobs.

This baseline is a decomposition and navigation artifact. It is not a claim that project-specific NvM configuration, generated BSW, target build, power-loss behavior or runtime persistence has been validated.

## 2. In scope

- Application persistence intent and NvData/RTE-facing handoff boundary where reviewed authority supports it.
- NvM logical NVRAM-block composition and management type semantics.
- RAM/NV/optional ROM/default/Administrative object distinctions.
- implicit versus explicit synchronization and RAM-mirror boundary.
- NvM read/write/default/recovery request semantics at reviewed depth.
- startup `ReadAll` and shutdown `WriteAll` lifecycle at reviewed depth.
- NvM request/result versus lower `MEMIF_JOB_*` semantics.
- NvM -> MemIf -> Fee/Ea -> Fls/Eep layer ownership.
- flash-emulation and EEPROM-abstraction alternative branches.
- lower-memory cancellation/error propagation and physical verification boundaries.
- configuration/validation/generation tooling only where exact reviewed tool authority exists.
- runtime persistence verification and evidence semantics.
- DEM/DCM/Application as consumers only where their persistence handoff matters to NvM; they are not folded into NvM ownership.

## 3. Out of scope for this baseline

- invention of Management ECU block identities or values;
- physical ECU memory-map design;
- wear/endurance budget without project inputs;
- universal power-loss-safe durability claims;
- complete DaVinci Configurator/MICROSAR procedure without reviewed product/release authority;
- generated-BSW acceptance without actual generation/build evidence;
- physical HIL/ECU test procedure as an assumed default;
- non-AUTOSAR persistent-storage architectures except as explicitly bounded comparison evidence;
- changing sibling DEM/diagnostics project authority.

## 4. Canonical ownership chain

At the current reviewed AUTOSAR boundary, use the following navigation model without collapsing adjacent layers:

Application persistent-data semantics
-> application/NvData/RTE-facing contract where applicable
-> NvM logical NVRAM-block management
-> MemIf uniform API and device dispatch
-> Fee or Ea logical-memory abstraction
-> Fls or Eep asynchronous physical-device job
-> physical memory

The Fee/Fls and Ea/Eep branches are alternatives selected by configuration; both are not mandatory in every ECU.

## 5. Mandatory task set

The first Luna baseline compilation must contain exactly the following 18 task identities and must not add a nineteenth task.

- `NVM-001` persistence scope, object model and ownership lifecycle
- `NVM-002` Application/NvData/RTE-to-NvM contract boundary
- `NVM-003` NvM logical NVRAM-block model and configuration semantics
- `NVM-004` RAM/NV/ROM-default/Administrative object relationships
- `NVM-005` startup and `ReadAll` lifecycle
- `NVM-006` explicit read request and asynchronous result lifecycle
- `NVM-007` explicit write request and asynchronous result lifecycle
- `NVM-008` shutdown and `WriteAll` lifecycle
- `NVM-009` restore-default/recovery flow
- `NVM-010` changed-state / RAM-block-status / write-on-change behavior, only where authority is explicit
- `NVM-011` integrity, CRC, redundant and dataset behavior, only where authority is explicit
- `NVM-012` write protection, locking and permanent-RAM behavior, only where authority is explicit
- `NVM-013` request status, job result, notification/callback and error handoff
- `NVM-014` NvM-to-MemIf dispatch/status boundary
- `NVM-015` MemIf-to-Fee/Ea branch and logical-consistency boundary
- `NVM-016` Fee/Ea-to-Fls/Eep device-job boundary
- `NVM-017` configuration, validation and generation tooling procedure availability
- `NVM-018` runtime persistence verification, durability claim and acceptance-evidence boundary

## 6. Hard semantic boundaries

The compilation must preserve all of the following:

1. Application persistence semantics != AUTOSAR contract != NvM configuration != generated implementation.
2. NvM NVRAM block != Fee/Ea logical block != physical flash/EEPROM block or sector.
3. NvM != MemIf != Fee != Ea != Fls != Eep.
4. MemIf DeviceIndex != NvM Dataset index.
5. `NVM_REQ_*` != `MEMIF_JOB_*`.
6. request accepted != asynchronous lower-memory job complete != durable physical persistence proven.
7. explicit-sync NvM RAM mirror is volatile synchronization storage, not another persistent NV copy.
8. Native/Redundant/Dataset are NvM management types, not lower-layer physical formats.
9. ReadAll != ReadBlock; WriteAll != WriteBlock.
10. lower-layer invalid/inconsistent detection does not transfer NvM default/recovery policy to Fee/Ea.
11. Fee is the flash-emulation branch over Fls; Ea is the EEPROM-abstraction branch over Eep.
12. configuration validation != code generation != compile != link != target/runtime validation.
13. write request success != power-loss-safe retention proof.
14. DEM/DTC, DID/RID and application persistence semantics are consumer/project semantics, not automatically NvM semantics.
15. test definition != execution result != verdict != coverage.

## 7. Project-owned inputs that must not be invented

- NvM block IDs and block count
- block lengths and alignment
- Native/Redundant/Dataset selection per block
- RAM block and ROM/default identities
- permanent versus temporary RAM policy
- explicit versus implicit synchronization policy
- CRC/static-ID/integrity configuration
- write protection/locking
- changed-state and write-on-change policy
- immediate/write-all policy
- queue sizes and priority behavior
- Fee versus Ea backend/device selection
- MemIf DeviceIndex identities
- Fee/Ea logical-block identities
- Fls/Eep device, address, sector/page and erase geometry
- flash wear/endurance assumptions and write-frequency budget
- startup/shutdown timing and EcuM/BswM integration policy
- retention and power-loss acceptance requirements
- DEM/DTC/DID/RID/application object mappings
- callback/runnable identities
- actual Vector/MICROSAR/DaVinci release and package variants
- compile/link/build baseline
- target or VECU execution environment
- test stimuli, fault injection, expected data, acceptance criteria and observed results

## 8. Authority use

Use only exact-pinned reviewed authority declared in `references/authority-pins.yaml` for technical claims during the first Luna compilation. Raw AUTOSAR PDFs, floating upstream heads, Web/current vendor documentation, generic model knowledge and sibling worklogs are not technical authority for that unit.

The reviewed AUTOSAR corpus already supports architecture/workflow statements through the lower memory stack. It does not by itself establish an exact project-specific DaVinci Configurator/MICROSAR GUI/CLI procedure.

## 9. Completion criteria for baseline compilation

The first Luna unit is complete when it produces exactly four allowlisted outputs containing:

- one current baseline row for every `NVM-001` through `NVM-018`;
- explicit exact-pinned provenance per supported row;
- a future research-gap decomposition for unsupported procedure depth;
- project-input blocking where project values are required;
- preserved semantic boundaries;
- a human-readable synthesis and completion checkpoint;
- validated task cardinality, classification counts and write allowlist;
- no invented Management ECU configuration values.

Unsupported tasks remain visible as bounded gaps. A missing vendor procedure is not to be converted into an inferred procedure from architecture knowledge.
