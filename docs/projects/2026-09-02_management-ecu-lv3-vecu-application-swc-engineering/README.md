# Management ECU Lv3 VECU — Application SWC Toolchain Reference Package

Date: 2026-09-02

This directory is the public packaging area for the Management ECU Lv3 VECU Application SWC Engineering methodology, task-oriented tool/reference navigation, and evidence-backed tool procedures.

## Current publication state

`LUNA_PROCEDURES_REVIEWED_AND_STAGED`

The bounded Luna Tool Procedure Compilation for `TTR-002` through `TTR-010` completed at source HEAD `d0f31a92a6031f3f90cf746dc0a5042739e91f33`. The ending commit is a direct child of the required starting SHA `f58ac9e387dfb98c52117c53672b3c1b2c7d4ccf`, and fixed-head review found only the ten instruction-allowlisted source paths. The six procedure outputs plus the refreshed Matrix and Guide are staged here; Luna worklogs and completion checkpoints remain excluded from the public package.

## Start here

1. `procedures/procedure-coverage-matrix.yaml` — current evidence level and stop boundary for every compiled task `TTR-002` through `TTR-010`.
2. `20260902_ManagementECU_Toolchain_Execution_Reference_Guide.md` — start from an engineering intent and navigate to the phase, tool, operation, input/output and Reviewed Knowledge locator.
3. `20260902_ManagementECU_Tool_Task_Reference_Matrix.yaml` — machine-readable task/tool/reference relation, refreshed with the procedure-compilation result.
4. `20260902_ManagementECU_SWC_Development_Methodology.md` — ownership model, lifecycle and engineering boundaries.
5. `20260902_ManagementECU_SWC_Development_Step_by_Step_Guide.md` — SWC-D0 through SWC-D7 execution order.
6. `20260902_ManagementECU_SWC_Reference_Index.yaml` and `references/` — exact provenance/navigation locators.

## Compiled procedure package

The publication branch contains five tool-family files plus one coverage matrix:

- `procedures/davinci-developer-classic.yaml`
- `procedures/autosar-blockset.yaml`
- `procedures/simulink-stateflow.yaml`
- `procedures/embedded-coder.yaml`
- `procedures/mil-sil.yaml`
- `procedures/procedure-coverage-matrix.yaml`

The compilation contains 10 procedures and 65 operation steps. Evidence-level totals are:

- `EXACT_GUI_PATH_REVIEWED`: 0
- `EXACT_API_OPERATION_REVIEWED`: 10
- `WORKFLOW_OBJECT_OPERATION_REVIEWED`: 35
- `PROCEDURE_PARTIAL`: 11
- `BLOCKED_BY_PROJECT_INPUT`: 9
- `UNRESOLVED_AUTHORITY`: 0

Exact API claims are intentionally bounded to names explicitly present in the frozen Reviewed Knowledge. They do not imply that arguments, GUI routes, project configuration, or a complete reproducible script were reviewed. No exact GUI procedure is claimed for `TTR-002` through `TTR-010`.

## Publication boundary

This package bundles project-local methodology, guides, matrices, locator manifests and accepted procedure compilations. It does **not** copy the underlying Vector, MathWorks, AUTOSAR or downstream canonical Reviewed Knowledge corpus.

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

This is a publication branch staging state. Public `main` is not changed by this package update. See `publication/publication-manifest.yaml` for fixed-source provenance and validation state.
