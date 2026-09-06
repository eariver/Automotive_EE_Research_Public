# Management ECU CAN Signal / I-PDU Communication
# Reference Index

Date: 2026-09-06
Status: LUNA_CURRENT_PACKAGE_COMPILATION_PROPOSAL

## 1. Authority fence

Only exact-pinned Sol-reviewed Knowledge is technical authority for this package.

### A-PRIMARY — AUTOSAR architecture and workflow

- Repository: eariver/Research_AUTOSAR_CP_Documents
- Exact commit: 8c67ddc4cc6ce4bba1881a879b933cf2b751d733
- Release: AUTOSAR Classic Platform 4.4.0
- Policy: only Sol-reviewed Knowledge at this exact commit

### A-COM — focused AUTOSAR COM semantics

- Repository: eariver/Research_AUTOSAR_CP_Documents
- Exact commit: fc05fc7824d56b1a34eaf42e3d50150ff70a789d
- Reviewed Knowledge:
  docs/knowledge/management-ecu-can-signal-ipdu-autosar-semantic-depth.md
- Release fence: AUTOSAR Classic Platform 4.4.0 / R18-10 family
- Scope: COM Signal/group, packing, Tx, Rx, update/invalid/timeout and I-PDU
  Group semantic depth plus an AUTOSAR-side product checklist

### V-COM — Vector/MICROSAR product procedure

- Repository: eariver/Research_Vector_Documents
- Exact commit: 138dba4d76bc9cf7fadec1ee818aa7e6b9db4b70
- Reviewed Knowledge:
  docs/knowledge/management-ecu-com-vector-procedure.md
- Product: DaVinci Configurator Classic 6.3.10 / MICROSAR
- Scope: reviewed product surface, procedure maturity and generic validate,
  generate, schema and CLI status context

### P-INPUT — project control input

- Repository: eariver/Automotive_EE_Engineering_Knowledge
- Path:
  docs/projects/2026-09-06_management-ecu-can-signal-ipdu-communication-engineering/references/project/can-signal-ipdu-communication-project-input-baseline.yaml
- Status: UNRESOLVED_PROJECT_INPUT
- Role: project-owned input register, not technical authority

## 2. Exact A-PRIMARY entries

The following reviewed entries are pinned at A-PRIMARY. The listed blob SHA is
the entry identity recorded by the downstream authority-pins file.

