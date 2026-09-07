# Publication — Management ECU Communication Mode & Network Management Engineering

Status: **SOL_REVIEWED_STAGED**

This dedicated branch contains the public projection of the Sol-reviewed Management ECU Communication Mode & Network Management current engineering package.

## Accepted Private source

- repository: `eariver/Automotive_EE_Engineering_Knowledge`
- branch: `work/sol-management-ecu-communication-mode-network-management-current-package-review-20260907`
- accepted source HEAD: `a8dd173415716a895c9787e2bf8a5dea9fd3051c`
- Luna current-package candidate: `136e5250efb7a932fc286e64405997fbce9fe801`
- accepted baseline: `56f753e5f605f7441b957490c36080f067bb0807`

Sol verdict: `SOL_CURRENT_PACKAGE_REVIEW_PASS`.

## Public projection policy

The public package carries the reviewed reader-facing current-package documents and a compact public machine-readable coverage projection.

The following Private execution-oriented material is intentionally not copied:

- Luna terminal checkpoint;
- large internal procedure-coverage matrix;
- large internal tool/task/reference matrix;
- historical baseline and research-gap artifacts;
- Luna prompts, worklogs and observations;
- raw Vector HELP, private Drive corpus bytes and raw AUTOSAR documents.

The compact public matrix preserves the accepted 18-task classifications and exact authority identities needed for public consumption without exposing internal execution material.

## Authority

- AUTOSAR semantic authority: `eariver/Research_AUTOSAR_CP_Documents@a7d063d4fb020e565497388c2c6cea5c2605a1ed`
- Vector/MICROSAR authority: `eariver/Research_Vector_Documents@9b1e1a1fb172cb43466b89f07a1c22f9a8e00990`
- retained older AUTOSAR context: `eariver/Research_AUTOSAR_CP_Documents@938ac4af696d263019ebdc61106a444447e15c4d`

## Fixed Vector ten-slice summary

```text
EXACT_PRODUCT_PROCEDURE_AVAILABLE     0
PARTIAL_PRODUCT_PROCEDURE_AVAILABLE   5
SURFACE_ONLY                          1
NO_EXPLICIT_REVIEWED_PROCEDURE        4
OUTSIDE_AUTHORIZED_PRODUCT_SCOPE      0
---------------------------------------
total                                10
```

No aggregate task is promoted to exact procedure availability merely because an exact sub-procedure exists.

## Retained gaps

Project-specific ComM users/channels, mode and inhibition policy, Nm/CanNm policy/timers, PNC adoption/mapping, gateway role, wakeup sources, controller/transceiver identities, bus-off recovery settings, BswM rules/actions, COM I-PDU Group realization, application-availability criteria, target/runtime scope, timing requirements and acceptance thresholds remain unresolved project input/design.

Execution evidence also remains separate. No runtime/build/validation result, verdict or coverage is published as though it existed.

## Main branch gate

This package is published only on:

`publish/management-ecu-communication-mode-network-management-engineering-20260907`

Public `main` is not merged or modified by this publication workflow.
