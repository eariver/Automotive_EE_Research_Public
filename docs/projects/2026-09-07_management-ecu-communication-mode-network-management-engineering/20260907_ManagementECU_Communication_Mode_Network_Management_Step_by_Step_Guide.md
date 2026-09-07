# Management ECU Communication Mode & Network Management
# Step-by-Step Guide

Date: 2026-09-07 JST
Status: LUNA_CURRENT_PACKAGE_COMPILED_PROPOSAL

This is an engineering navigation and handoff guide from fixed reviewed authority.
It is not an exact Vector procedure and does not claim executed configuration.

## Safe sequence

1. Read the accepted baseline and exact authority tuples; confirm CNM-001 through
   CNM-018.
2. For each task, consume the reviewed semantic boundary and fixed product
   surface or negative, keep project input/design unresolved, and stop before
   runtime claims.
3. Promote only when task handoff evidence is supplied by its owner.


## CNM-001 — Communication-state and network-management scope, ownership and handoff baseline

- Lifecycle / owner: SCOPE_AND_OWNERSHIP / Management ECU integration / communication-state and network-management plane
- Reviewed semantic requirement: Compile plane ownership and retain data-plane, OS/RTE and network-state separation.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed CNM product procedure for scope ownership.
- Project input: PROJECT_INPUT_REQUIRED; actual_comm_users, application_and_bsw_communication_demand_policy
- Project design: NOT_CURRENTLY_REQUIRED; none listed
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Accepted communication/network requirements and ownership allocation
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: Application/BSW communication demand != ComM user/channel state; data-plane communication != network-state management.

## CNM-002 — Application/BSW communication demand to ComM user abstraction

- Lifecycle / owner: COMMUNICATION_DEMAND_TO_COMM_USER / Application/BSW demand owner and ComM user boundary
- Reviewed semantic requirement: ComMUser and ComM_UserHandleType are requestor identities; ComM_RequestComMode is the user request; newest request overwrites older request.
- Product procedure status: PARTIAL_PRODUCT_PROCEDURE_AVAILABLE; Communication Users supports add/edit/remove and individual channel connection; it does not establish demand allocation or runtime behavior.
- Project input: PROJECT_INPUT_REQUIRED; application_and_bsw_communication_demand_policy, actual_comm_users
- Project design: NOT_CURRENTLY_REQUIRED; none listed
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project demand allocation and ComM user identity decision
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: Application/BSW communication demand != ComM user != ComM channel; COMM_SILENT_COMMUNICATION is not a user-request value.

## CNM-003 — ComM user/channel mapping and request aggregation

- Lifecycle / owner: COMM_USER_CHANNEL_MAPPING_AND_AGGREGATION / ComM user/channel aggregation
- Reviewed semantic requirement: ComMUser, ComMUserPerChannel, ComMUserChannel and ComMChannel are distinct; channel target and current BusSM indication remain separate.
- Product procedure status: PARTIAL_PRODUCT_PROCEDURE_AVAILABLE; Communication User channel checkbox is partial mapping support; exact aggregation, multiplicity and bus-mapping procedure is not reviewed.
- Project input: PROJECT_INPUT_REQUIRED; actual_comm_users, comm_channels_and_bus_mapping
- Project design: NOT_CURRENTLY_REQUIRED; none listed
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project ComM user/channel mapping and aggregation policy
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: ComM user != ComM channel; request aggregation != channel target != BusSM actual-mode indication.

## CNM-004 — ComM channel modes, request/release and indication semantics

- Lifecycle / owner: COMM_CHANNEL_MODE_SEMANTICS / ComM channel state and mode indication
- Reviewed semantic requirement: Keep user request, stored request, channel target evaluation, BusSM request, actual mode indication and user/BswM indication separate.
- Product procedure status: SURFACE_ONLY; Related ComM/user surface exists, but no page-local aggregate mode request/release/indication procedure; surface only.
- Project input: NOT_CURRENTLY_REQUIRED; none listed
- Project design: PROJECT_DESIGN_REQUIRED; comm_mode_policy, comm_inhibition_or_limitation_policy, mode_indication_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project ComM mode, inhibition and indication design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: COMM_SILENT_COMMUNICATION != user-requested mode; ComM mode != CanSM state != CanNm state != physical bus.

## CNM-005 — CommunicationAllowed, inhibition and limitation policy

