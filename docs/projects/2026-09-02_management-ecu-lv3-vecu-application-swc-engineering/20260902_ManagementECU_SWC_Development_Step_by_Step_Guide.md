# Management ECU — SWC Development Step-by-Step Guide
## Vector DaVinci Developer + MathWorks AUTOSAR Blockset / Embedded Coder

**Source methodology:** `20260902_ManagementECU_SWC_Development_Methodology.md`  
**Reference index:** `20260902_ManagementECU_SWC_Reference_Index.yaml`  
**Scope:** Application Software Component Development only  
**Target SWCs:** `ModeMgr`, `FuelMgr`, `AirMgr`, `ThermalMgr`, `ElectricalMgr`, `DiagMgr`

---

# 0. このガイドの使い方

このガイドはMethodologyの `SWC-D0`〜`SWC-D7` を実作業の順序へ展開したものとする。

各Stepでは以下を確認する。

```text
Input
  ↓
Methodology section
  ↓
External Reviewed Knowledge locator
  ↓
Action
  ↓
Artifact
  ↓
Completion criteria
  ↓
Next Step
```

外部Reviewed Knowledgeの具体的なrepository / exact commit / path / sectionは、この文書へ直接埋め込まず、

`20260902_ManagementECU_SWC_Reference_Index.yaml`

および `references/` 配下のlocator manifestを参照する。

MethodologyまたはReference Indexで未解決の項目を、一般知識や現在のvendor Web documentationで勝手に補完しない。

---

# 1. 開発境界を固定する

## 参照

Methodology:

- `§1 Purpose`
- `§2 Overall VECU Development Decomposition`
- `§32 Boundary to the Next VECU Phase`
- `§33 Canonical Development Principle`

## 今回の範囲

```text
Requirements
    ↓
DaVinci Developer
    ↓
AUTOSAR SWC Contract
    ↓
AUTOSAR Blockset
    ↓
Simulink / Stateflow
    ↓
Embedded Coder
    ↓
Generated C / H + implementation ARXML
    ↓
AUTOSAR Contract Reconciliation
    ↓
SWC Delivery Package
```

## 後工程

```text
Production RTE / BSW / OS
DaVinci Configurator / MICROSAR integration
VECU packaging
vVIRTUALtarget
CANoe / vTESTstudio / CANape
XCP runtime
UDS tester execution
```

## 完了条件

作業者が「SWC Development complete != VECU complete」を明示的に理解していること。

---

# 2. Step 0 — Tool / Version Baselineを固定する

## 参照

Methodology `§29 Tool Version Pinning`。

外部authority locatorはReference Indexで `Tool / Version Compatibility Record` とVector/MathWorks entriesを確認する。

## Action

最低限以下をbaseline化する。

```text
DaVinci Developer version
DaVinci Configurator version
MATLAB release
Simulink release
AUTOSAR Blockset release
Embedded Coder release
AUTOSAR schema version
code-generation configuration checksum
```

Methodology記載のReviewed Knowledge baselineは以下。

```text
DaVinci Developer Classic: 4.18 SP3 family
DaVinci Configurator Classic: 6.3.10
MathWorks: R2025b
```

実project releaseが異なる場合は、その実release combinationを別baselineとして固定する。

## Artifact

Project-local Tool / Version Compatibility Record。

## Completion

各SWC成果物からtool/release条件を追跡できること。

---

# 3. Step 1 — SWC-D0 Requirement Decomposition

## 参照

Methodology:

- `§3 Fundamental Ownership Model`
- `§5 SWC-D0 — Requirement Decomposition`
- `§12 DiagMgr`
- `§21 Production RTE Boundary`
- `§32 Boundary to the Next VECU Phase`

## Input

Requirement IDを保持したproject requirement artifact。

## Action

各RequirementをApplication SWC責務と後工程責務へ分解する。

最低限以下を決める。

```text
Requirement ID
Owning SWC
Required inputs
Required outputs
Trigger
State dependency
Calibration dependency
Diagnostic dependency
Network dependency
```

