# Management ECU Crypto Development Methodology

Date: `2026-09-06`

Status: `CURRENT_PACKAGE_COMPILATION`

## 1. Purpose and scope

This methodology compiles the already accepted Management ECU Crypto baseline into a usable engineering package. It does not reopen AUTOSAR Crypto research, Vector HELP research, vendor research, project design, generated-code inspection, or runtime execution.

The package is an integrated topic package within the existing Management ECU / Automotive EE Knowledge structure. It uses the accepted 18-task registry, the remaining-gap backlog, the project-input baseline, the Sol baseline review, the existing Consumption Layer anchors, and the existing UDS responsibility boundary as read-only inputs.

## 2. Engineering flow

```text
project security / consumer input
    -> scope and ownership baseline
    -> AUTOSAR CSM/CryIf/Crypto Driver/KeyM semantic model
    -> ECUC definition/reference design
    -> Vector/MICROSAR product-procedure boundary
    -> conditional Crypto Driver/HSM/SHE/vendor realization
    -> generated artifact and build handoff
    -> runtime Crypto execution and state evidence
    -> consumer acceptance, test verdict, and coverage
```

Every arrow is a handoff, not an automatic state transition. A later artifact may only be promoted when the preceding layer has its own accepted input and evidence.

## 3. Phase 0 — project input and ownership

Start with the project-owned questions: which consumers require Crypto services, which security properties are required, which owner accepts the result, and whether Authentication `0x29`, SecOC, KeyM certificate handling, or another consumer is adopted. The current project-input baseline has no concrete Crypto consumer adoption, so these values remain unresolved.

The UDS package remains the owner of diagnostic service/session/security responsibility. This package retains only the bounded `DCM Authentication 0x29 -> CSM/KeyM` consumer relation and does not assign project access policy.

No actual key, credential, algorithm selection, target setting, acceptance threshold, or runtime stimulus is created at this phase.

## 4. Phase 1 — AUTOSAR semantic design

Use the exact pinned AUTOSAR Reviewed Knowledge to allocate semantic ownership and references. Preserve these identities:

```text
CSM service request != Crypto Job != configured primitive
CsmKey != CryIfKey != CryptoKey != CryptoKeyType != CryptoKeyElement
CryIf channel != Crypto Driver Object
```

Keep processing mode, queue, priority, callback, cancellation, operation mode, key lifecycle, certificate state, and random/seed service state separate. Generic semantic closure does not establish a project consumer, product configuration, vendor implementation, or runtime result.

## 5. Phase 2 — ECUC and configuration design

Translate the semantic model into a value-free project checklist for CSM, CryIf, Crypto Driver, KeyM, key, primitive, queue, callback, and certificate definitions/references. Treat configuration definition, configuration value, configuration reference, generated configuration, and runtime state as separate artifacts.

The accepted baseline does not contain Management ECU-specific values. Do not fill IDs, algorithms, key roles, queue/priority values, key slots, or storage addresses.

## 6. Phase 3 — Vector/MICROSAR product boundary

The fixed Sol-reviewed Vector authority establishes no Crypto-specific reviewed product procedure for six slices and places two slices outside the authorized product scope. The exact generic supporting commands are retained only as workflow context:

```text
dvcfg-b project validate
dvcfg-b project generate
dvcfg-b project generate-schema
```

Generic CLI status/exit-code and generic CI workflow context may be used as supporting workflow. They do not establish Crypto-specific object mapping, diagnostic, generated-artifact, compiler/linker, HSM, provisioning, or runtime procedure.

When the safe frontier is reached, record the documentation-scope negative and hand off to project design or a separately authorized evidence unit. Do not manufacture an exact or partial Crypto procedure.

## 7. Phase 4 — conditional vendor and hardware realization

Vendor/HSM/SHE/accelerator authority is explicit for the implementation-realization task. For project input and execution tasks it is conditional: it becomes an additional dependency only when a concrete project realization makes it load-bearing.

No HSM topology, SHE policy, accelerator capability, driver implementation, key slot, firmware/image, persistence behavior, or performance claim is inferred from AUTOSAR or generic Configurator material.

## 8. Phase 5 — artifacts, build, runtime, and verification

Generated artifact inspection, compile/link, deployed/virtual/physical execution, Crypto Driver job execution, provisioning/population, performance/resource measurement, consumer acceptance, test verdict, and coverage are separate evidence layers. The current package only defines their required handoffs; it does not execute them.

```text
configuration != validation != generation != compile/link != runtime execution
cryptographic result != consumer acceptance != test verdict != coverage
```

Configuration or generation success cannot close the execution-evidence gate.

## 9. Global safety rules

- Keep the exact 18-task registry unchanged.
- Preserve `WORKFLOW_ONLY = 1`, `NO_EXPLICIT_REVIEWED_PROCEDURE = 14`, and `OUTSIDE_AUTHORIZED_PRODUCT_SCOPE = 3`.
- Preserve `CRY-016` as the explicit vendor/hardware authority blocker.
- Preserve `CRY-017` as project-input required with conditional vendor dependency.
- Preserve `CRY-018` as execution-evidence required with conditional vendor dependency.
- Never store symmetric/private keys, certificate private material, seed/entropy values, credentials, tokens, OEM secrets, key-element values, HSM slot contents, or proprietary derivation inputs.
- Stop at a safe frontier when authority is absent; record the bounded negative and the next required evidence.

## 10. Exit and next handoff

The current package is complete when all 18 task rows are represented in both matrices, exact authority provenance is retained, the dimensional classifications remain separate, and all unresolved project/vendor/runtime gates are explicit. The next justified step is Sol review of this current package. HSM/vendor research is not started automatically.
