# Management ECU NvM / Memory Persistence Reference Index

Status: `LUNA_CURRENT_PACKAGE_COMPILE_PROPOSAL`  
Date: 2026-09-05

This index is the provenance boundary for the current package. Every technical
claim in the two machine-readable matrices is tied to one or more exact tuples
below. The package does not read or cite a floating branch/head.

## 1. Primary exact pins

| Key | Exact reviewed tuple | Role |
|---|---|---|
| `AUTOSAR_BASE` | `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d` | AUTOSAR Classic 4.4.0 reviewed base. |
| `AUTOSAR_NVM_DEPTH` | `eariver/Research_AUTOSAR_CP_Documents@d021e2471b8c76efc6af43f66c17d7ead68821cc:docs/knowledge/management-ecu-nvm-autosar-semantic-depth.md` | Sol-reviewed NvM semantic depth. |
| `VECTOR_NVM_PROCEDURE` | `eariver/Research_Vector_Documents@d7eb75af93ac82d155fe508681b7057802c3aa45:docs/knowledge/management-ecu-nvm-vector-procedure.md` | Sol-reviewed DaVinci Configurator Classic 6.3.10 procedure expansion. |
| `PROJECT_INPUT` | `eariver/Automotive_EE_Engineering_Knowledge@e4ba6a26d2a90e4fd65e176c0b09c4edae12406b:docs/projects/2026-09-05_management-ecu-nvm-memory-persistence-engineering/references/project/nvm-memory-persistence-project-input-baseline.yaml` | Project-value authority; status `UNRESOLVED_PROJECT_INPUT`. |

The `PROJECT_INPUT` tuple is a project authority reference, not a technical
standard authority. No value from it is accepted by this compilation.

## 2. AUTOSAR reviewed base catalog

All rows in this table are pinned to
`eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d`.
The blob SHA is recorded from `references/authority-pins.yaml`.

