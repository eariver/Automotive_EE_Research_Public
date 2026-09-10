# Management ECU Startup / Shutdown / ECU Mode Management Current Package Overview

Date: 2026-09-11
Status: `SOL_CURRENT_PACKAGE_REVIEW_PASS` projection
Private authority: `eariver/Automotive_EE_Engineering_Knowledge@0811d2863669fcc3dfd0c0beecfbbd616e8f70d4`

## Purpose

This overview summarizes the Sol-reviewed Management ECU Startup / Shutdown / ECU Mode Management current package for public readers. It adds no new technical proposition beyond the accepted private package. Six large private YAML artifacts are used as authority for this synthesis; they are not raw-copied into the public repository.

## Lifecycle phases

The package keeps the startup, mode-management, shutdown, wakeup and sleep concerns as distinct phases preserved from the accepted baseline (`f23ebaac`):

1. scope, roles and ownership allocation (`ECUM-001`)
2. reset/boot entry and pre-OS entry (`ECUM-002`)
3. StartPreOS / driver-initialization phases (`ECUM-003`)
4. StartOS control transfer (`ECUM-004`)
5. StartupTwo / StartPostOS / SchM / BswM / RTE handoff (`ECUM-005`)
6. RUN / POST_RUN request and arbitration (`ECUM-006`)
7. BswM mode request and rule evaluation (`ECUM-007`)
8. BswM Action List and action execution (`ECUM-008`)
9. ComM/Nm lifecycle interaction (`ECUM-009`)
10. NvM ReadAll / WriteAll persistence handoffs (`ECUM-010`, `ECUM-012`)
11. shutdown initiation and target selection (`ECUM-011`)
12. late shutdown (`ECUM-013`)
13. wakeup detection, validation and reaction (`ECUM-014`, `ECUM-015`)
14. sleep/wakeup and communication-mode coordination (`ECUM-016`)
15. project-specific design inputs (`ECUM-017`)
16. runtime evidence, verdict and traceability (`ECUM-018`)

A stronger result in one phase never silently completes another phase.

## 18-task scope

`ECUM-001` through `ECUM-018` are retained exactly once. The compact coverage matrix (`matrices/20260911_ManagementECU_Startup_Shutdown_Mode_Management_Public_Coverage_Matrix.yaml`) is mechanically derived from the private Requirement Catalog, Gap Status and Validation Matrix.

## Reviewed safe frontier

- Semantic authority, product procedure authority, project input/design and execution evidence are independent planes.
- Configuration, generated artifact, runtime evidence, requirement verdict and coverage are never merged.
- Product procedure is never runtime proof.
- A semantic overlay never selects a project value and never proves a runtime outcome.

## AUTOSAR ECUM-006..008 overlay

Only the Sol-reviewed safe frontier from `Research_AUTOSAR_CP_Documents@4dc3d7c9` is reflected:

- `ECUM-006` (`REVIEWED_AUTHORITY_AVAILABLE`): EcuM owns the lifecycle-specific RUN/POST_RUN request protocol. `BswM_EcuM_RequestedState` is part of the reviewed EcuM-to-BswM request/input boundary. Request semantics are not complete BswM arbitration semantics. Project requestors, counts, timing, priority and lifecycle mapping remain unresolved.
- `ECUM-007` (`PARTIAL_REVIEWED_AUTHORITY`): BswM Mode Arbitration and Mode Control are distinct conceptual stages. Arbitration evaluates configured logical rules over mode requests/indications. Immediate arbitration (possibly in caller context) and deferred arbitration (through the BswM main function) are distinct at the reviewed depth. Project priorities, evaluation ordering, expressions and requestor-to-rule mappings are not established.
- `ECUM-008` (`PARTIAL_REVIEWED_AUTHORITY`): Mode Control executes ordered Action Lists selected by arbitration results at the reviewed concept depth. Action Lists may invoke other BSW/RTE services, reference another Action List, or cause further rule evaluation. Selection, invocation, downstream completion and runtime outcome remain distinct. BswM EcuM actions do not transfer EcuM implementation ownership; BswM NvM actions do not prove completion or persistence. Failure/return semantics, nesting detail, project contents/order and runtime outcome remain gaps.

