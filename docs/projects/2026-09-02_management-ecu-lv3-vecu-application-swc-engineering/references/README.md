# Reference locator area

This subtree stores **locators, manifests, coverage matrices, and project reference metadata** used by the Management ECU SWC Methodology and Step-by-Step Guide.

It does not store copied vendor Reviewed Knowledge or bulk standards content.

## Planned authority subdirectories

Luna's first bounded work unit creates these locator manifests:

```text
references/
├── downstream/
│   └── reference-locators.yaml
├── vector/
│   └── reference-locators.yaml
├── mathworks/
│   └── reference-locators.yaml
├── autosar/
│   └── reference-locators.yaml
├── reference-coverage-matrix.yaml
└── reference-coverage-report.md
```

Project-local requirement/calibration/tool baseline locations are tracked in the root `20260902_ManagementECU_SWC_Reference_Index.yaml`; they must not be invented when the project artifact is not yet available.

## Locator rule

For an external technical authority, record at minimum:

```text
authority_type
repository
exact_commit
exact_ref (when applicable)
knowledge_path
section_or_locator
supported_methodology_sections
supported_guide_steps
coverage_posture
retained_boundary
```

Never infer a current upstream `main` or branch head as authority when the downstream repository already pins a proposition-local technical authority commit.

## Authority separation

Keep these planes distinct:

```text
downstream navigation / synthesis metadata
    != vendor Reviewed Knowledge
    != direct AUTOSAR standards Reviewed Knowledge
    != project-specific requirement/design
```