例:

```text
Upper ECU Maintenance Request
UDS RoutineControl Maintenance Request
Upper ECU request has higher priority
```

を、

```text
Application:
  mode arbitration
  maintenance ownership
  state transition

Diagnostic stack:
  RoutineControl decoding
  NRC transmission
```

へ分離する。

## Artifact

`SWC Requirement Allocation Table`

推奨columns:

| Req ID | Requirement | Owning SWC | Inputs | Outputs | Trigger | State dependency | Calibration | Diagnostic dependency | Network dependency |
|---|---|---|---|---|---|---|---|---|---|

## Completion

未分類requirementが残っていないこと。Project固有要求不足をAUTOSAR/vendor仕様で埋めないこと。

---

# 4. Step 2 — SWC Composition / Responsibilityを固定する

## 参照

Methodology:

- `§6 SWC-D1 — AUTOSAR Application Architecture Definition`
- `§26 Recommended SWC-Specific Allocation`

## Initial composition

```text
ManagementECU_Application
├── ModeMgr
├── FuelMgr
├── AirMgr
├── ThermalMgr
├── ElectricalMgr
└── DiagMgr
```

## Action

Requirement AllocationをSWC別に並べ、各SWCについて以下を作る。

```text
owned requirements
required inputs
provided outputs
other-SWC dependencies
stack / network abstract-state dependencies
```

## Completion

責務重複または未所有requirementが説明できる状態になっていること。

---

# 5. Step 3 — Shared Data Type / Interface Governance

## 参照

Methodology:

- `§3 Fundamental Ownership Model`
- `§8 Data Type and Shared Interface Governance`
- `§24 Shared Definition Change`

## Action

共通型をDaVinci Developer側のshared definitionとして整理する。

例:

```text
OperatingMode_t
MaintenanceOwner_t
FaultState_t
NodeHealth_t
BusHealth_t
FsaLevel_t
```

推奨package構造:

```text
/ManagementECU
    /DataTypes
    /PortInterfaces
    /Components
    /Compositions
```

## Rule

SWC model側で同名のshared type/interfaceを独立再定義しない。

## Completion

shared objectごとのsource of truthとaffected SWCsが明確であること。

---

# 6. Step 4 — SWC-D1 AUTOSAR Application Architecture Definition

## Tool

DaVinci Developer Classic。

## 参照

Methodology:

- `§6 SWC-D1`
- `§6.1 Port / Interface Definition`
- `§7 Runnable Architecture`
- `§8 Data Type and Shared Interface Governance`
- `§25 Calibration Change`

Vectorのexact Reviewed Knowledge locatorはReference Index / `references/vector/` を参照する。

## Action

対象SWCについて順番に確定する。

1. SWC type
2. Ports
3. PortInterfaces
4. Data types
5. Runnable identities
6. Runnable triggers/events
7. RTE access contract
8. PIM / calibration interface identity where applicable

Interface categoryはrequirementに応じて、

```text
Sender/Receiver
Client/Server
Mode
Calibration
NV data
Trigger
```

を使い分ける。

周期値自体はproject requirementから決める。

## Artifact

AUTOSAR SWC Contract ARXML。

## Completion

SWC identity / ports / interfaces / datatypes / runnable / events / RTE accessがcontractとして固定されていること。

## Prohibition

同じarchitecture objectをSimulink側で独立authorしない。

---

# 7. Step 5 — SWC-D2 MathWorks Model Scaffold Generation

## Tool

AUTOSAR Blockset / Simulink / Stateflow。

## 参照

Methodology:

- `§9 SWC-D2 — MathWorks Model Scaffold Generation`
- `§17 SWC-D4 — AUTOSAR Mapping`
- `§27 Artifact Baseline`

MathWorksのexact locatorはReference Index / `references/mathworks/` を参照する。

## Input

DaVinci DeveloperからexportしたSoftware Component ARXML。

## Action

```text
ARXML
  ↓
AUTOSAR Blockset importer
  ↓
initial Simulink AUTOSAR representation
```

を構成する。

