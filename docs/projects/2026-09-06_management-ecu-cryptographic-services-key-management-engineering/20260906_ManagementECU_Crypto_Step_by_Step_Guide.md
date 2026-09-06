# Management ECU Crypto Step-by-Step Guide

Date: `2026-09-06`

This guide executes the accepted current-package task registry in order. It is a compilation guide, not a new research or runtime procedure. Every step stops at the authority frontier stated below it.

## Ordered task sequence

### 1. `CRY-001` — scope, consumer, ownership

Record the project/security consumer question, owning layer, Consumption Layer anchor, and UDS responsibility boundary. Do not select a consumer or security policy. Handoff: project input/design authority.

### 2. `CRY-002` — service, job, primitive

Create separate semantic references for the CSM service request, Crypto Job, and configured primitive. Do not select an algorithm or collapse these identities. Handoff: ECUC/project design.

### 3. `CRY-003` — processing and scheduling boundary

Record synchronous/asynchronous processing, queue, priority, callback, cancellation, and START/UPDATE/FINISH as distinct dimensions. Do not infer timing or observed execution. Handoff: project processing design.

### 4. `CRY-004` — CSM to CryIf channel

Register the CSM-to-CryIf channel relation as a value-free reference. Do not invent a channel identifier or equate it with a driver object. Handoff: ECUC/product mapping if adopted.

### 5. `CRY-005` — CryIf to Crypto Driver Object

Register the CryIf channel-to-driver-object boundary. Stop before vendor topology, HSM, SHE, accelerator, or driver implementation claims. Handoff: project/vendor authority.

### 6. `CRY-006` — key identity chain

Keep CsmKey, CryIfKey, CryptoKey, CryptoKeyType, and CryptoKeyElement as separate identities. Use symbolic/value-free records only. Handoff: project key design and product mapping.

### 7. `CRY-007` — key operations

Catalogue set/get/copy/generation/derivation/exchange/random-seed/set-valid as separate operations. Do not record key data or infer persistence or acceptance from set-valid. Handoff: lifecycle design.

### 8. `CRY-008` — key state boundary

Model configured/reference, provisioned/populated, valid, available, selected/referenced, actually used, and persisted as separate states. Do not assert any transition without evidence. Handoff: provisioning/storage/runtime evidence.

### 9. `CRY-009` — KeyM lifecycle

Record KeyM start/update/finalize and validity handoff as KeyM lifecycle semantics, distinct from CSM scheduling and driver execution. Do not create an OEM provisioning protocol. Handoff: project lifecycle design.

### 10. `CRY-010` — KeyM certificate boundary

Separate certificate configuration, storage/presentation, parsing, verification, status, and public-key handoff. Do not treat certificate status as authorization or store certificate/private material. Handoff: project PKI/design authority.

### 11. `CRY-011` — RNG and entropy boundary

Record random-generation/random-seed service semantics only. Stop before entropy-source identity, quality, provenance, testing, or certification. Handoff: project security/qualification authority if load-bearing.

### 12. `CRY-012` — Authentication `0x29` consumer

Retain only `DCM Authentication 0x29 -> CSM/KeyM`. Do not generalize to SecurityAccess `0x27`, universal diagnostic authorization, or current project adoption. Handoff: project diagnostic/security design.

### 13. `CRY-013` — SW-C/SecOC consumer

Record a generic application/SW-C and conditional SecOC consumer boundary. Do not add SecOC adoption, freshness, authenticator, secured-I-PDU, or acceptance design. Handoff: consumer-specific project authority.

### 14. `CRY-014` — ECUC Crypto surface

Create the AUTOSAR-side definition/reference checklist. Keep definition, value, reference, generated artifact, and runtime state separate. Stop before concrete ECUC values. Handoff: project/product configuration authority.

### 15. `CRY-015` — Vector/MICROSAR boundary

Retain the fixed Sol-reviewed product classification. Use only the generic supporting commands `dvcfg-b project validate`, `dvcfg-b project generate`, and `dvcfg-b project generate-schema` as workflow context. Stop at the Crypto-specific negative; do not upgrade it.

### 16. `CRY-016` — vendor realization

Mark Crypto Driver/HSM/SHE/accelerator realization as requiring separate vendor/hardware authority. Do not start that research in this package. Handoff: future authorized vendor unit only when load-bearing.

### 17. `CRY-017` — project provisioning and persistence inputs

List unresolved consumers, security properties, adoption choices, key hierarchy, provisioning, population, storage, persistence, and acceptance inputs with `none` selected. Vendor authority remains conditional on concrete design. Handoff: project design authority.

### 18. `CRY-018` — execution and verification evidence

Define separate evidence gates for artifacts, build, runtime, driver result, performance, consumer acceptance, verdict, and coverage. Do not execute or fabricate outcomes. Handoff: future authorized execution/evidence unit.

## Stop conditions

At any step, stop and record a bounded negative when the fixed authority does not establish a product procedure, project decision, vendor realization, or execution result. Do not fill missing values from generic AUTOSAR or Vector knowledge.

## Completion condition

The guide is complete when both matrices contain the exact 18 tasks once, the accepted availability distribution is preserved, and every next handoff is explicit. Completion is not Sol acceptance, runtime proof, or publication.
