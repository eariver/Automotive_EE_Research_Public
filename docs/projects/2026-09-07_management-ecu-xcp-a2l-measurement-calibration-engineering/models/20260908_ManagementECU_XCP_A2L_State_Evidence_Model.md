# Management ECU XCP/A2L State Evidence Model

Date: 2026-09-08
Status: Sol-reviewed projection; upstream states never auto-prove downstream states

## States

- description artifact exists
- address-resolved artifact exists
- consumer import accepted
- target server implemented
- transport/endpoints matched
- live session established
- DAQ acquisition observed
- STIM/write operation observed
- memory/page operation observed
- authorization observed
- requirement compared
- verdict assigned
- coverage assessed

## Separation rules

- A description artifact existing does not prove it is address-resolved or target-aware.
- An address-resolved artifact existing does not prove consumer acceptance.
- Consumer import accepted does not prove a target server is implemented.
- A target server implemented does not prove transport and endpoints match.
- Matched transport/endpoints do not prove a live session was established.
- A live session established does not prove DAQ acquisition, STIM/write success, page-operation success or authorization success.
- Calibration editing never proves a successful target write or read-back.
- Parameter-file save/load never proves ECU persistence or a flash result.
- Configured memory synchronization never proves successful synchronization or read-back.
- Configured Seed&Key/resource protection never proves successful authorization.
- Any observation never proves a requirement verdict by itself.
- Any verdict never proves coverage by itself.

## Reading the matrix with this model

The public coverage matrix reports authority/configuration status separately from execution evidence status. `XCP-006`, `XCP-007`, `XCP-009` and `XCP-011` remain `UNRESOLVED_RETAINED` because the generic lifecycle transitions they cover have no reviewed closure. `XCP-012` through `XCP-015` carry reviewed semantic configuration identities with execution still unobserved. `XCP-016` carries reviewed product-procedure surfaces with project adoption still undecided. All runtime verdicts are `NOT_EVALUATED`.
