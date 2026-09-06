# Management ECU Crypto Reference Index

Date: `2026-09-06`

This index is navigation and provenance for the current package. It does not promote any floating branch or source.

## 1. Exact technical authority

| Authority | Exact pin | Role |
|---|---|---|
| AUTOSAR Crypto | `eariver/Research_AUTOSAR_CP_Documents@9903efc816f8589d865e36f26f7fe44fb27c62b9` / `docs/knowledge/management-ecu-crypto-autosar-semantic-depth.md` / blob `4cb5eaba08ee7cba5d89bef67ee0174bd31997b7` | Sol-reviewed AUTOSAR CP 4.4.0 semantic authority |
| Vector/MICROSAR | `eariver/Research_Vector_Documents@aab6c3f9ad60493b6176ff0ad9b7f25dcc37b1fe` / `docs/knowledge/management-ecu-crypto-vector-procedure.md` | Sol-reviewed DaVinci Configurator Classic 6.3.10 procedure authority |
| Vector review checkpoint | `docs/checkpoints/2026-09-06_sol-management-ecu-crypto-vector-procedure-review.md` at the same Vector reviewed commit | Sol review provenance |

The Vector result is six `NO_EXPLICIT_REVIEWED_PROCEDURE` slices and two `OUTSIDE_AUTHORIZED_PRODUCT_SCOPE` slices. Generic validation/generation/schema commands are supporting workflow only.

## 2. Integrated downstream context

| Artifact | Exact pin/path | Role |
|---|---|---|
| Crypto integration baseline | `eariver/Automotive_EE_Engineering_Knowledge@b4dd1d40b0abe4fa7a18211808b1cc6df41d1997` / `docs/knowledge/management-ecu-crypto-authority-integration-baseline.md` | Existing Management ECU integration context |
| Management ECU project requirements | `eariver/Automotive_EE_Engineering_Knowledge@690b23a6d5f08713fc88f3ef251a041e4c9ec4d8` / `docs/projects/2026-09-02_management-ecu-lv3-vecu-application-swc-engineering/references/project/requirement-baseline.yaml` | Read-only project requirement context |
| UDS continuity | `eariver/Automotive_EE_Engineering_Knowledge@b1835a0df8803a0ee2483e553f4c9089d1807179` / `docs/projects/2026-09-02_management-ecu-uds-on-can-diagnostic-engineering/` | Read-only diagnostic ownership/boundary context |
| Sol accepted baseline | `docs/projects/2026-09-06_management-ecu-cryptographic-services-key-management-engineering/checkpoints/2026-09-06_sol-management-ecu-crypto-baseline-review.md` | Fixed acceptance and handoff |

## 3. Existing local baseline artifacts consumed read-only

- `baseline/crypto-task-baseline.yaml`
- `baseline/crypto-research-gap-backlog.yaml`
- `references/authority-pins.yaml`
- `references/project/crypto-project-input-baseline.yaml`
- `20260906_ManagementECU_Crypto_Baseline_Report.md`
- `20260906_ManagementECU_Crypto_Project_Scope.md`
- `docs/knowledge/management-ecu-crypto-authority-integration-baseline.md`

## 4. Current-package artifacts

- `20260906_ManagementECU_Crypto_Development_Methodology.md`
- `20260906_ManagementECU_Crypto_Step_by_Step_Guide.md`
- `matrices/20260906_ManagementECU_Crypto_Tool_Task_Reference_Matrix.yaml`
- `20260906_ManagementECU_Crypto_State_and_Evidence_Model.md`
- `20260906_ManagementECU_Crypto_Execution_Reference_Guide.md`
- `matrices/20260906_ManagementECU_Crypto_Procedure_Coverage_Matrix.yaml`
- `20260906_ManagementECU_Crypto_Reference_Index.md`
- `20260906_ManagementECU_Crypto_Current_Package_Compilation_Report.md`
- `checkpoints/2026-09-06_luna-management-ecu-crypto-current-package-compilation.md`

## 5. Navigation rule

The package consumes exact-pinned Reviewed Knowledge and project-local artifacts. It does not modify `docs/knowledge/**`, the Consumption Layer, the UDS package, or upstream repositories. New technical evidence is outside this compilation.