## Boundary

```text
ARXML artifact != Simulink representation
```

## Artifact

- Simulink AUTOSAR component model
- input ARXML revision record
- import/update record

## Completion

DaVinci contractに対応するmodel scaffoldが成立していること。

---

# 8. Step 6 — SWC-D3 Behavior Implementation

## 共通参照

Methodology:

- `§10 SWC-D3 — Behavior Implementation`
- `§11 Fuel / Air / Thermal / Electrical Manager`
- `§12 DiagMgr`
- `§26 Recommended SWC-Specific Allocation`

MathWorks model/Stateflow authority locatorはReference Indexを使用する。

## ModeMgr

主にStateflow + Simulink。

一つの巨大chartへ潰さず、少なくとも以下のstate domainを分離して考える。

```text
Operational Mode
Maintenance Ownership
Fault Arbitration
Communication Health
```

Maintenance ownership:

```text
NONE
UPPER_ECU
UDS
```

Priority:

```text
UPPER_ECU > UDS
```

Upper ECU起点Maintenance中のUDS要求は `ConditionsNotCorrect` 相当のapplication result。実NRC生成はDCM側。

## FuelMgr / AirMgr / ThermalMgr / ElectricalMgr

主にSimulink。Discrete stateが必要な部分のみStateflow。

```text
Mode / Request
    ↓
Control / Coordination Logic
    ↓
Driver Command
    ↓
Driver Status / Feedback
```

詳細algorithmはproject requirementが存在してから実装する。

## DiagMgr

Stateflow + Simulink。

Application側で扱う候補:

```text
message supervision
counter stuck detection
checksum judgement
node failure confirmation
bus failure latch
fault-source latch
FSA / Indicator arbitration
```

再実装しないもの:

```text
physical CAN error state
CAN controller BUS_OFF
CanSM communication state
DEM event memory
DCM diagnostic service
```

AUTOSAR direct-standard責務のlocatorはReference Index / `references/autosar/` を参照する。

---

# 9. Step 7 — Project-Specific Counter / Checksum / Fault Logic

## 参照

Methodology:

- `§13 Project-Specific Counter / Checksum`
- `§14 Communication Fault State Model`
- `§15 Bus-Off Mask Behavior`
- `§16 DTC Clear Interaction`

## Counter

```text
Current == Previous -> invalid
Current != Previous -> valid
```

したがって `0 -> 2` はvalid。

## Checksum

```text
Checksum = (0x10 - W) mod 0x10
```

## Boundary

```text
PROJECT_SPECIFIC_DESIGN != AUTOSAR E2E Profile
```

AUTOSAR E2E Transformerへ暗黙置換しない。

## Node state

```text
HEALTHY
  ↓
FAILURE_CONFIRMING
  ↓
FAILED_LATCHED
```

release:

```text
next startup OR corresponding DTC clear
```

## Bus state

```text
BUS_HEALTHY
  ↓ CAN BUS_OFF indication
BUS_OFF_CONFIRMING
  ↓ confirmation time
BUS_FAILED_LATCHED
```

重要:

```text
native CAN BUS_OFF != project BUS_FAILED_LATCHED
```

## Bus-Off supervision behavior

native BUS_OFF active中はnode supervision timerをFREEZEする。RESETしない。

## DTC Clear

source-specific latchをclear後、残存fault sourceからFSA / Indicatorを再演算する。単一global fault bitに潰さない。

---

# 10. Step 8 — SWC-D4 AUTOSAR Mapping

## Tool

AUTOSAR Blockset。

## 参照

Methodology `§17 SWC-D4 — AUTOSAR Mapping`。

## Mapping examples

```text
Simulink Inport     ↔ AUTOSAR R-Port
Simulink Outport    ↔ AUTOSAR P-Port
Function/Subsystem  ↔ Runnable
Model Parameter     ↔ Calibration Parameter
Data Store          ↔ PIM where appropriate
```

## Artifact

AUTOSAR Mapping Configuration / mapping review record。

## Completion

unresolved mappingがないこと。

