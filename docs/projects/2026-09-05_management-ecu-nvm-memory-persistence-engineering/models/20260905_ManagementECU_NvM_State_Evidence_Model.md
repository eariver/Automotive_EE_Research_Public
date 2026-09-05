# Management ECU NvM State & Evidence Model

Status: `LUNA_CURRENT_PACKAGE_COMPILE_PROPOSAL`  
Date: 2026-09-05

This model is a navigation contract for the current package. It records what an
observation can establish and what it cannot establish. It is not a project
runtime result.

## 1. Layered identity model

| Layer | Identity owned at the layer | Typical input/state | What an observation may establish | What it must not be promoted to |
|---|---|---|---|---|
| L0 | Application persistence semantics | Product data meaning and retention intent | The application requirement/design statement | An NvData contract, NvM block or physical address |
| L1 | NvData / ARXML contract | Ports, data elements, service/interface and mapping design | Contract shape and intended handoff | RTE execution or NvM configuration |
| L2 | RTE access | Generated/application access path | Access API/path exists when actually generated and inspected | NvM request completion or persistence |
| L3 | NvM logical NVRAM block | NV/RAM/optional ROM/Administrative objects and block-management policy | Logical block configuration/state at NvM | Fee/Ea logical block or physical storage |
| L4 | NvM synchronization | Permanent RAM, temporary RAM or explicit-sync mirror route | Synchronization route and callback observations | A second persistent NV copy or concurrency safety by assumption |
| L5 | NvM request state | Request acceptance, pending and `NVM_REQ_*` result | NvM software request state | Lower job state or durable persistence |
| L6 | MemIf dispatch | Selected memory-abstraction dispatch and `DeviceIndex` | Device-dispatch/status boundary when instrumented | Dataset index or Fee/Ea logical identity |
| L7 | Fee/Ea logical abstraction | Logical block processing, consistency and internal management | Fee/Ea processing/result boundary | NvM request result or physical address/layout |
| L8 | Fls/Eep physical device job | Read/write/erase/compare/blank-check job | Scoped physical-driver operation and `MEMIF_JOB_*` result | Fee/Ea logical consistency, NvM integrity or application validity |
| L9 | Persistent-media observation | Re-read of selected persistent data after completion | Observed bytes/value at the selected media interface | Reset/power-loss safety or semantic validity without the defined test |
| L10 | Reset / power-cycle / interruption | Reboot, power removal or interrupted-write scenario | Behavior under the executed scenario | General durability or all failure modes |
| L11 | Test verdict | Acceptance evaluation against defined criteria | Verdict for the defined test | Coverage or universal product claim |
| L12 | Coverage | Defined structural/functional/scenario coverage measure | Coverage metric for the defined scope | Verdict, proof or durability |

The layer separation is grounded in the exact-pinned AUTOSAR ownership,
synchronization, lower-memory and physical-verification entries plus the
focused NvM semantic review in the Reference Index.

## 2. Request and job state sequence

```text
configured intent
    -> NvM request accepted
    -> NVM_REQ_PENDING / equivalent NvM request state
    -> MemIf dispatch by configured DeviceIndex
    -> Fee or Ea logical processing
    -> Fls or Eep physical job accepted
    -> MEMIF_JOB_PENDING / terminal lower result
    -> Fee/Ea logical completion and upper notification
    -> NvM request result
    -> persistent-data re-read
    -> reset / power-cycle / interruption observation
    -> verdict
    -> coverage
```

This is a state/evidence ordering model, not a claim that every layer is called
synchronously in one stack frame. The exact-pinned AUTOSAR workflow authority
assigns asynchronous ownership and result propagation to the corresponding
layer.

### 2.1 Status vocabulary boundary

`NVM_REQ_*` is the NvM block-request vocabulary. `MEMIF_JOB_*` is the lower
memory-job vocabulary. They are not interchangeable:

```text
NVM_REQ_* != MEMIF_JOB_*
```

The following distinctions are mandatory:

- API request acceptance != NvM request completion;
- NvM request completion != lower-memory job completion;
- lower-memory job completion != persistent-media re-read;
- persistent-media re-read != reset/power-cycle evidence;
- software completion != durable persistence proof;
- test execution result != verdict != coverage.

`NVM_REQ_OK` and `MEMIF_JOB_OK` therefore receive the narrow evidence credit
"software request/job completion" only.

## 3. Logical block and synchronization model

The reviewed logical NVRAM-block model contains mandatory NV, RAM and
Administrative objects and an optional ROM object. Native, Redundant and Dataset
are NvM block-management types. They do not identify physical storage formats.

Synchronization routes remain distinct:

