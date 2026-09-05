# Management ECU NvM / Memory Persistence
# Current Engineering Package Compilation Methodology

Status: `LUNA_CURRENT_PACKAGE_COMPILE_PROPOSAL`  
Date: 2026-09-05  
Scope: downstream compilation only; no new technical research

## 1. Mission and boundary

This package turns the already Sol-reviewed, exact-pinned AUTOSAR and Vector
authority into an engineering-navigation package for the Management ECU NvM /
Memory Persistence work. It compiles exactly 18 task identities, `NVM-001`
through `NVM-018`. It does not choose project configuration values, claim a
generated build, or claim runtime persistence.

The package is a Luna proposal. Sol determines final maturity after review at a
fixed head.

The following semantic chain is mandatory:

```text
Application persistence semantics
!= NvData / ARXML contract
!= RTE access
!= NvM configuration
!= generated BSW / configuration artifact
!= compiled / linked artifact
!= runtime NvM request state
!= lower-memory job state
!= persistent-media observation
!= reset / power-cycle evidence
!= interrupted-write / power-loss evidence
!= test verdict
!= coverage
```

The memory-stack ownership chain is likewise kept explicit:

```text
NvM != MemIf != Fee != Ea != Fls != Eep
NvM NVRAM block != Fee/Ea logical block != Fls/Eep physical storage/address
MemIf DeviceIndex != NvM Dataset index
NVM_REQ_* != MEMIF_JOB_*
```

These boundaries are supported by the exact-pinned AUTOSAR Reviewed Knowledge
catalog and focused NvM semantic review listed in the Reference Index.

## 2. Authority fence

Only the following technical authority pins are used:

| Authority | Exact pin | Use in this package |
|---|---|---|
| AUTOSAR reviewed base | `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d` | Logical NvM ownership, lifecycle, layer ownership, lower-memory workflows and evidence boundaries. |
| AUTOSAR NvM semantic depth | `eariver/Research_AUTOSAR_CP_Documents@d021e2471b8c76efc6af43f66c17d7ead68821cc` | Changed-state, immediate-priority, protection/lock, synchronization, integrity/recovery and request-result semantics. |
| Vector product procedure review | `eariver/Research_Vector_Documents@d7eb75af93ac82d155fe508681b7057802c3aa45` | DaVinci Configurator Classic 6.3.10 partial surfaces and exact generic validation/generation commands. |

The project-input authority is the fixed branch input file
`references/project/nvm-memory-persistence-project-input-baseline.yaml` at the
starting head. It remains `UNRESOLVED_PROJECT_INPUT`; it is not a source of
invented values.

Web pages, current vendor documentation, raw AUTOSAR PDFs, raw Vector HELP,
floating upstream heads, generic model knowledge and unreviewed observations
are not used as technical authority.

## 3. Compilation method

### 3.1 Normalize the task set

The two machine-readable matrices contain one row per task and no task outside
the required 18. Task identity is defined by the row's `task_id`; summary
counts do not repeat task identifiers in those matrices.

### 3.2 Project the reviewed authority into engineering fields

Each task row records:

- engineering intent;
- lifecycle phase;
- owner and layer;
- tool or product boundary;
- exact reviewed authority tuple;
- strongest reviewed workflow or procedure;
- project design and input required;
- input artifact/state;
- operation/activity;
- output artifact/state;
- exit condition;
- next handoff;
- proposed procedure availability;
- retained boundary or documentation negative;
- evidence needed for the next promotion.

The row describes the strongest safe frontier. It does not fill an unresolved
project field merely because a standard-side concept exists.

### 3.3 Keep state and evidence layers separate

The State & Evidence Model treats configuration, validation, generation,
compile/link, runtime request state, lower job state, physical observation,
reset/power-cycle behavior, interrupted-write behavior, verdict and coverage as
different evidence layers. `NVM_REQ_OK` and `MEMIF_JOB_OK` remain software
request/job completion evidence only.

### 3.4 Classify procedure availability

The proposal uses only the permitted labels:

