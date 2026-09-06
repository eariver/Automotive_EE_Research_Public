# Management ECU Crypto Project Scope

Date: `2026-09-06`

Status: `BOUNDED_BASELINE_COMPILATION`

## Purpose

This package integrates already reviewed AUTOSAR Crypto semantics, Vector/MICROSAR procedure findings, existing Consumption Layer context, Management ECU project requirements, and UDS ownership boundaries into a task-level engineering baseline. It records what is available and what remains blocked; it does not create a new Crypto research system or project design.

## Authority planes

The technical authority planes are pinned in `references/authority-pins.yaml`:

- AUTOSAR CP 4.4.0 semantic authority: `eariver/Research_AUTOSAR_CP_Documents@9903efc816f8589d865e36f26f7fe44fb27c62b9`, Reviewed Knowledge blob `4cb5eaba08ee7cba5d89bef67ee0174bd31997b7`.
- Vector/MICROSAR procedure authority: `eariver/Research_Vector_Documents@aab6c3f9ad60493b6176ff0ad9b7f25dcc37b1fe`, reviewed DaVinci Configurator Classic 6.3.10 user-manual scope.
- Existing downstream integration baseline: `eariver/Automotive_EE_Engineering_Knowledge@b4dd1d40b0abe4fa7a18211808b1cc6df41d1997`.
- Project requirement and UDS context are read-only context pins, not Crypto technical authority.

No floating branch, `main`, current vendor page, Web page, raw AUTOSAR PDF, raw Vector HELP, or generic recollection is used as new technical evidence.

## Ownership and lifecycle boundary

The baseline keeps the following layers distinct:

```text
project scope / consumer intent
    -> AUTOSAR CSM / CryIf / Crypto Driver / KeyM semantic model
    -> ECUC configuration/reference design
    -> Vector/MICROSAR product procedure (if explicitly reviewed)
    -> Crypto Driver / HSM / SHE vendor realization (if separately authorized)
    -> generated artifact and build handoff
    -> runtime operation and evidence
    -> consumer acceptance, test verdict, and coverage
```

No arrow above is evidence that a downstream state exists. In particular:

```text
CSM service request != Crypto Job != configured primitive
CsmKey != CryIfKey != CryptoKey != CryptoKeyType != CryptoKeyElement
CryIf channel != Crypto Driver Object
configured/reference != provisioned/populated != valid != available != selected/referenced != actually used
KeyM certificate status != consumer authorization
DCM Authentication 0x29 != SecurityAccess 0x27 != universal diagnostic authorization
random/random-seed API != entropy source != entropy quality != seed provenance != randomness certification
AUTOSAR semantics != Vector/MICROSAR realization != vendor hardware realization != project design != runtime evidence
configuration != validation != generation != compile/link != runtime execution
cryptographic result != consumer acceptance != test verdict != coverage
```

## Current Management ECU project boundary

The fixed Management ECU requirement baseline does not adopt a specific Crypto consumer. The following remain unresolved project decisions and are not filled by this package:

- actual Crypto consumers and required security properties;
- Authentication `0x29` adoption;
- SecOC adoption;
- KeyM certificate use;
- algorithm, mode, key-role, queue, and priority choices;
- key hierarchy and provisioning source/backend/protocol;
- population/update lifecycle and persistence expectations;
- security-function acceptance criteria.

The existing UDS package continues to own its diagnostic responsibility and boundary. This package records only the source-supported `DCM Authentication 0x29 -> CSM/KeyM` consumer relation and does not alter the UDS package.

## Vector procedure boundary

The Sol-reviewed Vector result is fixed:

| Reviewed slice | Status |
|---|---|
| CSM configuration | `NO_EXPLICIT_REVIEWED_PROCEDURE` |
| CryIf channel/key mapping | `NO_EXPLICIT_REVIEWED_PROCEDURE` |
| Crypto Driver Object/key/key-element configuration | `NO_EXPLICIT_REVIEWED_PROCEDURE` |
| KeyM key/certificate configuration | `NO_EXPLICIT_REVIEWED_PROCEDURE` |
| DCM Authentication `0x29` -> CSM/KeyM product integration | `NO_EXPLICIT_REVIEWED_PROCEDURE` |
| Crypto-specific validation/generation/artifact procedure | `NO_EXPLICIT_REVIEWED_PROCEDURE` |
| HSM/SHE/Crypto Driver implementation realization | `OUTSIDE_AUTHORIZED_PRODUCT_SCOPE` |
| provisioning/population/runtime-evidence procedure | `OUTSIDE_AUTHORIZED_PRODUCT_SCOPE` |

The exact generic supporting procedures remain separately visible:

```text
dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
```

These generic commands do not establish a Crypto-specific object procedure, diagnostic, generated artifact identity, compile/link contract, HSM image, provisioning result, or runtime result.

## Secret-material boundary

This package contains no actual symmetric key, private key, certificate private material, seed or entropy value, credential, password, token, OEM secret, project key value, key-element value, HSM slot content, or proprietary derivation input. Symbolic roles, value-free field identities, state categories, and engineering boundaries only may be retained.

## Disposition

Generic AUTOSAR Crypto research is closed. Vector Crypto-specific procedure research is closed at the fixed reviewed scope. Remaining gaps are explicitly classified in the two YAML baselines and are not silently promoted to project requirements or runtime proof.

Next justified step: current-package compilation / Sol review. HSM/vendor research is conditional on a later concrete project design or load-bearing requirement.
