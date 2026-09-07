# Management ECU Communication Mode & Network Management
# Execution Reference Guide

Date: 2026-09-07 JST
Status: LUNA_CURRENT_PACKAGE_COMPILED_PROPOSAL
Purpose: authority navigation and evidence planning; no execution is claimed

## Exact authority routes

- Accepted baseline: eariver/Automotive_EE_Engineering_Knowledge@56f753e5f605f7441b957490c36080f067bb0807
- AUTOSAR semantic overlay: eariver/Research_AUTOSAR_CP_Documents@a7d063d4fb020e565497388c2c6cea5c2605a1ed
- Vector procedure overlay: eariver/Research_Vector_Documents@9b1e1a1fb172cb43466b89f07a1c22f9a8e00990

## Generic workflow support only

    dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
    dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
    dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"

These generic workflows are not a CNM-specific procedure and do not imply
artifact, build, runtime transition, recovery, availability, verdict or coverage.

## Evidence planes

1. requirement and communication demand
2. symbolic ComM user/request/channel/target
3. ComM and BusSM indication
4. CanSM state/lower-layer/bus-off
5. Nm/CanNm request/protocol
6. PNC identity/aggregation
7. BswM action and COM I-PDU Group
8. validation/generation/artifact/build
9. runtime transition, bus/wakeup/recovery/availability/timing
10. requirement comparison, verdict and coverage

## Documentation-scope negatives

Communication User CRUD/channel connection is not exact ComM aggregation or mode
policy. PNC-ID counting is not full PNC realization. Bus Controller configuration
is not CanSM configuration. BswM Communication Control is not complete cross-layer
or application-availability procedure. Generic validate/generate/schema workflow
is not CNM-specific. A missing page-local procedure is not capability absence.

## Stop and handoff

Stop at the reviewed product, project-input/design or execution frontier. Hand off
to Sol fixed-head review; do not begin publication, implementation, runtime
verification or main merge.