| Label | Meaning in this compilation |
|---|---|
| `EXACT_PROCEDURE_AVAILABLE` | A complete exact reviewed procedure for the task boundary. None is claimed here. |
| `PARTIAL_PROCEDURE_AVAILABLE` | A bounded operation or product surface is reviewed, but the task is not complete object-by-object or project-specific. |
| `WORKFLOW_ONLY` | A reviewed ownership/control workflow is available, but no scoped product procedure is established. |
| `NO_EXPLICIT_PROCEDURE` | The exact authority preserves semantics/boundaries but does not expose an explicit operation sequence for the task. |
| `PROJECT_INPUT_REQUIRED` | The primary safe next step is blocked by an unresolved project value. This label is not used as the primary label when generic safe workflow can still be compiled. |
| `PROJECT_DESIGN_REQUIRED` | Project architecture/design must decide the route before it can be closed. |
| `EXECUTION_EVIDENCE_REQUIRED` | The task cannot be promoted without actual project build/runtime/persistence evidence. |

`PARTIAL_PROCEDURE_AVAILABLE` does not mean that DaVinci Configurator has a
complete NvM procedure. In particular, the Memory Editor / Memory Blocks Editor,
the Event Memory Blocks Assistant and partition-level Fee/Fls-versus-Ea wording
remain bounded surfaces only. The generic `dvcfg-b project validate`,
`project generate` and `project generate-schema` commands are exact generic
project procedures, not complete NvM-specific diagnostic or runtime procedures.

## 4. Current availability proposal

The non-overlapping primary availability counts are:

| Proposed availability | Count |
|---|---:|
| `EXACT_PROCEDURE_AVAILABLE` | 0 |
| `PARTIAL_PROCEDURE_AVAILABLE` | 10 |
| `WORKFLOW_ONLY` | 5 |
| `NO_EXPLICIT_PROCEDURE` | 1 |
| `PROJECT_INPUT_REQUIRED` | 0 |
| `PROJECT_DESIGN_REQUIRED` | 1 |
| `EXECUTION_EVIDENCE_REQUIRED` | 1 |
| **Total** | **18** |

The task-level allocation is recorded in both machine-readable matrices and in
the Compilation Report. Project-input and project-design blockers are
orthogonal to this primary availability value; the unresolved project baseline
therefore remains visible for all affected rows.

## 5. Non-inference policy

The compilation never invents or defaults:

- NvM block IDs, sizes, counts or management types;
- Dataset count/index policy;
- RAM, NV, ROM/default or Administrative identities;
- explicit/implicit synchronization choice or callbacks;
- CRC, Static Block ID, write-verification or retry policy;
- changed-state, write-on-change, immediate priority or queue policy;
- write protection, write-once or block-lock policy;
- MemIf `DeviceIndex`;
- Fee/Ea backend, logical block identity or physical address/geometry;
- endurance, write-frequency, startup/shutdown timing or retention policy;
- runtime stimulus, expected data, reset/power-loss outcome, verdict or coverage.

`write-on-change` is retained only as a project-facing umbrella. Changed state,
CRC comparison, `WriteAll` selection, explicit `WriteBlock` and job priority are
separate mechanisms. Immediate priority is retained only where the reviewed
source explicitly defines it; no generic deferred counterpart is added.

Write protection, write once and block lock remain separate. Permanent RAM,
temporary RAM and an explicit-synchronization mirror remain separate. Native,
Redundant and Dataset, along with CRC, Static Block ID, write verification,
default/recovery and retry behavior, remain conditional project decisions.

## 6. Promotion rule

A task is promotable only when the next evidence layer exists at the owning
boundary. A generated file does not prove compilation or link. A successful
software request or lower job does not prove durable persistence. A physical
compare does not prove NvM integrity or application-data validity. A test result
does not automatically provide a verdict or coverage claim.

NVM-002 remains project-design/input bound until an actual Application/NvData/RTE
mapping is supplied. NVM-018 remains execution-evidence bound until the project
provides the configured intent, generated artifact, compile/link result,
runtime request, lower job, persistent-data re-read, reset/power-cycle,
interrupted-write/power-loss evidence, verdict and coverage as separate layers.

## 7. Package navigation

- The Step-by-Step Guide is the ordered engineering handoff.
- The Tool / Task / Reference Matrix is the single detailed task catalog.
- The State & Evidence Model defines state ownership and non-collapse rules.
- The Execution Reference Guide defines the evidence capture sequence for later project execution.
- The Procedure Coverage Matrix is the compact task-by-task procedure/evidence view.
- The Reference Index is the exact source tuple catalog.
- The Compilation Report and terminal checkpoint record this Luna proposal and validation posture.

No upstream repository, `docs/knowledge/**`, authority pin, project-input
baseline, plan, instruction, prompt or sibling project is changed by this
package.