- Lifecycle / owner: COMM_POLICY_INHIBITION_AND_LIMITATION / ComM policy, CommunicationAllowed and inhibition/limitation boundary
- Reviewed semantic requirement: ComM_CommunicationAllowed is channel-level control; channel limitation, ECU limitation and wakeup inhibition remain distinct.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed product procedure for CommunicationAllowed, inhibition or limitation realization.
- Project input: NOT_CURRENTLY_REQUIRED; none listed
- Project design: PROJECT_DESIGN_REQUIRED; comm_inhibition_or_limitation_policy, communication_allowed_policy, wakeup_inhibition_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project ComM policy design and acceptance owner
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: CommunicationAllowed != physical-bus availability; channel limitation != ECU limitation != wakeup inhibition.

## CNM-006 — ComM/Nm/BusNm request and notification direction

- Lifecycle / owner: COMM_NM_BUSNM_DIRECTIONAL_HANDOFF / ComM / Nm Interface / BusNm handoff
- Reviewed semantic requirement: Retain ComM -> Nm -> BusNm and BusNm -> Nm -> ComM as opposite request and notification paths.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed product mapping procedure for the directional handoff.
- Project input: PROJECT_INPUT_REQUIRED; nm_cannm_adoption_per_channel
- Project design: PROJECT_DESIGN_REQUIRED; active_or_passive_nm_policy, nm_coordination_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project Nm/CanNm adoption and request/indication design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: ComM -> Nm -> BusNm request != BusNm -> Nm -> ComM notification; Nm != CanNm.

## CNM-007 — CanSM communication-state sequencing

- Lifecycle / owner: CANSM_COMMUNICATION_STATE_SEQUENCING / CanSM CAN communication-state manager
- Reviewed semantic requirement: Keep CanSM request, stored trigger, CanSM_MainFunction processing, CanIf control/indication, state update and upper notifications distinct.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed CanSM state-machine configuration procedure.
- Project input: PROJECT_INPUT_REQUIRED; comm_channels_and_bus_mapping
- Project design: PROJECT_DESIGN_REQUIRED; can_bus_off_recovery_policy, can_state_transition_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project CanSM channel and bus-off recovery design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: CanSM request != main-function processing != CanIf indication != physical controller completion.

## CNM-008 — CanSM lower-layer handoff, wakeup and bus-off boundary

- Lifecycle / owner: CANSM_LOWER_LAYER_WAKEUP_AND_BUS_OFF / CanSM / CanIf / CanTrcv / CAN controller and wakeup integration
- Reviewed semantic requirement: Keep CanSM_ControllerBusOff, main-function processing, CanIf handoff, controller/transceiver status, WUVALIDATION and EcuM validation separate; retain recovery controls without values.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed CanSM/CanTrcv/controller procedure; Configuring Bus Controllers is not promoted to CanSM.
- Project input: PROJECT_INPUT_REQUIRED; wakeup_sources, can_transceiver_selective_wakeup_adoption
- Project design: PROJECT_DESIGN_REQUIRED; can_bus_off_recovery_policy, wakeup_validation_owner_and_reaction_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project lower-layer, wakeup and bus-off recovery design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: CanTrcv WUF/status != CanSM wakeup-validation phase != EcuM wakeup validation/result; bus-off callback != recovered bus.

## CNM-009 — Nm Interface adaptation and optional coordination

- Lifecycle / owner: NM_INTERFACE_ADAPTATION_AND_COORDINATION / Nm Interface and optional NM Coordinator
- Reviewed semantic requirement: Use Nm Interface as bus-independent adaptation and optional coordination without absorbing CanNm protocol state.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed Nm Interface/coordinator product procedure.
- Project input: PROJECT_INPUT_REQUIRED; nm_cannm_adoption_per_channel
- Project design: PROJECT_DESIGN_REQUIRED; active_or_passive_nm_policy, nm_coordination_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project channel adoption and optional coordination design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: Nm Interface adaptation/coordinator != bus-specific CanNm state machine.

## CNM-010 — CanNm protocol modes, NM-PDU processing and timers

- Lifecycle / owner: CANNM_PROTOCOL_STATE_AND_TIMING / CanNm bus-specific NM protocol
- Reviewed semantic requirement: Keep CanNm operational/protocol modes, NM-PDU processing and timers separate from ComM modes, CanSM state and OS scheduling.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed CanNm protocol/timer/request procedure.
- Project input: PROJECT_INPUT_REQUIRED; nm_cannm_adoption_per_channel
- Project design: PROJECT_DESIGN_REQUIRED; active_or_passive_nm_policy, cannm_timer_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project CanNm channel policy and timing design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: CanNm requested/released != operational mode != internal protocol state; CanNm timer != OS schedule.

