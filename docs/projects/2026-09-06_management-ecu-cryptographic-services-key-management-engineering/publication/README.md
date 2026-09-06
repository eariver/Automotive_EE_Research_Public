# Publication — Management ECU Cryptographic Services & Key Management Engineering

Date: 2026-09-07
Status: `SOL_REVIEWED_STAGED`

## Accepted private source

- Repository: `eariver/Automotive_EE_Engineering_Knowledge`
- Sol review branch: `work/sol-management-ecu-crypto-current-package-review-20260906`
- Accepted source HEAD: `adbeef4d3916d76e23b6b3c866543796af522090`
- Luna current-package terminal reviewed: `67ef5893915f3c7998964938d78226ed04b6c6a6`
- Luna current-package starting SHA: `23581e4da3fded3ebef7648cb176507fc2cc451d`
- Sol verdict: `MANAGEMENT_ECU_CRYPTO_CURRENT_PACKAGE_SOL_REVIEW_PASS`

The private current package contains exactly `CRY-001` through `CRY-018` and was independently fixed-head reviewed before publication staging.

## Public staging branch

- Repository: `eariver/Automotive_EE_Research_Public`
- Branch: `publish/management-ecu-cryptographic-services-key-management-engineering-20260906`
- Public base `main`: `183d9dc0ab120484e4018e530a33e5b291bd7baa`
- `main` merged: **false**

Publication staging does not modify public `main`. Merge requires separate explicit human approval.

## Current maturity

Primary task-level procedure availability:

- `WORKFLOW_ONLY`: 1
- `NO_EXPLICIT_REVIEWED_PROCEDURE`: 14
- `OUTSIDE_AUTHORIZED_PRODUCT_SCOPE`: 3
- total: 18

No task is promoted to exact, partial, or surface-only Crypto-specific product procedure maturity.

The following generic DaVinci Configurator Classic procedures remain exact supporting workflow only:

```text
dvcfg-b project validate
dvcfg-b project generate
dvcfg-b project generate-schema
```

Generic CLI status/exit-code and generic CI workflow context are also supporting context. None establishes a Crypto-specific configuration, generated artifact, build, HSM, provisioning, or runtime procedure.

## Remaining blockers

- `PROJECT_INPUT_REQUIRED`: 6 tasks — `CRY-001`, `CRY-011`, `CRY-012`, `CRY-013`, `CRY-017`, `CRY-018`.
- `PROJECT_DESIGN_REQUIRED`: 12 tasks — `CRY-002` through `CRY-010`, plus `CRY-014`, `CRY-015`, `CRY-016`.
- `VENDOR_HARDWARE_AUTHORITY_REQUIRED`: `CRY-016` only at the current baseline. Vendor/HSM authority for `CRY-017` and `CRY-018` remains conditional on concrete project realization.
- `EXECUTION_EVIDENCE_REQUIRED`: `CRY-018`.

No specific Crypto consumer, Authentication `0x29` adoption, SecOC adoption, KeyM certificate use, algorithm/mode/key role, key hierarchy, queue/priority, HSM/SHE topology, entropy source, provisioning backend/protocol, persistence realization, target/runtime result, acceptance threshold, verdict, or coverage value is introduced by publication.

## Reviewed authority

- AUTOSAR Crypto semantic authority:
  `eariver/Research_AUTOSAR_CP_Documents@9903efc816f8589d865e36f26f7fe44fb27c62b9`
  - Reviewed Knowledge: `docs/knowledge/management-ecu-crypto-autosar-semantic-depth.md`
  - canonical blob: `4cb5eaba08ee7cba5d89bef67ee0174bd31997b7`
- Vector/MICROSAR Crypto procedure authority:
  `eariver/Research_Vector_Documents@aab6c3f9ad60493b6176ff0ad9b7f25dcc37b1fe`
  - Reviewed Knowledge: `docs/knowledge/management-ecu-crypto-vector-procedure.md`

Generic AUTOSAR CSM/CryIf/Crypto Driver/KeyM semantic research is closed at the reviewed scope. Vector Crypto-specific product procedure research is closed at the reviewed DaVinci Configurator Classic 6.3.10 user-manual scope: six reviewed slices have no explicit reviewed procedure and two slices are outside the authorized product scope.

## Publication bundle

The staged bundle contains 13 source-derived engineering artifacts plus 2 publication metadata files:

1. project README
2. Project Scope
3. Development Methodology
4. Step-by-Step Guide
5. Tool / Task / Reference Matrix
6. State & Evidence Model
7. Execution Reference Guide
8. Procedure Coverage Matrix
9. Reference Index
10. Current Package Compilation Report
11. Sol fixed-head review
12. authority pins
13. publication-safe unresolved project-input baseline
14. this Publication README
15. `publication-plan.yaml`

The two YAML matrices are semantically reconstructed from the accepted private fixed head because cross-repository Git blob reuse is not supported. Public Git blob IDs are therefore not private-byte identity claims. Publication validation checks task cardinality, authority tuples, classifications, blockers, handoffs and retained boundaries.

## Retained boundaries

- CSM service request != Crypto Job != configured primitive
- CsmKey != CryIfKey != CryptoKey != CryptoKeyType != CryptoKeyElement
- CryIf channel != Crypto Driver Object
- configured/reference != provisioned/populated != valid != available != selected/referenced != actually used != persisted
- KeyM certificate status != consumer authorization
- DCM Authentication `0x29` != SecurityAccess `0x27` != universal diagnostic authorization
- random/random-seed API != entropy source != entropy quality != seed provenance != randomness certification
- AUTOSAR semantics != Vector/MICROSAR realization != Crypto Driver/HSM vendor realization != project design != runtime evidence
- configuration != validation != generation != compile/link != runtime execution
- cryptographic result != consumer acceptance != test verdict != coverage

Authentication `0x29`, SecOC, KeyM certificate use, HSM/SHE, hardware-backed Crypto, provisioning realization and entropy qualification remain conditional/project-owned and are not adopted merely by publication.

## Secret-material guard

Publication contains no symmetric/private key, certificate private material, seed/entropy value, credential, password, token, OEM secret, key-element value, HSM slot content, or proprietary derivation material. Only symbolic/value-free engineering metadata is admissible.

## Excluded from publication

- Luna prompts, plans, instructions, observations and worklogs
- Luna baseline/current-package terminal checkpoints and internal Sol baseline checkpoint
- historical task baseline and research-gap backlog not required for current public consumption
- raw AUTOSAR/Vector source documents
- upstream canonical `docs/knowledge/**` bodies
- confidential/project-specific actual Crypto values
- secret/private key or provisioning material
- invented runtime results, verdicts or coverage

This branch is a publication staging branch. Public `main` remains unchanged until separately authorized.
