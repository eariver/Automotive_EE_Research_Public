# Management ECU XCP/A2L Current Package Overview

Date: 2026-09-08
Status: `SOL_CURRENT_PACKAGE_REVIEW_PASS` projection
Private authority: `eariver/Automotive_EE_Engineering_Knowledge@ff096484c8f36bc59a850b1b36575f9cf34ac279`

## Purpose

This overview summarizes the Sol-reviewed Management ECU XCP/A2L Measurement & Calibration current package for public readers. It adds no new technical proposition beyond the accepted private package. Six large private YAML artifacts are used as authority for this synthesis; they are not raw-copied into the public repository.

## Seven-lane lifecycle

The package decomposes the chain into seven lanes preserved from the fixed R2D authority (`6ab70451`, 26 evidence rows, 8 retained candidates):

1. description producer
2. address resolution
3. consumer/master
4. transport
5. server/slave endpoint
6. live session
7. ownership/lifecycle

A stronger result in one lane never silently completes another lane.

## 18-task scope

`XCP-001` through `XCP-018` are retained exactly once. The compact coverage matrix (`matrices/20260908_ManagementECU_XCP_A2L_Public_Coverage_Matrix.yaml`) is mechanically derived from the private Requirement Catalog, Gap Status and Validation Matrix.

## Reviewed safe frontier

- Standards/semantic authority, product procedure authority, project input/design and execution evidence are independent planes.
- Configuration, runtime evidence, requirement verdict and coverage are never merged.
- Product procedure is never runtime proof.

## AUTOSAR XCP-012..015 overlay

Only the Sol-reviewed safe frontier from `Research_AUTOSAR_CP_Documents@d3de1f71` is reflected:

- `XCP-012`: DAQ slave-to-master direction; `DAQ list != ODT != ODT entry != DTO`; `XcpEventChannel != XcpCommunicationChannel`; static versus dynamic DAQ configuration surfaces; event/timestamp/timing configuration ownership. Detailed dynamic-DAQ state remains a conditional ASAM dependency only if load-bearing.
- `XCP-013`: STIM as the inverse DAQ direction; bypass as DAQ+STIM without identity collapse; online calibration kept distinct. `DAQ != STIM != calibration memory write` is mandatory. The pure-STIM DTO/PDU wording ambiguity is retained as-is and is never guessed away.
- `XCP-014`: online calibration read/write at module-feature level; master page query and slave page-switch request; ECUC-scope negative for detailed page layout. `DAQ RESUME != calibration page/value persistence`.
- `XCP-015`: Seed&Key support purpose as protection handling and secure slave-memory access; symbolic resource/configuration ownership only. Actual enablement and resource policy are project design; successful authorization is execution evidence. No secret material is included. Detailed protection behavior is a conditional ASAM dependency only if load-bearing.

No ASAM-complete protocol coverage is claimed.

## CANape XCP-016 partial coverage

From `Research_Vector_Documents@f75bb98`:

- `CANAPE-PROC-01` project creation/opening: `PARTIAL_PRODUCT_PROCEDURE_AVAILABLE`
- `CANAPE-PROC-02` A2L/XCP device/transport setup: `PARTIAL_PRODUCT_PROCEDURE_AVAILABLE`
- `CANAPE-PROC-03` measurement mode / Polling / DAQ setup: `PARTIAL_PRODUCT_PROCEDURE_AVAILABLE`
- `CANAPE-PROC-04` calibration editing / parameter workflow: `PARTIAL_PRODUCT_PROCEDURE_AVAILABLE`
- `CANAPE-PROC-05` linker MAP / A2L address update: `SOURCE_UNAVAILABLE`
- `CANAPE-PROC-06` memory/address synchronization / mapping: `SOURCE_UNAVAILABLE`
- `CANAPE-PROC-07` Seed&Key / protection setup: `SOURCE_UNAVAILABLE`

Aggregate: `PARTIAL_PRODUCT_PROCEDURE_AVAILABLE`.

`SOURCE_UNAVAILABLE` records authentication-gated documentation/access scope and is never a product-capability absence claim. The CANape tutorial `online/ready` state, measurement-mode selection, calibration editing and parameter-file handling prove no target server, live binding, target write, persistence or authorization.

## Retained XCP-006/007/009/011 gaps

- `XCP-006` build/map/symbol/address provenance and A2L update lifecycle: `UNRESOLVED_RETAINED`
- `XCP-007` consumer import/update/reload and live-binding lifecycle: `UNRESOLVED_RETAINED`
- `XCP-009` generic/non-Simulink-Real-Time target-side slave/server implementation: `UNRESOLVED_RETAINED`
- `XCP-011` generic live-session prerequisites, connection lifecycle and endpoint binding: `UNRESOLVED_RETAINED`

None is closed by neighboring CANape, CANoe, AUTOSAR, MathWorks or dSPACE evidence.

## Bounded Simulink Real-Time exception

```text
build real-time application
 -> target-aware A2L
 -> running Simulink Real-Time target/application as XCP server
 -> third-party calibration client
 -> UDP
 -> live measurement/calibration
```

This is a Simulink Real-Time R2025b bounded positive route only. It is never generalized to generic Management ECU, generic Embedded Coder, AUTOSAR, MICROSAR or a CANape target/server.

## Project design blockers

Every concrete Management ECU selection remains unresolved: consumers, owners, A2L identity, producer/consumer choice, server implementation, transport/endpoints, DAQ/STIM design, memory/page design, security policy and acceptance rules. Vendor and standards authority never selects these values.

## Runtime evidence boundary

The public package contains no generated A2L, resolved addresses, build/deploy result, running server, live connection, acquisition trace, write/read-back, synchronization, authorization, persistence, verdict or coverage evidence. All runtime verdicts are `NOT_EVALUATED`. Runtime PASS count is 0.