---

# 11. Step 9 — SWC-D5 Model-Level Verification / MIL

## 参照

Methodology:

- `§18 SWC-D5 — Model-Level Verification`
- `§19 MIL / SIL Separation`

MathWorks MIL/SIL authority locatorはReference Indexを参照する。

## Minimum categories

```text
Nominal behavior
Boundary behavior
State transition
Invalid input
Timeout
Counter failure
Checksum failure
Node failure
Bus failure
DTC clear
Maintenance arbitration
Startup initialization
```

ModeMgrでは追加で:

```text
Upper request
UDS request
simultaneous request
fault during Maintenance
fault clear
startup reset
```

## Artifact

- MIL test cases
- MIL result
- Requirement ↔ MIL traceability

## Completion

MIL PASSかつmajor state/fault transition確認済み。

## Boundary

```text
MIL PASS != SIL PASS
```

---

# 12. Step 10 — SWC-D6 Production-Intent Code Generation

## Tool

Embedded Coder。

## 参照

Methodology:

- `§20 SWC-D6 — Production-Intent Code Generation`
- `§21 Production RTE Boundary`
- `§27 Artifact Baseline`

## Output

```text
C source
H headers
AUTOSAR implementation ARXML
build metadata
code generation report
```

## Boundaries

```text
code generation != compile != link
MathWorks RTE stub != production MICROSAR RTE
```

Production RTEは後工程のDaVinci Configurator / MICROSAR側。

---

# 13. Step 11 — SIL Verification

## 参照

Methodology `§19 MIL / SIL Separation` と `§31 Definition of Done`。

## Action

MILで確認したmajor behaviorをgenerated implementation側でも検証する。

特に:

```text
state transition
fault confirmation
counter/checksum
bus-failure logic
DTC clear
Maintenance arbitration
startup initialization
```

## Artifact

- SIL test cases
- SIL result
- MIL/SIL correspondence
- updated requirement traceability

## Boundary

```text
MIL PASS != SIL PASS != later VECU verification PASS
```

---

# 14. Step 12 — SWC-D7 AUTOSAR Contract Reconciliation

## 参照

Methodology:

- `§22 SWC-D7 — AUTOSAR Contract Reconciliation`
- `§23 Change Management Rules`
- `§24 Shared Definition Change`

## Action

```text
Original DaVinci contract
        │
        ├── compare
        │
Generated MathWorks ARXML
        ↓
Integration decision
```

比較対象:

```text
SWC identity
port identity
interface identity
datatype identity
runnable identity
event mapping
calibration identity
PIM identity
AUTOSAR schema version
package path
unexpected AUTOSAR objects
```

## Boundary

round-trip supportはbyte-for-byte identityやuniversal automatic mergeを意味しない。

## Completion

unintended architecture change、unresolved mappingがないこと。Generated ARXMLを無条件上書きしないこと。

---

# 15. Step 13 — SWC Delivery Package

## 参照

Methodology:

- `§30 SWC Delivery Package`
- `§31 Definition of Done — SWC Development`
- `§32 Boundary to the Next VECU Phase`

## Required package

```text
SWC Delivery
├── AUTOSAR contract ARXML
├── Simulink / Stateflow source model
├── AUTOSAR mapping configuration
├── generated C source
├── generated headers
├── implementation ARXML
├── code-generation report
├── MIL result
├── SIL result
├── requirement traceability
└── delivery manifest
```
Delivery Manifest:

```text
SWC version
Requirement baseline
DaVinci baseline
MathWorks baseline
AUTOSAR schema
input ARXML revision
model revision
generated-code revision/hash
generated-ARXML revision/hash
MIL status
SIL status
known limitations
```

## Completion

version-fixedでDaVinci Configurator / MICROSAR integrationへhandoff可能なこと。

---

# 16. Definition of Done

## Contract

- [ ] DaVinci Developer上でSWC contract確定
- [ ] Port / Interface / Datatype確定
- [ ] Runnable / Event確定
- [ ] RTE access contract確定

## Model

