# Management ECU Crypto Execution Reference Guide

Date: `2026-09-06`

This guide distinguishes the current safe frontier from later project, vendor, and execution evidence. It does not execute any of the later activities.

## 1. Available now from reviewed authority

- AUTOSAR CP 4.4.0 CSM, CryIf, Crypto Driver, KeyM semantic relationships and state distinctions.
- AUTOSAR-side ECUC definition/reference checklist.
- Bounded generic application/SW-C and conditional SecOC consumer relations.
- Bounded `DCM Authentication 0x29 -> CSM/KeyM` relation.
- Sol-reviewed Vector/MICROSAR product-procedure classification.
- Generic Configurator supporting workflow:

  ```text
  dvcfg-b project validate
  dvcfg-b project generate
  dvcfg-b project generate-schema
  ```

- Generic CLI status/exit-code and CI workflow context, without Crypto-specific promotion.

## 2. Requires project input or design

The project authority must decide, without defaulting values:

- actual Crypto consumers and owners;
- required security properties and acceptance criteria;
- Authentication `0x29`, SecOC, and KeyM certificate adoption;
- algorithm/mode/key roles and key hierarchy;
- queue, priority, processing, callback, and cancellation policy;
- provisioning source/backend/protocol;
- population/update lifecycle and persistence expectations;
- target or virtual execution scope, runtime stimulus, and evidence ownership.

The current project baseline does not supply these decisions.

## 3. Requires vendor or hardware authority

Concrete Crypto Driver/HSM/SHE/accelerator realization requires a separately authorized vendor/hardware source when project design makes it load-bearing. This includes topology, capabilities, key slots, driver implementation, firmware/image, hardware-backed persistence, and performance claims.

This dependency is explicit for vendor-realization scope and conditional for project-input and execution scope. No vendor research is started automatically.

## 4. Requires actual execution evidence

The following must be collected as separate evidence layers in a future authorized unit:

```text
configured intent
-> generated artifact
-> compile/link result
-> deployed/virtual/physical execution
-> Crypto Driver job execution/result
-> provisioning/population result
-> timing/performance/resource measurement
-> consumer acceptance
-> test verdict
-> coverage
```

Each arrow requires its own artifact or observation. A generic generation command cannot close the chain.

## 5. Must not be inferred

- AUTOSAR parameter names do not establish Vector GUI/object paths or product operations.
- Generic Configurator validation/generation does not establish Crypto-specific diagnostics, generated filenames, build ownership, HSM behavior, or runtime result.
- `CRY-016` vendor authority does not mean the Management ECU selected HSM/SHE or an accelerator.
- Project design/input tasks do not contain algorithms, identifiers, keys, slots, entropy values, or acceptance thresholds.
- CSM/CryIf/Crypto Driver completion does not prove durable persistence, authorization, test verdict, or coverage.
- `DCM Authentication 0x29` is not SecurityAccess `0x27` and is not universal diagnostic authorization.
- Conditional SecOC is not current project adoption.

## 6. Safe-frontier handoff

When a required item is absent, record:

1. the layer that is available;
2. the exact unresolved input or evidence;
3. the owner of the next decision;
4. the promotion evidence required;
5. the negative statement that must not be overread as capability absence.

The next justified activity after this package is Sol review. HSM/vendor research, runtime execution, and publication remain outside this unit.