| Ref ID | Reviewed Knowledge path | Entry blob SHA | Locators / package use |
|---|---|---|---|
| A-001 | docs/knowledge/concepts/sender-receiver-model-runtime-boundary.json | 37c05da9630b4682c4cfb7a2f2fee90c83a99bbe | TPS_SoftwareComponentTemplate p.520; SRS_RTE p.45; SWS_RTE p.500; SRS_Rte_00028; SWS_Rte_03574 |
| A-002 | docs/knowledge/concepts/swc-port-interface-connector-model-boundary.json | a418bb4bf06170159567439b1e244eba07da0a72 | TPS_SoftwareComponentTemplate p.80; SRS_RTE p.20 |
| A-003 | docs/knowledge/workflows/sender-receiver-model-to-runtime-access.json | 64fd5d9a515b1a6156e07ed39026a42360f37417 | TPS_SoftwareComponentTemplate p.520; SWS_RTE p.500; SRS_Rte_00098; SWS_Rte_03574 |
| A-004 | docs/knowledge/workflows/system-to-ecu-configuration.json | d18f65665801eac666f5457d480ce59d1f934815 | TR_Methodology p.79; TPS_ECUConfiguration p.16; TPS_SystemTemplate p.571 |
| A-005 | docs/knowledge/artifacts/ecu-extract.json | adb75abaa32566d1ca2d12a9244f6399522d568d | TR_Methodology p.84; TPS_SystemTemplate p.571; TPS_SWCT p.665; TPS_SYST_01139 |
| A-006 | docs/knowledge/artifacts/ecu-configuration-values.json | 3b41073d64f100ff44372f65dfd6b229150453bc | TPS_ECUConfiguration p.24; TR_Methodology p.481; SWS_RTE p.88 |
| A-007 | docs/knowledge/concepts/can-communication-modeling-boundary.json | b5251a8b005076f90684d213d070db074bbdbd79 | TPS_SystemTemplate 3.3.1 CAN p.56; section 6 Communication p.181 |
| A-008 | docs/knowledge/workflows/can-signal-ipdu-data-path.json | fecf3d21c0f5068bf604e0d18a45301a2cd221c0 | SWS_COM p.9; SWS_PduR p.13; SWS_CANInterface p.11; SWS_CANDriver p.42; TPS_SystemTemplate p.181; SWS_Com_00495; SWS_Can_00016 |
| A-009 | docs/knowledge/concepts/pdur-if-tp-gateway-boundary.json | e246bf29ef9004f0a588375fccb9b6a281073cc3 | SWS_PduR p.18 and p.40; SRS_PduR_06012; SWS_PduR_00436; SWS_PduR_00708; ECUC_PduR_00320 |
| A-010 | docs/knowledge/concepts/can-hardware-abstraction-ownership.json | c6ee6de178662a076c97e64c29aad8d525288d18 | SWS_CANInterface p.11; SWS_CANDriver p.13; SWS_CANTransceiverDriver p.22; SWS_Can_00059; SWS_Can_00016 |
| A-011 | docs/knowledge/goal-maps/configure-and-trace-can-communication.json | 0946e79ece6b8c5417b398ea55b42626044ceb32 | TPS_SystemTemplate p.56 and p.181; SWS_COM p.9; SWS_PduR p.13; SWS_CANInterface p.11; SWS_COMManager p.10; SWS_CANStateManager p.15 |
| A-012 | docs/knowledge/goal-maps/configure-ecu-from-system-description.json | 5349a926173f695057595752c84bca6e0fb96039 | TR_Methodology pp.79-86; TPS_ECUConfiguration p.16; SWS_RTE p.88 |
| A-013 | docs/knowledge/workflows/can-transport-protocol-path.json | efeb8e8b68da673786b0eb2e83aa7ba8f177ef56 | SWS_CanTp pp.17, 23-24; SWS_Com p.63; SWS_CanTp_00033; SWS_CanTp_00238; boundary-only conditional CanTp |
| A-014 | docs/knowledge/concepts/ipdum-conditional-processing-boundary.json | c011de43607e207560070582eff5e7394b9c1bc1 | SWS_IpduM pp.9, 28; SWS_IpduM_00041; SWS_IpduM_00188; conditional IpduM |
| A-015 | docs/knowledge/workflows/ipdum-multiplex-container-path.json | fc8cd7bd1a78f741f1fefc97538bc7437534cf06 | SWS_IpduM pp.9, 28; SWS_PduR p.11; conditional multiplex/container route |
| A-016 | docs/knowledge/concepts/secoc-communication-protection-ownership.json | 6e95583bbd87797b7cbd0d257a0da11d71494693 | SWS_SecOC pp.15, 43-48; SWS_SecOC_00104; boundary-only conditional SecOC |
| A-017 | docs/knowledge/workflows/secoc-protected-ipdu-path.json | 3cac86f599fcd5087a82f3c643cff24bb6c2a3f7 | SWS_SecOC pp.15, 40, 43-48, 76; conditional security route |
| A-018 | docs/knowledge/concepts/com-based-transformer-serialization-boundary.json | 4aeb8ba88666562710c02fc2513c750e4d77c0be | SWS_COMBasedTransformer pp.14, 20; SWS_ComXf_00003; boundary-only transformer |
| A-019 | docs/knowledge/workflows/com-signal-gateway-routing.json | 8a4363c0eef320133c05ce51628841ee5390813b | SWS_COM section 7.11 p.72; SWS_PduR p.18; TPS_SystemTemplate p.446; signal gateway boundary |
| A-020 | docs/knowledge/concepts/can-communication-mode-ownership.json | 9842906b945d2c56dcac89e45c5660bce45a910a | SWS_ComM p.10; SWS_CanSM p.15; ComM/CanSM state-plane boundary |

