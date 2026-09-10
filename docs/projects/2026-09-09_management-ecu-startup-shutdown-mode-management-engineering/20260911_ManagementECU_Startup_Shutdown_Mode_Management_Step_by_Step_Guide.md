# Management ECU Startup / Shutdown / ECU Mode Management Step-by-Step Guide

Date: 2026-09-11
Status: future project execution framework — not a project implementation result

Nothing below is reported as completed. Each step distinguishes reviewed authority, the project decision still required, and the future evidence still required.

## 1. Decide scope, roles and ownership

- Reviewed authority: EcuM lifecycle orchestration vs BswM rule arbitration vs EcuM controlled late shutdown (ownership direction only).
- Project decision required: EcuM/BswM/OS/SchM/RTE/ComM-Nm/NvM owners, lifecycle-plane definitions, integration responsibility.
- Future evidence required: accepted symbolic scope/ownership record. No allocation values.

## 2. Decide reset/boot entry and pre-OS policy

- Reviewed authority: none at bounded depth (`AUTHORITY_GAP` retained; no explicit Vector procedure).
- Project decision required: reset sources, boot policy, MCU/power-controller integration, pre-OS entry criteria.
- Future evidence required: accepted reset/boot design record. No source inferred from generic startup workflows.

## 3. Fix StartPreOS driver-initialization phases

- Reviewed authority: StartPreOS phase existence; DaVinci pre-OS list/item configuration procedure (partial).
- Project decision required: driver-init phase allocation, driver-init order, completion criteria.
- Future evidence required: accepted phase allocation/order design; configured record kept distinct from observed startup order.
- Note: list/item configuration never selects the Management ECU allocation.

## 4. Confirm the StartOS control transfer

- Reviewed authority: EcuM_Init/StartPreOS hands control to StartOS; the first normal StartOS call does not return into EcuM startup continuation.
- Project decision required: OS application mode, handoff configuration, post-handoff scheduling policy.
- Future evidence required: configured handoff record plus StartOS transfer observation distinct from any runnable trace.
- Note: handoff proves no runnable execution and no readiness.

## 5. Design StartupTwo / StartPostOS / SchM / BswM / RTE completion

- Reviewed authority: OS-started task invokes EcuM_StartupTwo; StartPostOS SchM/BswM handoffs; `BswM_Init` negative; post-OS list/item configuration procedure (partial).
- Project decision required: StartupTwo invocation design, SchM/BswM/RTE startup sequence, startup-completion definition.
- Future evidence required: invocation trace, startup observations, completion-criteria comparison.
- Note: RTE start never defines application availability.

## 6. Design RUN / POST_RUN requestors, arbitration and state

- Reviewed authority: EcuM RUN/POST_RUN request protocol and `BswM_EcuM_RequestedState` input boundary; BswM Ecu State Handling surface only.
- Project decision required: RUN/POST_RUN requestors, arbitration policy, RUN-state definition, functional-readiness criteria.
- Future evidence required: request trace, arbitration/state observation, readiness observation where required.
- Note: request, state and readiness are evidenced as separate layers.

## 7. Design BswM mode requests and rule evaluation

- Reviewed authority: arbitration vs control distinction; logical-rule evaluation concept; immediate vs deferred arbitration distinction. No explicit Vector rule/expression/priority/order procedure.
- Project decision required: BswM rules, rule expressions, rule priorities, evaluation policy.
- Future evidence required: mode-request trace, rule-evaluation observation.
- Note: no AUTOSAR example is copied as a project rule.

## 8. Design BswM Action Lists and action execution

- Reviewed authority: ordered Action List execution concept; BSW/RTE invocation, list reference, further rule evaluation at concept depth. No explicit Vector Action List/action procedure.
- Project decision required: Action Lists, action-selection policy, action-execution policy and order.
- Future evidence required: action-selection record, action-execution trace, outcome observation.
- Note: no AUTOSAR example is copied as a project action; BswM EcuM/NvM actions prove no downstream implementation, completion or persistence.

## 9. Map ComM/Nm interaction with the ECU lifecycle

