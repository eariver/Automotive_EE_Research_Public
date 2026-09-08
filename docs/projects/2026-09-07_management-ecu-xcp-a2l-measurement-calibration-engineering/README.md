# Management ECU XCP/A2L Measurement & Calibration Engineering

## Theme scope

This public package presents the Sol-reviewed (`SOL_CURRENT_PACKAGE_REVIEW_PASS`) Management ECU XCP/A2L Measurement & Calibration current package as a reader-facing projection. It covers the A2L-description to live XCP measurement/calibration chain without collapsing standards semantics, vendor product roles, project design and runtime evidence.

The engineering lifecycle is treated as seven lanes:

- description producer
- address resolution
- consumer/master
- transport
- server/slave endpoint
- live session
- ownership/lifecycle

Each lane transition must be evidenced separately. No arrow is automatic.

## 18-task identity

The fixed task population is exactly `XCP-001` through `XCP-018`, each once:

- `XCP-001` — scope, role and ownership baseline
- `XCP-002` — intent versus application behavior and calibration ownership boundary
- `XCP-003` — object identity and A2L description ownership boundary
- `XCP-004` — A2L generation, producer role and format/version identity
- `XCP-005` — generated versus address-resolved / target-aware A2L lifecycle
- `XCP-006` — build/map/symbol/address provenance and A2L update lifecycle (`UNRESOLVED_RETAINED`)
- `XCP-007` — consumer import/update/reload and consumption ownership (`UNRESOLVED_RETAINED`)
- `XCP-008` — master/client role and tool-side connection ownership
- `XCP-009` — target-side slave/server endpoint implementation and ownership (`UNRESOLVED_RETAINED`)
- `XCP-010` — transport/profile binding and A2L-version versus XCP-protocol-version boundary
- `XCP-011` — live-session prerequisites, connection lifecycle and endpoint binding (`UNRESOLVED_RETAINED`)
- `XCP-012` — DAQ/event/channel acquisition configuration and timing ownership (AUTOSAR safe frontier)
- `XCP-013` — STIM/write/calibration operation path and boundary (AUTOSAR safe frontier)
- `XCP-014` — calibration memory/page/segment/writeability lifecycle (AUTOSAR safe frontier)
- `XCP-015` — resource/security/access-control boundary (AUTOSAR safe frontier, symbolic only)
- `XCP-016` — product-procedure/support availability and cross-tool boundary (CANape aggregate partial)
- `XCP-017` — project-specific design inputs (all values unresolved)
- `XCP-018` — runtime evidence, requirement verdict, traceability and coverage boundary (no evidence claimed)

## Package contents

- `20260908_ManagementECU_XCP_A2L_Current_Package_Overview.md` — reader-facing summary
- `20260908_ManagementECU_XCP_A2L_Engineering_Methodology.md` — evidence-plane separation and lifecycle rules
- `20260908_ManagementECU_XCP_A2L_Step_by_Step_Guide.md` — future project execution framework (not a result)
- `20260908_ManagementECU_XCP_A2L_Sol_Review.md` — Sol review, byte-identical to the accepted private authority
- `models/20260908_ManagementECU_XCP_A2L_State_Evidence_Model.md` — state separation model
- `matrices/20260908_ManagementECU_XCP_A2L_Public_Coverage_Matrix.yaml` — 18-row compact matrix, runtime PASS 0
- `references/20260908_ManagementECU_XCP_A2L_Reference_Index.md` — exact repository/commit/path authority index
- `publication/README.md` — publication boundary statement
- `publication/publication-plan.yaml` — fixed pins and projection policy
- `publication/2026-09-08_publication-validation.md` — added in Phase P2 only

## Reviewed authority pins

- Private publication authority: `eariver/Automotive_EE_Engineering_Knowledge@ff096484c8f36bc59a850b1b36575f9cf34ac279` (`SOL_CURRENT_PACKAGE_REVIEW_PASS`)
- Candidate: `eariver/Automotive_EE_Engineering_Knowledge@b0fdfeba7b92b155b3a2386a0a7fe4aa48328ce6`
- Baseline: `eariver/Automotive_EE_Engineering_Knowledge@cade7a1407e6808585b45cc46246319a2c89ed85`
- AUTOSAR semantic depth: `eariver/Research_AUTOSAR_CP_Documents@d3de1f713e84ee5131f422d64da67975527d0e91` / `docs/knowledge/management-ecu-xcp-a2l-autosar-semantic-depth.md`
- Vector CANape procedure: `eariver/Research_Vector_Documents@f75bb98188652a80056753d9a6cadd395d5d17b6` / `docs/knowledge/management-ecu-xcp-a2l-canape-product-procedure.md`
- R2D decomposition: `eariver/Automotive_EE_Engineering_Knowledge@6ab7045145ce665181baad93d97e36cdacc34358` / `docs/compilation/r2d-xcp-a2l-chain-evidence.md`

Floating branch heads are never authority. Upstream Reviewed Knowledge is referenced by locator only. No raw licensed source bytes are included.

## Important unresolved gaps

- `XCP-006`, `XCP-007`, `XCP-009`, `XCP-011` are `UNRESOLVED_RETAINED` by design and are not closed by CANape, CANoe, AUTOSAR, MathWorks or Simulink Real-Time inference.
- `XCP-012` through `XCP-015` carry the AUTOSAR reviewed safe frontier only; detailed ASAM behavior is a conditional dependency only if later load-bearing.
- `XCP-016` is `PARTIAL_PRODUCT_PROCEDURE_AVAILABLE` (CANape PROC-01..04 partial, PROC-05..07 `SOURCE_UNAVAILABLE`); `SOURCE_UNAVAILABLE` is an access-scope status, not a capability absence.
- The Simulink Real-Time route is a bounded R2025b exception only and is never generalized.

## No runtime or project implementation claim

All Management ECU-specific values (variables, module/device identity, transport, endpoints, DAQ/STIM settings, memory/page policy, security policy, thresholds) remain unresolved. No runtime evidence, requirement verdict or coverage is claimed. Every runtime verdict in the coverage matrix is `NOT_EVALUATED`.

## Navigation

Start with the Overview, then the Methodology and State Evidence Model for boundary rules, the Step-by-Step Guide for the future execution framework, the Coverage Matrix for task-level status, the Reference Index for provenance, and the Sol Review for the independent acceptance record.