| Key | Exact path | Blob SHA | Reviewed entry / use |
|---|---|---|---|
| `logical_block_ownership` | `docs/knowledge/concepts/nvm-logical-block-ownership.json` | `0b0fbd189e6fe5c300a705e74b2d858b27bf1c48` | `AUTOSAR-CP-4.4.0-CONCEPT-NVM-LOGICAL-BLOCK-OWNERSHIP`; logical NvM block and Native/Redundant/Dataset model. |
| `synchronization_recovery_boundary` | `docs/knowledge/concepts/nvm-synchronization-recovery-boundary.json` | `6f4efb7288c4d5a7eecd856f47d92d4f69c8459d` | `AUTOSAR-CP-4.4.0-CONCEPT-NVM-SYNCHRONIZATION-RECOVERY-BOUNDARY`; RAM synchronization and recovery ownership. |
| `memory_stack_layer_ownership` | `docs/knowledge/concepts/memory-stack-layer-ownership.json` | `e15489868acb8b537ecfca11cb2ce89441871e01` | `AUTOSAR-CP-4.4.0-CONCEPT-MEMORY-STACK-LAYER-OWNERSHIP`; NvM/MemIf/Fee/Ea/Fls/Eep ownership. |
| `memif_dispatch_status_boundary` | `docs/knowledge/concepts/memif-dispatch-status-boundary.json` | `c03c6b8ba29cdc3d522b3d0cc6ff76d4f7da34de` | `AUTOSAR-CP-4.4.0-CONCEPT-MEMIF-DISPATCH-STATUS-BOUNDARY`; DeviceIndex and `MEMIF_*` status boundary. |
| `fee_ea_logical_consistency_boundary` | `docs/knowledge/concepts/fee-ea-logical-consistency-internal-management-boundary.json` | `77a22beabedc694661fd3fe87581c3721e342c9e` | `AUTOSAR-CP-4.4.0-CONCEPT-FEE-EA-LOGICAL-CONSISTENCY-INTERNAL-MANAGEMENT-BOUNDARY`; logical consistency/internal management. |
| `lower_cancel_hardware_boundary` | `docs/knowledge/concepts/lower-memory-cancel-hardware-completion-boundary.json` | `bedfbad05f223ae1f2b98edd396656a490af5252` | `AUTOSAR-CP-4.4.0-CONCEPT-LOWER-MEMORY-CANCEL-HARDWARE-COMPLETION-BOUNDARY`; cancel versus hardware completion. |
| `lower_error_result_boundary` | `docs/knowledge/concepts/lower-memory-error-result-reporting-boundary.json` | `1aa7638862389a4ec1f7e0f623f8eac306767854` | `AUTOSAR-CP-4.4.0-CONCEPT-LOWER-MEMORY-ERROR-RESULT-REPORTING-BOUNDARY`; status, result and reporting vocabularies. |
| `physical_verification_integrity_boundary` | `docs/knowledge/concepts/physical-memory-verification-integrity-boundary.json` | `f4a6c92527a6d9a26f0f64c54d6fba164d76f035` | `AUTOSAR-CP-4.4.0-CONCEPT-PHYSICAL-MEMORY-VERIFICATION-INTEGRITY-BOUNDARY`; physical verification versus upper integrity. |
| `readall_writeall_lifecycle` | `docs/knowledge/workflows/nvm-readall-writeall-lifecycle.json` | `7539c526f760e54b8ee2a1d2f92227ac3896ea62` | `AUTOSAR-CP-4.4.0-WORKFLOW-NVM-READALL-WRITEALL-LIFECYCLE`; BswM/NvM startup-shutdown handoff. |
| `nvm_to_physical_job_path` | `docs/knowledge/workflows/nvm-to-physical-memory-job-path.json` | `8ebc7abaf02129e67d12bc3900f78c3f09253ae5` | `AUTOSAR-CP-4.4.0-WORKFLOW-NVM-TO-PHYSICAL-MEMORY-JOB-PATH`; logical request to physical job navigation. |
| `fee_to_fls_trace` | `docs/knowledge/workflows/trace-fee-logical-write-to-fls-physical-job.json` | `6fd333d037b8205b86378824a428652e4c7c9045` | `AUTOSAR-CP-4.4.0-WORKFLOW-TRACE-FEE-LOGICAL-WRITE-TO-FLS-PHYSICAL-JOB`; Fee/Fls trace. |
| `ea_to_eep_trace` | `docs/knowledge/workflows/trace-ea-logical-write-to-eep-physical-job.json` | `c28ecf97811d6aa014f6f30e52a1b8a8d406d018` | `AUTOSAR-CP-4.4.0-WORKFLOW-TRACE-EA-LOGICAL-WRITE-TO-EEP-PHYSICAL-JOB`; Ea/Eep trace. |
| `lower_cancel_recovery_trace` | `docs/knowledge/workflows/trace-lower-memory-cancel-and-recovery.json` | `cc86d38c49ad07ee95ae4c34f683f645d391471b` | `AUTOSAR-CP-4.4.0-WORKFLOW-TRACE-LOWER-MEMORY-CANCEL-AND-RECOVERY`; cancel/recovery evidence route. |
| `physical_to_upper_integrity_trace` | `docs/knowledge/workflows/trace-physical-verification-to-upper-integrity-policy.json` | `1d1b4626be9ce33ff5b83c9dbf9b30d8302788d2` | `AUTOSAR-CP-4.4.0-WORKFLOW-TRACE-PHYSICAL-VERIFICATION-TO-UPPER-INTEGRITY-POLICY`; physical-to-upper integrity handoff. |

## 3. Focused and product-local reviewed documents