- Reviewed authority: ComM/Nm coordination plane; BswM Communication Control (partial).
- Project decision required: ComM users/channels/modes, Nm adoption per channel, ComM/Nm-to-lifecycle mapping.
- Future evidence required: ComM/Nm mode observation, lifecycle-state observation, interaction comparison.
- Note: ComM mode, EcuM lifecycle state and BswM rule/mode state are evidenced separately.

## 10. Design NvM ReadAll startup participation

- Reviewed authority: BswM ReadAll trigger ownership; NvM async execution/result ownership. No explicit Vector ReadAll action procedure.
- Project decision required: participating blocks, startup timing policy, completion handoff, application-data validity criteria.
- Future evidence required: request record, async-completion observation, data-validity observation.
- Note: no block is inferred from generic NvM maturity.

## 11. Design shutdown initiation and target selection

- Reviewed authority: BswM trigger/selection vs EcuM late-shutdown ownership; Ecu State Handling surface only.
- Project decision required: shutdown requestors, GoDown adoption, shutdown target, trigger policy.
- Future evidence required: shutdown-request record, target-selection record, initiation observation.
- Note: request, selection, execution and power loss are evidenced as separate layers.

## 12. Design NvM WriteAll shutdown participation

- Reviewed authority: BswM WriteAll trigger ownership; NvM async execution/result ownership. No explicit Vector WriteAll action procedure.
- Project decision required: participating blocks, shutdown time budget, completion handoff, durability criteria.
- Future evidence required: request record, NvM completion observation, lower-memory completion observation, durability observation.

## 13. Design late shutdown and power targets

- Reviewed authority: ShutdownOS vs ShutdownAllCores distinction; EcuM late-shutdown ownership; OFF/RESET/sleep target identities. No explicit Vector shutdown-target procedure.
- Project decision required: OFF/RESET/sleep target, halt/poll/sleep strategy, power-control strategy, single-core vs multi-core topology.
- Future evidence required: late-shutdown execution trace, target-state observation, single-core vs multi-core execution record.
- Note: single-core evidence never covers multi-core.

## 14. Decide wakeup sources and detection policy

- Reviewed authority: physical/WUF vs CanSM WUVALIDATION vs EcuM validation separation; detection as a phase distinct from validation/reaction. No explicit Vector detection/registration procedure.
- Project decision required: wakeup sources, detection owner, event-registration policy.
- Future evidence required: wakeup-detection observation, event-registration record.

## 15. Design wakeup validation, expiration and reaction

- Reviewed authority: validation-phase separation. No explicit Vector validation/expiration/reaction procedure.
- Project decision required: validation owner, validation timeout, debounce/filter policy, expiration policy, reaction policy.
- Future evidence required: validation-phase observation, expiration observation where applicable, reaction observation.

## 16. Design sleep/wakeup and communication-mode coordination

- Reviewed authority: Car Wakeup vs BusSM startup vs EcuM policy separation; communication/state-handling surfaces only.
- Project decision required: sleep/power-state strategy, BusSM startup mapping, EcuM wakeup-source policy, communication-coordination policy.
- Future evidence required: sleep/wakeup transition trace, communication-mode observation, coordination comparison.
- Note: Car Wakeup indication selects no power policy.

## 17. Consolidate the project design package

- Reviewed authority: none; this is the project plane.
- Project decision required: reset/boot policy, driver-init design, BswM rule/action design, RUN/POST_RUN design, ComM/Nm mapping, NvM block policy, shutdown-target design, wakeup design, sleep/power design, multicore design, acceptance thresholds. No numeric threshold is pre-selected here.
- Future evidence required: accepted traceable project baseline with symbolic identities and explicit ownership.

## 18. Collect runtime evidence and form verdict and coverage

- Reviewed authority: none; test-integration navigation at most, never a runtime result.
- Project decision required: target/runtime environment, stimulus and expected observations, acceptance/traceability/verdict/coverage rules.
- Future evidence required: generated/configured artifact, build result, runtime startup/shutdown/wakeup observations, requirement comparison, verdict assignment and coverage assessment as separate records.
