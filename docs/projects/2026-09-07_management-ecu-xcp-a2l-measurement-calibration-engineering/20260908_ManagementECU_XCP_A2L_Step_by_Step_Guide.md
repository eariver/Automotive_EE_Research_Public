# Management ECU XCP/A2L Step-by-Step Guide

Date: 2026-09-08
Status: future project execution framework — not a project implementation result

Nothing below is reported as completed. Each step distinguishes reviewed authority, the project decision still required, and the future evidence still required.

## 1. Decide scope and ownership

- Reviewed authority: seven-lane decomposition and master/client versus server/slave boundaries.
- Project decision required: measurement/calibration consumers; artifact, configuration and runtime owners; change-control ownership.
- Future evidence required: accepted symbolic ownership record. No endpoint values.

## 2. Decide the A2L producer and description version

- Reviewed authority: bounded post-code-generation A2L export and selectable description versions.
- Project decision required: producer toolchain; A2L format/version; module/object identity policy; artifact owner, location and regeneration trigger.
- Future evidence required: actual generated A2L, generation log, manifest and provenance.

## 3. Fix build and address provenance

- Reviewed authority: product-local symbol/address replacement and ASAP2 update surfaces only.
- Project decision required: build identity; map/symbol/executable artifacts; resolution source; update cadence; consumer reload trigger.
- Future evidence required: build/symbol hashes, address update log, reload/rebind record.
- Note: `XCP-006` is `UNRESOLVED_RETAINED`; vendor-local workflows do not close the generic lifecycle.

## 4. Decide consumer, import and reload policy

- Reviewed authority: product-local import/update surfaces only.
- Project decision required: consumer tool and version; accepted A2L artifact; reload/update policy; description owner.
- Future evidence required: import/parse result, warnings/limitations record, reload revision binding.
- Note: `XCP-007` is `UNRESOLVED_RETAINED`; import success proves no server or session.

## 5. Select and realize the target-side server

- Reviewed authority: running Simulink Real-Time target as server only in the bounded R2025b route.
- Project decision required: target runtime; server implementation/product; resource configuration; server owner; build/deployment boundary.
- Future evidence required: server configuration/source artifact, compile/link and deployment result, running endpoint observation.
- Note: `XCP-009` is `UNRESOLVED_RETAINED` for generic/non-SLRT and Management ECU targets.

## 6. Align protocol, transport and endpoints

- Reviewed authority: bounded CAN/CAN FD/Ethernet/TCP/UDP and profile/version surfaces; SLRT UDP only for the bounded route.
- Project decision required: protocol/profile version; transport family; CAN or IP endpoint; backend/device/channel; A2L transport metadata policy.
- Future evidence required: matching client/server transport configuration, backend/driver readiness, endpoint connectivity evidence.
- Note: A2L version never selects an XCP protocol version; transport support never implements a server.

## 7. Confirm live-session prerequisites

- Reviewed authority: exact SLRT prerequisite closure for that product/runtime only.
- Project decision required: compatible target-aware A2L; running server; selected client; matched endpoints; connection lifecycle and ownership.
- Future evidence required: connect/disconnect trace, server/client state observations, error and recovery evidence.
- Note: `XCP-011` is `UNRESOLVED_RETAINED` for generic targets; tutorial online/ready is not session evidence.

## 8. Design DAQ, events and timing

- Reviewed authority: AUTOSAR safe frontier (DAQ direction, list/ODT/entry/DTO identities, event versus communication channel, static/dynamic configuration, event/timestamp/counter surfaces).
- Project decision required: DAQ lists, event channels, periods, prescalers, priorities, timestamp policy, timing owner.
- Future evidence required: configured manifest, acquisition trace, timing measurements, loss/error observations.
- Note: configured timing is never application scheduling and never measured timing.

## 9. Design STIM and calibration-write policy

- Reviewed authority: AUTOSAR STIM/calibration boundary with `DAQ != STIM != calibration memory write`; pure-STIM mapping ambiguity retained.
- Project decision required: STIM adoption, writable resources, write/online-calibration policy, operation owner, rollback and safety policy.
- Future evidence required: command/result trace, before/after read-back, rejection/error behavior, rollback evidence.

## 10. Design memory, pages and writeability

- Reviewed authority: AUTOSAR page query/switch boundary; `DAQ RESUME != calibration page/value persistence`.
- Project decision required: memory segments, calibration pages, page-switching policy, writable ranges, initial-value and persistence policy.
- Future evidence required: memory-map binding, page/segment transition trace, write/read-back result, reset/persistence observation where required.

## 11. Design security and resource policy

- Reviewed authority: AUTOSAR Seed&Key purpose and symbolic ownership only; secret-material guard binding.
- Project decision required: protected resources, Seed&Key requirement decision, symbolic algorithm/credential ownership, access policy, secret-handling boundary. No secret values are ever stored in the repository.
- Future evidence required: non-secret authorization result trace, allowed/denied behavior, security error observations.

## 12. Confirm tool roles and CANape procedure coverage

- Reviewed authority: CANape PROC-01..04 partial; PROC-05..07 `SOURCE_UNAVAILABLE`; aggregate partial.
- Project decision required: tool selection and versions, role allocation, whether CANape is required, cross-tool handoffs.
- Future evidence required: none at present beyond the selection record; detailed MAP/memory/security procedure is unavailable on access scope, not on capability grounds.

## 13. Collect runtime evidence

- Reviewed authority: none beyond the bounded SLRT reference route.
- Project decision required: target/runtime environment and stimulus plan.
- Future evidence required: generated/address-resolved artifacts, deploy result, connection, DAQ/STIM/read/write observations, synchronization and authorization outcomes, persistence where required.

## 14. Compare with requirements and form verdict and coverage

- Reviewed authority: none; verdict and coverage are project evidence planes.
- Project decision required: traceability rules, verdict rules, coverage targets. No numeric threshold is pre-selected here.
- Future evidence required: requirement comparison, verdict assignment and coverage assessment as separate records.
