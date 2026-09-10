# Management ECU Startup / Shutdown / ECU Mode Management Engineering

## Theme scope

This public package presents the Sol-reviewed (`SOL_CURRENT_PACKAGE_REVIEW_PASS`) Management ECU Startup / Shutdown / ECU Mode Management current package as a reader-facing projection. It covers the ECU reset/boot entry, pre-OS and post-OS startup handoffs, RUN/POST_RUN arbitration, BswM rule evaluation and action execution, ComM/Nm and NvM lifecycle handoffs, controlled shutdown, wakeup handling and sleep coordination without collapsing lifecycle orchestration, rule arbitration, project design and runtime evidence.

The engineering lifecycle is treated as kept-distinct phases:

- scope, roles and ownership allocation
- reset/boot entry and pre-OS entry
- StartPreOS / driver-initialization phases
- StartOS control transfer
- StartupTwo / StartPostOS / SchM / BswM / RTE startup handoff
- RUN / POST_RUN request and arbitration
- BswM mode request and rule evaluation
- BswM Action List and action execution
- ComM/Nm lifecycle interaction
- NvM ReadAll / WriteAll persistence handoffs
- shutdown initiation and target selection
- late shutdown (ShutdownOS / ShutdownAllCores / OFF / RESET / sleep)
- wakeup detection, validation and reaction
- sleep/wakeup and communication-mode coordination
- project-specific design inputs
- runtime evidence, verdict and traceability

Each phase transition must be evidenced separately. No arrow is automatic.

## 18-task identity

The fixed task population is exactly `ECUM-001` through `ECUM-018`, each once:

- `ECUM-001` — scope, roles, ownership and lifecycle-plane boundaries
- `ECUM-002` — reset/boot entry and pre-OS initialization boundary (`AUTHORITY_GAP` retained)
- `ECUM-003` — EcuM StartPreOS / driver-initialization phases and handoff (partial product procedure)
- `ECUM-004` — StartOS control-transfer boundary (reviewed handoff fact; runnable proof still required)
- `ECUM-005` — EcuM_StartupTwo, StartPostOS, SchM/BswM/RTE startup handoff (partial product procedure)
- `ECUM-006` — RUN / POST_RUN request and lifecycle arbitration boundary (AUTOSAR reviewed authority)
- `ECUM-007` — BswM mode request / rule-evaluation semantics (AUTOSAR partial authority; no explicit Vector rule procedure)
- `ECUM-008` — BswM action-list / action-execution boundary (AUTOSAR partial authority; no explicit Vector Action List procedure)
- `ECUM-009` — ComM/Nm mode interaction with ECU lifecycle (partial product procedure)
- `ECUM-010` — NvM ReadAll startup persistence handoff (reviewed trigger ownership; no explicit Vector action procedure)
- `ECUM-011` — shutdown initiation / GoDown / shutdown-target selection (product surface only)
- `ECUM-012` — NvM WriteAll shutdown persistence handoff (reviewed trigger ownership; no explicit Vector action procedure)
- `ECUM-013` — late shutdown / ShutdownOS / OFF / RESET / sleep-target boundary (target still project design)
- `ECUM-014` — wakeup-source detection / event-registration boundary (sources still project design)
- `ECUM-015` — wakeup validation / expiration / reaction boundary (timeouts/reaction still project design)
- `ECUM-016` — sleep/wakeup and communication-mode coordination (product surfaces only)
- `ECUM-017` — Management ECU project-specific design inputs (all values unresolved)
- `ECUM-018` — runtime evidence, requirement verdict and traceability (no evidence claimed)

## Package contents

- `20260911_ManagementECU_Startup_Shutdown_Mode_Management_Current_Package_Overview.md` — reader-facing summary
- `20260911_ManagementECU_Startup_Shutdown_Mode_Management_Engineering_Methodology.md` — evidence-plane separation and lifecycle rules
- `20260911_ManagementECU_Startup_Shutdown_Mode_Management_Step_by_Step_Guide.md` — future project execution framework (not a result)
- `20260911_ManagementECU_Startup_Shutdown_Mode_Management_Sol_Review.md` — Sol review, byte-identical to the accepted private authority
- `models/20260911_ManagementECU_Startup_Shutdown_Mode_Management_State_Evidence_Model.md` — state separation model
- `matrices/20260911_ManagementECU_Startup_Shutdown_Mode_Management_Public_Coverage_Matrix.yaml` — 18-row compact matrix, runtime PASS 0
- `references/20260911_ManagementECU_Startup_Shutdown_Mode_Management_Reference_Index.md` — exact repository/commit/path authority index
- `publication/README.md` — publication boundary statement
- `publication/publication-plan.yaml` — fixed pins and projection policy
- `publication/2026-09-11_publication-validation.md` — added in Phase P2 only

## Reviewed authority pins

- Private publication authority: `eariver/Automotive_EE_Engineering_Knowledge@0811d2863669fcc3dfd0c0beecfbbd616e8f70d4` (`SOL_CURRENT_PACKAGE_REVIEW_PASS`)
- Candidate: `eariver/Automotive_EE_Engineering_Knowledge@6974c45a571b053ec3f48c7cbfa8e5b87cdf2077`
- Baseline: `eariver/Automotive_EE_Engineering_Knowledge@f23ebaac9c9b658507263894b096bda680d6f890`
- AUTOSAR semantic depth: `eariver/Research_AUTOSAR_CP_Documents@4dc3d7c912cba7c3df77285d32bf2ad18a47a5f0` / `docs/knowledge/management-ecu-startup-shutdown-mode-management-autosar-semantic-depth.md`
- Vector product procedure: `eariver/Research_Vector_Documents@c7fc341afd12a0c4a636641efcad2ceabceb9d0f` / `docs/knowledge/management-ecu-startup-shutdown-mode-management-vector-procedure.md`

No Web, Drive, raw AUTOSAR PDF, Vector HELP, floating-branch, generated-code, project-ARXML or runtime-target source is part of this publication. No raw licensed bytes are included. No Management ECU project values are selected. Every runtime verdict is `NOT_EVALUATED` and the runtime PASS count is 0.