| Key | Exact tuple | Scope and retained negative |
|---|---|---|
| `nvm_semantic_depth` | `eariver/Research_AUTOSAR_CP_Documents@d021e2471b8c76efc6af43f66c17d7ead68821cc:docs/knowledge/management-ecu-nvm-autosar-semantic-depth.md` | Sol-reviewed changed-state, immediate-priority, protection/lock, synchronization, integrity/recovery, request-result and AUTOSAR configuration checklist. Does not define Management ECU values or Vector GUI realization. |
| `vector_procedure` | `eariver/Research_Vector_Documents@d7eb75af93ac82d155fe508681b7057802c3aa45:docs/knowledge/management-ecu-nvm-vector-procedure.md` | DaVinci Configurator Classic 6.3.10 Memory Editor, Memory Blocks Editor, bounded Event Memory Blocks Assistant, partition-level Fee/Fls-versus-Ea wording, example `Ifp.json`, exact generic validation/generation commands. Does not provide complete object-by-object NvM procedure, exact DeviceIndex mapping, complete lower-stack mapping or runtime/durability evidence. |

## 4. Task-to-authority navigation

The detailed rows in the Tool / Task / Reference Matrix carry the exact tuple
strings. This table is a compact navigation aid; it does not create additional
task identities.

| Task range | Primary reviewed authority keys | Engineering focus |
|---|---|---|
| NVM-001 | `logical_block_ownership`, `memory_stack_layer_ownership`, `readall_writeall_lifecycle` | Scope, ownership and lifecycle boundary. |
| NVM-002 | `logical_block_ownership`, `memory_stack_layer_ownership` | Application/NvData/RTE mapping remains project design/input. |
| NVM-003 | `logical_block_ownership`, `synchronization_recovery_boundary`, `nvm_semantic_depth`, `vector_procedure` | Logical blocks and bounded Memory Editor surface. |
| NVM-004 | `logical_block_ownership`, `synchronization_recovery_boundary`, `nvm_semantic_depth` | Object identity and synchronization boundary. |
| NVM-005, NVM-008 | `readall_writeall_lifecycle`, `synchronization_recovery_boundary` | Startup/shutdown multi-block workflow. |
| NVM-006, NVM-007 | `nvm_to_physical_job_path`, `synchronization_recovery_boundary`, `memif_dispatch_status_boundary`, `lower_error_result_boundary`, `fee_to_fls_trace`, `ea_to_eep_trace` | Explicit request and asynchronous lower path. |
| NVM-009, NVM-011 | `synchronization_recovery_boundary`, `physical_verification_integrity_boundary`, `nvm_semantic_depth`, `vector_procedure` | Conditional recovery/integrity choices. |
| NVM-010, NVM-012, NVM-013 | `nvm_semantic_depth`, `synchronization_recovery_boundary`, `lower_error_result_boundary`, `memif_dispatch_status_boundary`, `vector_procedure` | Changed/write, protection/RAM and status/notification boundaries. |
| NVM-014, NVM-015 | `memory_stack_layer_ownership`, `memif_dispatch_status_boundary`, `fee_ea_logical_consistency_boundary`, `nvm_to_physical_job_path`, `vector_procedure` | Dispatch, Fee/Ea branch and logical consistency. |
| NVM-016 | `fee_to_fls_trace`, `ea_to_eep_trace`, `physical_verification_integrity_boundary`, `nvm_to_physical_job_path` | Physical device-job trace. |
| NVM-017 | `nvm_semantic_depth`, `vector_procedure` | Generic validation/generation exact boundary plus partial NvM surface. |
| NVM-018 | `nvm_to_physical_job_path`, `physical_verification_integrity_boundary`, `lower_cancel_hardware_boundary`, `lower_error_result_boundary`, `lower_cancel_recovery_trace`, `physical_to_upper_integrity_trace`, `vector_procedure` | Evidence plan only; actual execution required. |

## 5. Explicit non-authority

The following are intentionally excluded from technical evidence for this
package:

- Web or current vendor documentation;
- raw AUTOSAR PDFs and raw Vector HELP;
- floating upstream `main` or branch heads;
- generic AUTOSAR/Vector model knowledge;
- unreviewed observations, worklogs, prompts or sibling-project conclusions;
- `Ifp.json` example mappings as Management ECU backend selection;
- generated artifacts as compile/link/runtime/durable-persistence evidence;
- `NVM_REQ_OK` or `MEMIF_JOB_OK` as durability, power-loss, verdict or coverage proof.

No source outside the exact tuples above is needed to interpret the current
package.
