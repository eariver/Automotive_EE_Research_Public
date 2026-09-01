# Management ECU SWC authority/reference-index coverage report

- Status: **COMPILED**
- Branch: `work/luna-management-ecu-swc-authority-index-20260902`
- Starting SHA: `997d09d57ca3246c5323c2e366598bd9f7a9f50e`
- Scope: existing Reviewed Knowledge navigation compilation only
- New technical research: **NO**
- external_source_access_count: **0** (no new source collection; only exact-pinned frozen Reviewed Knowledge was read)

## Locator coverage

| Authority plane | Locator count |
|---|---:|
| downstream | 24 |
| vector | 12 |
| mathworks | 15 |
| autosar | 20 |
| **total** | **71** |

## Coverage posture

| Coverage posture | Count |
|---|---:|
| REVIEWED_ROUTE_AVAILABLE | 47 |
| BOUNDED_ROUTE_AVAILABLE | 10 |
| NO_EXPLICIT_MAPPING | 3 |
| PROJECT_SPECIFIC_DESIGN | 2 |
| PROJECT_INPUT_REQUIRED | 3 |
| PROJECT_ARTIFACT | 2 |
| PROCESS_RULE | 3 |
| UNRESOLVED_AUTHORITY | 1 |

## Explicit unresolved or missing routes

- `DS-016`: Stop this affected route here; do not use current upstream documentation or infer CANape behavior from CANoe/VNT/XCP similarity.

## NO_EXPLICIT_MAPPING

- `DS-007`, `DS-008`, `DS-017`
- These rows are navigation/projection gaps only; they are not capability-negative evidence.
- CG-009 retains its NO_EXPLICIT_MAPPING downstream posture while exact direct AUTOSAR mode/lifecycle locators are listed separately.
- CG-008 and CG-006 retain the same non-negative interpretation.

## PROJECT_INPUT_REQUIRED

- `DS-PROJ-001`, `DS-PROJ-002`, `DS-PROJ-003`
- Project requirement baseline, actual tool/version combination and project calibration values must be supplied by project control.

## Boundary controls

- application architecture != AUTOSAR contract != behavior model != generated implementation != production RTE/BSW/OS != VECU runtime
- DiagMgr != DCM != DEM
- project counter/checksum != AUTOSAR E2E
- native CAN BUS_OFF != project BUS_FAILED_LATCHED
- MIL != SIL != VECU/HIL/physical-SUT evidence
- MathWorks RTE stub != production MICROSAR RTE
- vendor realization != direct AUTOSAR standards authority
- shared AUTOSAR support != interoperability proof

## Completion checks

| Check | Result |
|---|---|
| Every external Methodology/Guide dependency represented | PASS |
| External locator has exact repository + commit + path + section | PASS |
| Proposition identity only from explicit downstream records | PASS |
| No current upstream head used | PASS |
| Project-specific rules remain project-specific | PASS |
| Missing/unresolved routes explicit | PASS |
| Per-authority manifests and root index agree | PASS |
| Methodology and Guide byte-unchanged | PASS |
| Canonical Knowledge and authority registry unchanged | PASS |
| Allowlist-only output set | PASS |

The Methodology and Step-by-Step Guide remain navigation inputs and were not edited. Stop after this compilation; no downstream promotion, C4 work, PR work or main merge is included.