## CNM-011 — CanNm request/release, passive-start and conditional Car Wakeup

- Lifecycle / owner: CANNM_REQUEST_RELEASE_PASSIVE_START_AND_CAR_WAKEUP / CanNm request/release and conditional Car Wakeup boundary
- Reviewed semantic requirement: Keep CanNm_NetworkRequest, NetworkRelease and PassiveStartUp asynchronous services separate from operational/internal protocol state; reuse GC10 Car Wakeup.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed CanNm request/release/passive-start procedure; ComMNmVariant is not promoted.
- Project input: PROJECT_INPUT_REQUIRED; wakeup_sources
- Project design: PROJECT_DESIGN_REQUIRED; active_or_passive_nm_policy, cannm_request_release_policy, passive_start_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project CanNm/wakeup policy design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: CanNm request/release != operational mode != EcuM wakeup validation; Car Wakeup is reused, not reopened.

## CNM-012 — EcuM wakeup-source validation and lifecycle reaction

- Lifecycle / owner: ECUM_WAKEUP_VALIDATION_AND_LIFECYCLE_REACTION / EcuM wakeup source, validation and lifecycle reaction
- Reviewed semantic requirement: Keep wakeup source, CanTrcv indication, CanSM validation phase and EcuM result/lifecycle reaction separate.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed EcuM wakeup validation procedure.
- Project input: PROJECT_INPUT_REQUIRED; wakeup_sources
- Project design: PROJECT_DESIGN_REQUIRED; wakeup_validation_owner_and_reaction_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project wakeup-source and validation-reaction design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: CanTrcv WUF/status != CanSM wakeup-validation phase != EcuM wakeup validation/result.

## CNM-013 — EcuM/BswM startup, shutdown and sleep lifecycle

- Lifecycle / owner: ECUM_BSWM_STARTUP_SHUTDOWN_AND_SLEEP / EcuM lifecycle and BswM mode arbitration/control
- Reviewed semantic requirement: Keep EcuM lifecycle, BswM arbitration/action lists and startup/shutdown/sleep policy as separate owners.
- Product procedure status: NO_EXPLICIT_REVIEWED_PROCEDURE; No explicit reviewed lifecycle product procedure.
- Project input: NOT_CURRENTLY_REQUIRED; none listed
- Project design: PROJECT_DESIGN_REQUIRED; startup_shutdown_sleep_policy, bswm_rule_and_action_list_realization
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project lifecycle and BswM mode-control design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: BswM arbitration/action list != ComM PNC ownership != EcuM lifecycle state.

## CNM-014 — PNC identity, EIRA/ERA, ComM PNC state and conditional gateway demand

- Lifecycle / owner: PNC_IDENTITY_AND_RUNTIME_DEMAND / System Template PNC identity / CanNm PN processing / ComM PNC state
- Reviewed semantic requirement: Keep PNC identity/derivation, EIRA/ERA, ComM PNC state, selective wakeup and gateway demand distinct.
- Product procedure status: PARTIAL_PRODUCT_PROCEDURE_AVAILABLE; ComMPncID Counting Mode with NM_MESSAGE and PNC_VECTOR is partial ID derivation, not full PNC realization.
- Project input: PROJECT_INPUT_REQUIRED; pnc_adoption_and_mapping, pnc_gateway_role
- Project design: NOT_CURRENTLY_REQUIRED; none listed
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project PNC adoption, mapping and gateway-role decision
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: PNC ID derivation != EIRA/ERA runtime aggregation != ComM PNC state != selective wakeup; PNC adoption != gateway responsibility.

## CNM-015 — BswM arbitration to COM I-PDU Group and application-availability handoff

- Lifecycle / owner: BSWM_COM_IPDU_GROUP_AND_APPLICATION_AVAILABILITY_HANDOFF / BswM policy handoff / COM I-PDU Group / application communication availability
- Reviewed semantic requirement: Keep BswM indications/rule evaluation/action ordering, BswMPduGroupSwitch and COM I-PDU Group processing separate from application availability and physical bus state.
- Product procedure status: PARTIAL_PRODUCT_PROCEDURE_AVAILABLE; Communication Control exposes I-PDU Groups, NM Communication and J1939 State; partial surface, not complete cross-layer mapping.
- Project input: NOT_CURRENTLY_REQUIRED; none listed
- Project design: PROJECT_DESIGN_REQUIRED; bswm_rule_and_action_list_realization, com_ipdu_group_activation_policy, application_availability_criteria
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project BswM, COM I-PDU Group and application-availability design
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: BswM action != ownership; BswMPduGroupSwitch != application availability; COM I-PDU Group state != ComM mode != CanSM state.

