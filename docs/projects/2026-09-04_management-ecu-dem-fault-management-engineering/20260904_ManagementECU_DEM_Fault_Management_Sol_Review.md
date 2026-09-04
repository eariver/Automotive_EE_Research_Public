# Management ECU DEM Fault Management Engineering — Sol Fixed-Head Review

Date: 2026-09-04

Status: **PASS / CURRENT PACKAGE ACCEPTED**

## Reviewed source

- Repository: `eariver/Automotive_EE_Engineering_Knowledge`
- Luna compilation branch: `work/luna-management-ecu-dem-current-package-compilation-20260904`
- Exact Starting SHA: `b52b51b5546965fdb048ce3c1d8952e993fd153e`
- Luna terminal SHA: `283409a12eca334a619daccdf2733726e503cc09`
- Compare: ahead 2 / behind 0
- Changed paths: exactly the nine allowlisted current-package compilation paths

## Review verdict

The package is accepted without maturity changes relative to Luna's compile proposal. AUTOSAR semantic-depth expansion materially improves the normative state/configuration model, and Vector research materially improves product-local validation/generation, Integration runtime, CANoe, and DiVa route evidence. However, the reviewed sources still do not justify promoting the detailed Configurator DEM object mappings or project execution slices beyond their bounded classifications.

Final procedure availability is therefore:

- `EXACT_PROCEDURE_AVAILABLE`: 1
- `PARTIAL_PROCEDURE_AVAILABLE`: 12
- `WORKFLOW_ONLY`: 3
- `NO_EXPLICIT_PROCEDURE`: 2
- `PROJECT_INPUT_REQUIRED`: 1
- `PROJECT_DESIGN_REQUIRED`: 1
- total: 20

The authoritative machine-readable final classification is `procedures/20260904_ManagementECU_DEM_Final_Availability_Overlay.yaml`.

## Fixed authority

- AUTOSAR CP 4.4.0 semantic depth: `eariver/Research_AUTOSAR_CP_Documents@4eff43bdc4a99f3219104c2b16994a539e0b08eb`
- Vector procedure/runtime/test: `eariver/Research_Vector_Documents@d922812a20ed1e9669fff45f26aa17791254ae65`
- MathWorks R2025b procedure authority: `eariver/Research_MathWorks_Documents@2fb38fe40d87a9cb8e7a22f7fe4a1a6a04354187`

## Retained closure boundaries

1. Detailed DaVinci Configurator Classic 6.3.10 object-by-object realization is not established for several DEM semantic areas. AUTOSAR ECUC names must not be converted into guessed Vector GUI routes.
2. Dem/NvM Event Memory Blocks Assistant is accepted only as bounded mapping evidence.
3. vVIRTUALtarget `Integration` remains the canonical virtual-ECU route for this project.
4. Tester-visible DTC behavior is not direct proof of internal debounce, event-memory, or NvM representation.
5. Internal DEM observability requires an explicitly project-authorized instrumentation bridge.
6. Actual runtime/test execution requires project artifacts, diagnostic description, stimulus, expected transition, and acceptance criteria.
7. The absence of one universal cross-product Test Unit package/build/runtime contract is retained as a documentation-scope negative, while DiVa generation and CANoe import/execution remain valid product-local routes.

## Project gates

- DFM-000 remains project-input-first.
- DFM-002 remains project-design-first.
- Project-specific values and execution evidence must not be synthesized from generic vendor/AUTOSAR procedures.

## Publication disposition

The current package is approved for staging to `eariver/Automotive_EE_Research_Public` on the prepared publication branch, provided source-derived files are byte-identical to this accepted Private source and internal Luna material, raw sources, canonical upstream `docs/knowledge/**`, and confidential project values remain excluded. Public `main` remains human-gated.
