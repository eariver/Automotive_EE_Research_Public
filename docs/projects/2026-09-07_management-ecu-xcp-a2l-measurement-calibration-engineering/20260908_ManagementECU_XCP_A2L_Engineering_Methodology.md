# Management ECU XCP/A2L Engineering Methodology

Date: 2026-09-08
Status: Sol-reviewed projection; no new propositions

## Evidence planes

Five planes are kept separate for every task:

1. standards/semantic authority — what the reviewed AUTOSAR and description standards establish at bounded depth
2. product procedure authority — what reviewed vendor tools establish at product-local scope
3. project input/design — what the Management ECU project must still decide
4. execution evidence — what must still be observed on the project target and toolchain
5. requirement verdict/coverage — what must still be compared, judged and measured for completeness

A stronger status in one plane never upgrades another plane. In particular, product procedure is never runtime proof, and configuration is never a verdict.

## Engineering lifecycle

The lifecycle is read as:

```text
description -> address resolution -> consumption -> server -> transport -> session -> measurement/calibration/security -> evidence
```

Each arrow is a claim that must be evidenced independently:

- description exists does not prove address resolution
- address-resolved artifact exists does not prove consumer acceptance
- consumer import accepted does not prove a server exists
- server implemented does not prove transport/endpoints match
- endpoints matched does not prove a live session
- live session established does not prove acquisition, write, page operation or authorization success
- any observation does not prove a requirement verdict
- any verdict does not prove coverage

## Mandatory non-collapse boundaries

```text
A2L producer != A2L consumer

A2L consumer != XCP server

XCP master/client != XCP slave/server

A2L generation != server creation

generated A2L != address-resolved / target-aware A2L

address update / reload != server creation

address update / reload != live-binding proof

A2L format/version != XCP protocol version

transport support != endpoint implementation

transport selection != endpoint reachability

A2L import/device creation != running endpoint

CANape tutorial online/ready != Management ECU runtime evidence

XcpEventChannel != XcpCommunicationChannel

DAQ list != ODT != ODT entry != DTO

DAQ/event timing != application runnable scheduling

configured event/raster != measured acquisition timing

DAQ != STIM != calibration memory write

calibration edit != successful target write/read-back

parameter-file save/load != ECU persistence/flash result

DAQ RESUME != calibration page/value persistence

linker MAP/A2L update != deployed-image identity proof

address mapping != successful live binding

configured memory synchronization != successful synchronization/read-back

configured Seed&Key/resource protection != successful authorization

configuration != runtime evidence

runtime evidence != requirement verdict

requirement verdict != coverage
```

## Depth rules

- AUTOSAR depth closes only the reviewed safe frontier for `XCP-012` through `XCP-015`. Dynamic protocol detail is a conditional ASAM dependency only if a later requirement makes it load-bearing.
- CANape depth closes only introductory project/device, measurement-mode selection and calibration-editing/parameter-file surfaces for `XCP-016`. MAP, mapping/synchronization and security detail remain `SOURCE_UNAVAILABLE`.
- The Simulink Real-Time route is a bounded R2025b exception and is never a generic method step.
- `SOURCE_UNAVAILABLE` is always read as documentation/access scope, never as capability absence.
