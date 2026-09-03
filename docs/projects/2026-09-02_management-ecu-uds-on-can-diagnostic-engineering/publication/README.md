# Publication Package — Management ECU UDS on CAN Diagnostic Engineering

This directory contains publication metadata for the Sol-reviewed Management ECU UDS on CAN diagnostic engineering package.

## Source of truth

- Private source repository: `eariver/Automotive_EE_Engineering_Knowledge`
- Accepted source branch: `work/management-ecu-uds-can-diagnostic-toolchain-20260902`
- Accepted source HEAD: `22cec277e88a416c2d71f696e5c45a2859842384`
- Historical Luna procedure-compilation Ending SHA: `3b5f2cdfc418e46cd2ad4a8509fc77ac50eacc12`
- Vector procedure-authority reviewed SHA: `bcbe4e5b57aa144bfa5cb3d5e86f2a1e5a1274ee`
- MathWorks R2025b procedure-authority reviewed SHA: `2fb38fe40d87a9cb8e7a22f7fe4a1a6a04354187`

## Public package policy

The public package bundles the project-local Methodology, Step-by-Step Guide, Tool/Task Matrix, Execution Guide, Reference Index, locator manifests, project-input scaffolds, reference-coverage artifacts, historical procedure compilation, tool-family procedure files, and the current Sol-reviewed procedure-authority expansion overlay/addendum/pins.

Upstream Vector, MathWorks, AUTOSAR and downstream canonical Knowledge bodies are not copied. Their exact repository/commit/path locators remain in the package.

Internal Luna plans/instructions/evidence, prompts, worklogs, checkpoints, canonical `docs/knowledge/**`, raw vendor HELP, raw standards documents and project-confidential diagnostic values are excluded.

## Current procedure maturity

For `DTR-002` through `DTR-019`:

- `EXACT_PROCEDURE_AVAILABLE`: **11**
- `PARTIAL_PROCEDURE_AVAILABLE`: **5**
- `WORKFLOW_ONLY`: **1**
- `PROJECT_INPUT_REQUIRED`: **1**
- `UNRESOLVED_AUTHORITY`: **0**

Exact bounded tasks are `DTR-002`, `DTR-004`, `DTR-005`, `DTR-007`, `DTR-008`, `DTR-009`, `DTR-010`, `DTR-015`, `DTR-016`, `DTR-018`, and `DTR-019`.

`DTR-006` remains project-design-first. `DTR-013` remains blocked until Management ECU UDS-on-CAN network/transport values are supplied. Remaining partial tasks are `DTR-003`, `DTR-011`, `DTR-012`, `DTR-014`, and `DTR-017`.

The canonical vVIRTUALtarget route for this project is **Integration**. The canonical CANoe SUT consumer route is Integration SUT DLL via node `Configuration > Components > Add`. BSW Emulation remains a separate alternate route.

## Publication status

This branch is a staged, Sol-reviewed publication snapshot. Source-derived files are required to be byte-identical to the accepted Private source snapshot. Public `main` has not been changed or merged by this publication update.
