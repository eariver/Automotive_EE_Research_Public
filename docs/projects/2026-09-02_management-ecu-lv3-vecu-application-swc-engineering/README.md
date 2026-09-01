# Management ECU Lv3 VECU — Application SWC Toolchain Reference Package

Date: 2026-09-02

This directory is the public packaging area for the Management ECU Lv3 VECU Application SWC Engineering methodology, task-oriented tool/reference navigation, and evidence-backed tool procedures.

## Current publication state

`PREPARED_AWAITING_LUNA_PROCEDURES`

The stable methodology/reference materials are being staged now. The `procedures/` family will be added only after the bounded Luna Tool Procedure Compilation (`TTR-002` through `TTR-010`) is complete and passes fixed-head Sol review.

## Start here

1. `20260902_ManagementECU_Toolchain_Execution_Reference_Guide.md` — start from an engineering intent and navigate to the phase, tool, operation, input/output and Reviewed Knowledge locator.
2. `20260902_ManagementECU_Tool_Task_Reference_Matrix.yaml` — machine-readable task/tool/reference relation.
3. `20260902_ManagementECU_SWC_Development_Methodology.md` — ownership model, lifecycle and engineering boundaries.
4. `20260902_ManagementECU_SWC_Development_Step_by_Step_Guide.md` — SWC-D0 through SWC-D7 execution order.
5. `20260902_ManagementECU_SWC_Reference_Index.yaml` and `references/` — exact provenance/navigation locators.

## Publication boundary

This package bundles project-local methodology, guides, matrices and locator manifests. It does **not** copy the underlying Vector, MathWorks, AUTOSAR or downstream canonical Reviewed Knowledge corpus.

For those authorities, the bundled locator manifests preserve the exact repository / commit or ref / path / section needed to resolve the source. A locator is provenance; it is not a claim that the referenced repository is publicly accessible.

The following are intentionally not published here:

- Luna prompts, plans, worklogs and checkpoints;
- canonical `docs/knowledge/**` content;
- upstream vendor/standards Reviewed Knowledge bodies;
- raw vendor HELP or raw standards PDFs;
- generated production C/ARXML/binaries;
- confidential raw project specifications.

## Key semantic boundaries

- application architecture != AUTOSAR contract != behavior model != generated implementation != production RTE/BSW/OS integration;
- DiagMgr != DCM != DEM;
- project counter/checksum != AUTOSAR E2E;
- native CAN BUS_OFF != project BUS_FAILED_LATCHED;
- MIL != SIL != VECU/HIL/physical-SUT evidence;
- verdict != coverage;
- code generation != compile != link;
- MathWorks RTE stub != production MICROSAR RTE.

See `publication/publication-manifest.yaml` for source snapshot and packaging status.
