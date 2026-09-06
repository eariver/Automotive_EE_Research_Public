# Management ECU — Cryptographic Services & Key Management Engineering

Status: `BASELINE_COMPILATION_READY_FOR_SOL_REVIEW`

This directory is a topic engineering package inside the existing Management ECU / Automotive EE Knowledge integration. It is not an independent Crypto knowledge system and it does not reopen the generic AUTOSAR or Vector research tracks.

The package compiles exactly 18 task records, `CRY-001` through `CRY-018`, from fixed Sol-reviewed authority. It keeps standards semantics, product procedure, project design/input, vendor/hardware authority, and execution evidence as separate dimensions.

## Fixed scope

- AUTOSAR Classic Platform 4.4.0 Crypto Services and Key Management semantic authority is closed at the reviewed depth.
- DaVinci Configurator Classic 6.3.10 / MICROSAR Crypto-specific procedure coverage remains the reviewed six-slice negative plus two authorized-scope negatives; generic project commands are retained only as supporting workflow.
- Management ECU consumer adoption, provisioning, population, persistence, hardware realization, performance, runtime, verdict, and coverage remain open boundaries.
- DCM Authentication `0x29` is retained only as the bounded `DCM -> CSM/KeyM` consumer relation. It is not generalized to SecurityAccess `0x27` or universal diagnostic authorization.
- SecOC remains conditional and is not adopted by the current Management ECU requirement baseline.
- Secret/private/project-specific Crypto material is excluded. Only symbolic, value-free engineering metadata is admissible.

## Outputs

1. `20260906_ManagementECU_Crypto_Project_Scope.md` — scope, ownership, and boundary contract.
2. `references/authority-pins.yaml` — exact authority tuples and source policy.
3. `references/project/crypto-project-input-baseline.yaml` — unresolved project inputs/design decisions without invented values.
4. `baseline/crypto-task-baseline.yaml` — the exact 18-task engineering baseline.
5. `baseline/crypto-research-gap-backlog.yaml` — one remaining-gap record per task.
6. `20260906_ManagementECU_Crypto_Baseline_Report.md` — bounded compilation report.
7. `checkpoints/2026-09-06_luna-management-ecu-crypto-baseline-compilation.md` — compilation checkpoint and validation contract.

## Next justified step

The next step is current-package compilation / Sol review of this bounded baseline. HSM/vendor research is not started automatically; it is reconsidered only if concrete project design or a load-bearing requirement requires it.