## CNM-016 — Vector/MICROSAR configuration, validation, generation and build handoff

- Lifecycle / owner: PRODUCT_CONFIGURATION_VALIDATION_GENERATION_AND_BUILD_HANDOFF / Vector/MICROSAR product workflow and project configuration ownership
- Reviewed semantic requirement: Keep configured intent, validation, generation/schema, artifact, compile/link, deployed binary and runtime transition distinct.
- Product procedure status: PARTIAL_PRODUCT_PROCEDURE_AVAILABLE; Generic dvcfg-b validate/generate/generate-schema and CLI/CI context only; no complete CNM-specific chain.
- Project input: PROJECT_INPUT_REQUIRED; actual_comm_nm_cansm_cannm_project_scope, actual_vector_microsar_package_and_release
- Project design: PROJECT_DESIGN_REQUIRED; configuration_scope_and_artifact_manifest_policy
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Project tool/package selection and authorized CNM product evidence
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: Generic validation/generation/schema workflow != CNM-specific procedure != compile/link != runtime transition.

## CNM-017 — Management ECU communication/network policy and project design register

- Lifecycle / owner: PROJECT_POLICY_AND_DESIGN / Management ECU requirements, architecture and network-policy ownership
- Reviewed semantic requirement: Record project-owned identities, policy, ownership and criteria as input/design; do not derive them from standards or product surfaces.
- Product procedure status: NOT_REQUIRED_FOR_THIS_TASK; Product procedure is downstream of accepted project design and is not required for this task.
- Project input: PROJECT_INPUT_REQUIRED; actual_comm_users, comm_channels_and_bus_mapping, nm_cannm_adoption_per_channel, pnc_adoption_and_mapping, wakeup_sources, target_or_virtual_execution_scope
- Project design: PROJECT_DESIGN_REQUIRED; active_or_passive_nm_policy, nm_coordination_policy, wakeup_validation_owner_and_reaction_policy, startup_shutdown_sleep_policy, can_bus_off_recovery_policy, bswm_rule_and_action_list_realization, com_ipdu_group_activation_policy, application_availability_criteria
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Management ECU requirements and design authority
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: Dual CAN does not imply gatewaying; PNC adoption does not imply gateway responsibility; project policy is not a default.

## CNM-018 — Configured intent, generated artifact, build, runtime transition, verdict and coverage closure

- Lifecycle / owner: RUNTIME_EVIDENCE_AND_VERIFICATION / Build / target-runtime / measurement / requirements and verification ownership
- Reviewed semantic requirement: Define separate evidence planes from configured intent through validation/generation, artifact, compile/link, runtime, comparison, verdict and coverage.
- Product procedure status: OUTSIDE_AUTHORIZED_PRODUCT_SCOPE; No runtime or target-specific product procedure is authorized in this compilation.
- Project input: PROJECT_INPUT_REQUIRED; target_or_virtual_execution_scope, mode_transition_timing_requirements, network_and_application_availability_acceptance_criteria
- Project design: NOT_CURRENTLY_REQUIRED; none listed
- Safe activity: Compile only the bounded boundary and do not select values.
- Output/state: Project-neutral boundary with unresolved input/design and separate evidence handoff.
- Exit condition: Missing authority, project value or execution result remains explicit rather than inferred.
- Next handoff: Accepted requirements, execution plan and verification owner
- Future evidence: Accepted project input/design, then separately traceable validation/generation, build, runtime and requirement evidence as applicable.
- Retained negative: Configuration != validation != generation != compile/link != runtime; generated artifact != deployed binary; runtime observation != requirement != verdict != coverage.

## CNM-016 supporting workflow

The reviewed authority permits these generic commands as supporting workflow only;
no actual project path is selected and no CNM-specific completion is implied:

    dvcfg-b project validate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
    dvcfg-b project generate -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"
    dvcfg-b project generate-schema -p="/Path/To/DaVinci/Project" -b="/Path/To/BSW/Package"

These commands do not establish CNM mapping, diagnostics, artifact identity,
compile/link, runtime transition, requirement comparison, verdict or coverage.

## Final stop boundary

Do not select ComM users/channels, Nm/CanNm policy/timers, PNC IDs, wakeup
sources, controller/transceiver identities, bus-off values, BswM rules, COM
I-PDU Group membership, application availability, target/runtime or acceptance
criteria. These remain project input/design or later evidence.