| Route | Working storage identity | Required project decision | Non-collapse rule |
|---|---|---|---|
| Implicit synchronization | Application/permanent RAM | Ownership and concurrency around asynchronous access | Permanent RAM is not temporary RAM or an explicit-sync mirror |
| Temporary/application route | Temporary RAM where the selected operation permits it | API and lifetime design | Temporary RAM is not a persistent NV copy |
| Explicit synchronization | One NvM-internal RAM mirror plus copy callbacks | Explicit-sync choice, callback identity and concurrency | Mirror is volatile synchronization storage, not another NV block |

The model does not select a management type, dataset index, RAM/NV/ROM object,
callback or synchronization route for the Management ECU.

## 4. Lower-memory branch model

```text
NvM logical request
        |
        v
MemIf uniform dispatch
       / \
      v   v
   Fee   Ea
    |     |
    v     v
   Fls   Eep
```

Fee/Fls and Ea/Eep are configuration-selected alternatives. The model does not
select one branch. The following are intentionally separate:

- NvM NVRAM block != Fee/Ea logical block;
- Fee/Ea logical block != Fls/Eep physical storage/address;
- MemIf `DeviceIndex` != NvM Dataset index;
- Fee/Ea internal-management state != `NVM_REQ_*`;
- `MEMIF_JOB_*` != `NVM_REQ_*`.

The exact Vector procedure review only establishes partition-level
Fee/Fls-versus-Ea wording and bounded product surfaces. It does not establish
the Management ECU backend, DeviceIndex mapping, logical-block mapping,
physical geometry or on-media metadata.

## 5. Invalidity, cancellation and recovery

Lower layers may expose invalid, inconsistent, failed or canceled states. Their
meaning is local to the owning layer:

| Observation | Safe interpretation | Not established |
|---|---|---|
| `MEMIF_BLOCK_INVALID` / inconsistent result | Lower logical data was reported unavailable or inconsistent according to that layer | NvM default/recovery policy or application invalidity |
| `MEMIF_JOB_FAILED` | Lower job failed | DET/DEM classification, NvM result or durable-media conclusion beyond the job |
| `MEMIF_JOB_CANCELED` / software idle after cancel | Software cancellation state was reached | Hardware quiescence or valid affected storage |
| Physical compare/blank-check success | The scoped physical operation passed its check | NvM CRC/static-ID policy, application semantic validity or safety sufficiency |
| NvM default/recovery outcome | Configured NvM recovery policy selected an outcome | A lower module owning the upper recovery policy |

The exact source workflow requires the owning upper policy to decide retry,
recovery and data validity. No retry, default, corruption, power-loss or
acceptance result is invented here.

## 6. Evidence promotion contract for NVM-018

NVM-018 can advance only when the project records the following as separate
evidence objects:

1. configured intent and exact project configuration;
2. generated BSW/RTE/configuration artifact;
3. compile result;
4. link/resulting executable or package;
5. runtime NvM request acceptance and request result;
6. lower MemIf/Fee/Ea/Fls/Eep status/job result;
7. RAM observation, when relevant;
8. persistent-data re-read at the selected persistence interface;
9. reset/power-cycle observation;
10. interrupted-write/power-loss observation;
11. test execution result;
12. verdict against supplied acceptance criteria;
13. coverage measure and scope.

Missing any layer keeps the corresponding claim bounded. In particular:

```text
generated artifact != compile/link result
NVM_REQ_OK != durable persistence
MEMIF_JOB_OK != power-loss safety
RAM observation != persistent-data re-read
test result != verdict != coverage
```

The current package contains no actual project execution evidence.

## 7. Authority tuples

The primary claims in this model are compiled from these exact tuples:

- `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d:docs/knowledge/concepts/memory-stack-layer-ownership.json#AUTOSAR-CP-4.4.0-CONCEPT-MEMORY-STACK-LAYER-OWNERSHIP`
- `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d:docs/knowledge/concepts/memif-dispatch-status-boundary.json#AUTOSAR-CP-4.4.0-CONCEPT-MEMIF-DISPATCH-STATUS-BOUNDARY`
- `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d:docs/knowledge/concepts/nvm-logical-block-ownership.json#AUTOSAR-CP-4.4.0-CONCEPT-NVM-LOGICAL-BLOCK-OWNERSHIP`
- `eariver/Research_AUTOSAR_CP_Documents@d021e2471b8c76efc6af43f66c17d7ead68821cc:docs/knowledge/management-ecu-nvm-autosar-semantic-depth.md`
- `eariver/Research_Vector_Documents@d7eb75af93ac82d155fe508681b7057802c3aa45:docs/knowledge/management-ecu-nvm-vector-procedure.md`

No claim in this model depends on a floating source.