- [ ] ARXMLからmodel scaffold成立
- [ ] AUTOSAR mapping完成
- [ ] Application behavior実装済み

## Verification

- [ ] Requirement traceabilityあり
- [ ] MIL PASS
- [ ] SIL PASS
- [ ] major state/fault transition検証済み

## Generation

- [ ] Embedded Coder generation PASS
- [ ] C/H生成済み
- [ ] implementation ARXML生成済み
- [ ] code-generation report生成済み

## Reconciliation

- [ ] DaVinci contract / generated ARXML差分確認済み
- [ ] unintended architecture changeなし
- [ ] unresolved AUTOSAR mappingなし

## Delivery

- [ ] SWC Delivery Package version-fixed
- [ ] DaVinci Configurator handoff readiness確認済み

---

# 17. Change Request Routing

| Change | First owner | Methodology |
|---|---|---|
| Algorithm変更 | Simulink | `§23.1` |
| State transition変更 | Stateflow | `§23.1` |
| Fault confirmation logic変更 | Simulink / Stateflow | `§23.1` |
| Port追加/変更 | DaVinci Developer | `§23.2` |
| Datatype変更 | DaVinci Developer | `§23.2`, `§24` |
| Runnable追加/変更 | DaVinci Developer | `§23.2` |
| Shared type変更 | DaVinci Developer | `§24` |
| Calibration contract変更 | architecture/integration control | `§25` |
| Calibration value変更 | project calibration | `§25` |
| Production RTE/BSW/OS変更 | later Configurator/MICROSAR phase | `§21`, `§32` |

Interface changeは必ず:

```text
Change Request
  ↓
DaVinci Developer
  ↓
new ARXML
  ↓
AUTOSAR Blockset update/import
  ↓
Simulink adaptation
```

とする。

---

# 18. ModeMgr Quick Start

参照順序:

1. Methodology `§5`
2. `§6–§8`
3. `§9`
4. `§10.1`
5. `§17–§19`
6. `§20–§22`
7. `§30–§31`

最初に作るもの:

- [ ] ModeMgr Requirement Allocation
- [ ] input/output list
- [ ] shared type dependency list
- [ ] state-domain list
- [ ] AUTOSAR contract
- [ ] runnable/event list
- [ ] model scaffold
- [ ] MIL test list
- [ ] SIL test list
- [ ] delivery manifest skeleton

---

# 19. DiagMgr Quick Start

参照順序:

1. Methodology `§5`
2. `§7–§8`
3. `§12–§16`
4. `§17–§22`
5. `§30–§31`

最初に作るもの:

- [ ] DiagMgr Requirement Allocation
- [ ] communication observation inputs
- [ ] abstract CAN / CanSM state inputs
- [ ] counter/checksum definition
- [ ] node fault-state model
- [ ] bus fault-state model
- [ ] source-specific latch list
- [ ] FSA / Indicator arbitration I/O
- [ ] DTC-clear interaction table
- [ ] MIL/SIL fault-injection tests

---

# 20. 外部参照を探すとき

Methodologyと本Guide内の外部authorityは、次の順序でReference Indexから辿る。

```text
Methodology section / Guide Step
    ↓
20260902_ManagementECU_SWC_Reference_Index.yaml
    ↓
references/<authority-plane>/reference-locators.yaml
    ↓
fixed downstream route
    ↓
exact upstream repository / commit / path / section
```

Authority planes:

```text
downstream
vector
mathworks
autosar
project
```

`NOT_SPECIFIED_IN_SOURCE` / `NO_EXPLICIT_MAPPING` / `PROJECT_INPUT_REQUIRED` の項目を、推測で埋めてはいけない。

---

# 21. Final Boundary

SWC Developmentの終了点は、

> production RTE / BSW / OSへ統合可能な、検証済みApplication SWC implementation

である。

まだManagement ECU VECUではない。

次工程:

```text
SWC Delivery Package
    ↓
DaVinci Configurator Classic
    ↓
MICROSAR
    ↓
Production RTE / BSW / OS Integration
```