## 3. Focused A-COM semantic sections

| Ref ID | Reviewed Knowledge section | Task use |
|---|---|---|
| C-001 | section 2 Canonical non-collapse model | all COM identity and evidence boundaries |
| C-002 | section 3 COM Signal, GroupSignal, SignalGroup and I-PDU identities | COM object ownership and explicit references |
| C-003 | section 3.1 Foreign System Template references | external mapping remains a foreign-reference contract |
| C-004 | section 4 Signal-group consistency and access alternatives | shadow-buffer versus UINT8-array conditional branch |
| C-005 | section 5 COM I-PDU layout and representation | bit position, bit size, type, length, endianness and dynamic branch |
| C-006 | section 6 Tx transfer property, mode selection and repetition | transfer property, TMS, mode, repetition and cyclic dimensions |
| C-007 | section 7 COM scheduled-function timing handoff | COM time base/main-function boundary |
| C-008 | section 8 Rx indication, unpacking and delivery boundary | immediate/deferred processing and application boundary |
| C-009 | section 9 Update-bit, filter, invalid and timeout states | independent Rx data-quality conditions |
| C-010 | section 10 COM notification versus application consumption | callback and consumption separation |
| C-011 | section 11 Deadline monitoring | first/subsequent timeout, monitoring and timeout-action boundary |
| C-012 | section 12 COM I-PDU Group control boundary | COM group control versus ComM/CanSM state |
| C-013 | section 13 AUTOSAR-side input contract for later product research | product mapping checklist without GUI inference |
| C-014 | sections 14 and 16 task disposition and retained negatives | semantic closure and remaining project/product/runtime gaps |

## 4. V-COM product sections

| Ref ID | Reviewed Knowledge section | Task use |
|---|---|---|
| V-001 | section 1 Reviewed product role | product scope and documentation negatives |
| V-002 | section 2.1 Aggregated PDU Editor versus COM-specific ownership | COM-004/005 partial maturity |
| V-003 | section 2.2 BswM I-PDU Group mention versus COM product ownership | COM-010 partial maturity |
| V-004 | section 2.3 Exact generic commands versus aggregate COM-016 maturity | COM-016 partial maturity and exact subprocedures |
| V-005 | section 3 Product PDU and configuration surfaces | PDU/PDU-group and generic module/container surfaces |
| V-006 | section 4 Tx/Rx/deadline/control realization boundary | surface-only/no-explicit product coverage |
| V-007 | section 5 Validation, generation and artifact boundary | exact generic commands, output and CI/build limits |
| V-008 | section 6 Reviewed aggregate coverage | fixed task-level product classifications and counts |
| V-009 | section 7 Retained documentation-scope negatives | bounded negative handling |
| V-010 | section 8 Mandatory non-collapse boundaries | product/model/runtime separation |
| V-011 | section 9 Project-input and execution-evidence boundary | blocker separation |
| V-012 | section 10 Generic research closure | no broad HELP re-investigation |

## 5. Project input families

The project baseline identifies unresolved families for:

- application communication contract;
- System Description and ECU mapping;
- COM signal configuration;
- COM I-PDU Tx/Rx configuration;
- I-PDU Group control;
- PduR routing;
- CanIf configuration;
- CanDrv/controller;
- CAN/CAN FD frame and bus;
- toolchain;
- verification and acceptance.

These are project inputs/design decisions. They are not authority for invented
values.

## 6. Exclusions

Not used as new technical evidence:

- Web or current vendor documentation;
- raw AUTOSAR PDFs or raw Vector HELP;
- floating upstream heads;
- generic AUTOSAR/Vector model knowledge;
- unreviewed observations, sibling worklogs, prompts or checkpoints;
- inferred Vector GUI/CLI from AUTOSAR parameter names.

No docs/knowledge/** source is modified by this compilation.