No project BswM rule or Action List is inferred from these semantic examples.

## Vector product-procedure aggregate

From `Research_Vector_Documents@c7fc341a` via the lossless baseline-canonical mapping:

- `PARTIAL_REVIEWED_PRODUCT_PROCEDURE`: 3 (`ECUM-003` pre-OS list/item configuration, `ECUM-005` post-OS list/item configuration, `ECUM-009` BswM Communication Control)
- `SURFACE_OR_ROLE_ONLY`: 4 (`ECUM-001`, `ECUM-006` / `ECUM-011` BswM Ecu State Handling, `ECUM-016` communication/state-handling surfaces)
- `NO_EXPLICIT_REVIEWED_PRODUCT_PROCEDURE`: 9 (`ECUM-002`, `ECUM-004`, `ECUM-007`, `ECUM-008`, `ECUM-010`, `ECUM-012`, `ECUM-013`, `ECUM-014`, `ECUM-015`)
- `OUTSIDE_AUTHORIZED_PRODUCT_SCOPE`: 1 (`ECUM-018`)
- `NOT_REQUIRED`: 1 (`ECUM-017`)
- explicit reviewed procedure: 0; total 18

`NO_EXPLICIT_REVIEWED_PRODUCT_PROCEDURE` records a documentation/reviewed-procedure scope outcome at the exact Vector commit and is never a Vector/MICROSAR capability-absence claim. Partial procedures never select Management ECU allocations: no driver allocation/order, no invocation proof, no availability proof, no complete ComM/Nm handoff.

## Retained gaps

- Reset/boot source and policy; MCU/power-controller integration (`ECUM-002`)
- Actual driver-init phase allocation/order (`ECUM-003`)
- OS application mode/scheduling; RTE/application completion definition (`ECUM-004`, `ECUM-005`)
- RUN/POST_RUN requestors, arbitration and readiness criteria (`ECUM-006`)
- BswM project rules/expressions/priorities/evaluation order and explicit Vector rule procedure (`ECUM-007`)
- BswM project Action Lists/actions/order and explicit Vector Action List procedure (`ECUM-008`)
- ComM/Nm users/channels/PNCs/mappings; NvM participating blocks and validity/durability policy (`ECUM-009`, `ECUM-010`, `ECUM-012`)
- Shutdown requestors/trigger/target; OFF/RESET/sleep selection; halt/poll/sleep and power strategy; single-core vs multi-core topology (`ECUM-011`, `ECUM-013`)
- Wakeup sources, detection owner/registration, validation owner/timeouts/expiration/reaction (`ECUM-014`, `ECUM-015`)
- Sleep/power-state strategy and coordination policy (`ECUM-016`)

None is closed by neighboring semantic, product-surface or workflow evidence.

## Project design blockers

Every concrete Management ECU selection remains unresolved: reset/boot policy, MCU/power integration, initialization lists/items/order, OS application mode/scheduling, startup completion and application-readiness definition, RUN/POST_RUN requestors, BswM rules and Action Lists, ComM/Nm mappings, NvM blocks, shutdown trigger/target, OFF/RESET/sleep strategy, wakeup sources and validation timing, sleep/power policy, multicore topology, compiler/linker/deployment baseline, numeric thresholds, verdict rules and coverage targets. Standards and product authority never select these values.

## Runtime evidence boundary

The public package contains no configured project artifact, build/deploy result, startup/shutdown/wakeup observation, requirement comparison, verdict or coverage evidence. DaVinci validation/generation success and configured initialization order prove no lifecycle behavior. All runtime verdicts are `NOT_EVALUATED`. Runtime PASS count is 0.
