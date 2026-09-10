# Management ECU Startup / Shutdown / ECU Mode Management Engineering Methodology

Date: 2026-09-11
Status: Sol-reviewed projection; no new propositions

## Evidence planes

Five planes are kept separate for every task:

1. semantic authority — what the reviewed AUTOSAR depth establishes (request protocols, arbitration/action concepts, handoff facts, phase distinctions)
2. product procedure authority — what the reviewed Vector/MICROSAR body establishes at product-local scope (list/item configuration, Communication Control, state-handling surfaces)
3. project input/design — what the Management ECU project must still decide (every concrete allocation, mapping, policy and threshold)
4. execution evidence — what must still be observed on the project target and toolchain (traces, completions, observations)
5. requirement verdict/coverage — what must still be compared, judged and measured for completeness

A stronger status in one plane never upgrades another plane. In particular, product procedure is never runtime proof, semantic authority never selects a project value, and configuration is never a verdict.

## Engineering lifecycle

The lifecycle is read as:

```text
reset/boot -> StartPreOS -> StartOS -> StartPostOS -> RUN/POST_RUN -> BswM arbitration -> Action List execution -> ComM/Nm/NvM coordination -> shutdown initiation -> late shutdown -> wakeup -> sleep/coordination -> evidence
```

Each arrow is a claim that must be evidenced independently:

- reset/boot described does not prove pre-OS entry or driver allocation
- configured initialization order does not prove observed runtime startup order
- StartOS transfer observed does not prove runnable execution or application readiness
- BswM initialized does not prove BSW, RTE or application startup is complete
- RUN/POST_RUN requested does not prove RUN state or functional readiness
- mode requested does not prove rule evaluation, Action List selection, action invocation or downstream outcome
- BswM action invoked does not prove downstream service/job completion
- BswM EcuM action invoked does not prove EcuM controlled lifecycle implementation
- BswM NvM action invoked does not prove NvM asynchronous completion or durable persistence
- shutdown requested does not prove target selection, late-shutdown execution or physical power loss
- wakeup detected does not prove wakeup validation or reaction
- validation success does not prove generation success, compile/link, deployment or runtime behavior
- any observation does not prove a requirement verdict
- any verdict does not prove coverage

## Mandatory non-collapse boundaries

```text
EcuM lifecycle orchestration != BswM Mode Arbitration / Mode Control

RUN request != RUN state != application functional readiness

mode request != rule evaluation != Action List selection != action invocation != downstream outcome

immediate BswM arbitration != deferred BswM arbitration

BswM action invocation != downstream service/job completion

BswM EcuM action != EcuM-controlled lifecycle implementation

BswM NvM action != NvM asynchronous completion != durable persistence

EcuM_Init / StartPreOS != StartOS != EcuM_StartupTwo / StartPostOS

StartOS handoff != runnable execution proof

BswM_Init != completed BSW/RTE/application startup

ComM/Nm mode != EcuM lifecycle state != BswM rule/mode state

NvM_ReadAll request != asynchronous completion != valid application-data proof

NvM_WriteAll request != NvM completion != lower-memory completion != durable persistence proof

shutdown request != shutdown-target selection != late-shutdown execution != physical power loss

ShutdownOS != ShutdownAllCores

OFF != RESET != sleep target

physical wakeup/WUF != CanSM WUVALIDATION != EcuM wakeup validation

wakeup detection != wakeup validation != wakeup reaction

Car Wakeup indication != BusSM startup != EcuM wakeup-source policy

configured initialization order != observed runtime startup order

validation success != generation success != compile/link != deployment != runtime evidence

configuration != generated artifact != runtime evidence != requirement verdict != coverage
```

Single-core flows are never generalized to multi-core: `ShutdownOS` evidence never satisfies `ShutdownAllCores` evidence.

## Depth rules

- AUTOSAR depth closes only the reviewed safe frontier for `ECUM-006` through `ECUM-008` (request-protocol input boundary, arbitration/action concepts with explicit negatives). Project rules, expressions, priorities, evaluation order, Action List contents/order and runtime outcomes remain open.
- Vector depth closes only pre-OS/post-OS list/item configuration surfaces and partial Communication Control for `ECUM-003`, `ECUM-005` and `ECUM-009`, plus role/surface references for `ECUM-001`, `ECUM-006`, `ECUM-011` and `ECUM-016`. Management ECU allocations, invocation proofs and complete handoffs remain open.
- `NO_EXPLICIT_REVIEWED_PRODUCT_PROCEDURE` is always read as documentation/reviewed-procedure scope, never as capability absence.
- `SURFACE_OR_ROLE_ONLY` never selects a trigger, target, requestor or policy.
