# Management ECU Crypto State and Evidence Model

Date: `2026-09-06`

Status: `VALUE_FREE_STATE_MODEL`

## 1. Principle

The following are distinct states or evidence planes. No automatic transition is implied by the presence of an earlier artifact.

| State / evidence plane | Meaning retained | Does not prove |
|---|---|---|
| `configured/reference` | A semantic or configuration definition/reference is selected in an accepted design artifact. | Population, validity, availability, use, persistence, or runtime success. |
| `provisioned/populated` | A separately evidenced lifecycle activity has populated a key or related state. | Validity, availability, selection, durable storage, or consumer acceptance. |
| `valid` | The applicable Crypto key validity state is established by the authorized operation. | Persistence, availability, actual selection, use, or security acceptance. |
| `available` | The applicable layer reports an available state. | Non-empty content, successful use, durability, or consumer acceptance. |
| `selected/referenced` | A configured operation or consumer refers to the symbolic key/object. | That the operation executed or used the referenced object successfully. |
| `actually used` | Runtime evidence shows the selected object was used by an operation. | Consumer acceptance, performance requirement satisfaction, verdict, or coverage. |
| `persisted` | Separate storage/durability evidence establishes the persistence claim. | Validity, later availability, power-loss safety, or application correctness. |
| `cryptographic result` | A service/job/driver operation reports its own result. | Consumer acceptance, diagnostic authorization, test verdict, or coverage. |
| `consumer acceptance` | The owning SW-C, SecOC, DCM, or other consumer accepts the result under its own criteria. | Test verdict or coverage. |
| `test verdict` | An authorized test process records a pass/fail/other verdict. | Requirement completeness or coverage by itself. |
| `coverage` | A separately defined coverage method reports its scope/result. | Correctness, security acceptance, or runtime behavior outside the measured scope. |

## 2. Non-automatic transition model

```text
configured/reference
    -[separate population evidence]-> provisioned/populated
    -[separate validity evidence]-> valid
    -[separate availability evidence]-> available
    -[separate operation/runtime evidence]-> selected/referenced / actually used
    -[separate storage/durability evidence]-> persisted
    -[separate service evidence]-> cryptographic result
    -[consumer-owned criteria]-> consumer acceptance
    -[test process]-> test verdict
    -[coverage method]-> coverage
```

The arrows identify possible evidence relationships, not claims that the transitions exist for the current Management ECU.

## 3. Identity boundaries

```text
CSM service request != Crypto Job != configured primitive
CsmKey != CryIfKey != CryptoKey != CryptoKeyType != CryptoKeyElement
CryIf channel != Crypto Driver Object
KeyM certificate status != consumer authorization
DCM Authentication 0x29 != SecurityAccess 0x27 != universal diagnostic authorization
random/random-seed API != entropy source != entropy quality != seed provenance != randomness certification
```

## 4. Evidence ownership

| Evidence layer | Owning concern | Current package state |
|---|---|---|
| semantic model | AUTOSAR reviewed authority | Available at pinned generic depth |
| product procedure | Vector/MICROSAR reviewed authority | Fixed negative/supporting-workflow boundary |
| project design/input | Management ECU requirements/design | Unresolved; no concrete consumer adopted |
| vendor/hardware realization | Crypto Driver/HSM/SHE/vendor | Conditional or explicit gap; not researched here |
| artifact/build | generated configuration and compile/link | Not executed or inspected |
| runtime | deployed/virtual/physical execution | Not executed |
| acceptance | consumer-specific criteria | Not supplied |
| verdict/coverage | authorized verification process | Not supplied |

## 5. Required negative rules

- Configuration is not validation, generation, compile/link, or runtime execution.
- A generated artifact is not proof of driver behavior, persistence, acceptance, verdict, or coverage.
- A successful Crypto request/job is not durable persistence or consumer acceptance.
- A certificate status is not diagnostic or application authorization.
- Generic Vector support is not Crypto-specific procedure evidence.
- No state is assigned a concrete project value in this package.
