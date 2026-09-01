# Management ECU — SWC Development Methodology

## Vector DaVinci Developer + MathWorks AUTOSAR Blockset / Embedded Coder

## 1. Purpose

本方法論は、Management ECUのVECU開発構想を複数の開発領域へ分割したうえで、その最初の領域である **Application Software Component Development** を対象とする。

対象SWCは、現時点で以下の6コンポーネントとする。

- `ModeMgr`
- `FuelMgr`
- `AirMgr`
- `ThermalMgr`
- `ElectricalMgr`
- `DiagMgr`

本工程の目的は、要求仕様からAUTOSAR Classic SWC contractを定義し、Simulink / Stateflowでbehaviorを実装し、production-intentのAUTOSAR C codeおよびARXMLを生成して、後続のDaVinci Configurator Classic / MICROSAR ECU Integration工程へ引き渡せる状態まで完成させることである。

---

# 2. Overall VECU Development Decomposition

Management ECU VECU開発全体は、少なくとも以下の領域へ分離する。

```text
Management ECU Requirements
        │
        ▼
┌───────────────────────────────────────┐
│ 1. SWC Development                    │
│                                       │
│ DaVinci Developer                     │
│ Simulink / Stateflow                  │
│ AUTOSAR Blockset                      │
│ Embedded Coder                        │
└───────────────────┬───────────────────┘
                    │
             SWC C + ARXML
                    │
                    ▼
┌───────────────────────────────────────┐
│ 2. ECU Integration                    │
│                                       │
│ DaVinci Configurator Classic          │
│ MICROSAR Classic                      │
│ RTE / BSW / OS                        │
└───────────────────┬───────────────────┘
                    │
             Integrated ECU SW
                    │
                    ▼
┌───────────────────────────────────────┐
│ 3. VECU Construction                  │
│                                       │
│ vVIRTUALtarget                        │
└───────────────────┬───────────────────┘
                    │
                    ▼
┌───────────────────────────────────────┐
│ 4. Virtual Integration / Verification │
│                                       │
│ CANoe                                 │
│ vTESTstudio                           │
│ CANape                                │
└───────────────────────────────────────┘
```

本書で扱うのは **1. SWC Development** のみとする。

RTE、BSW、OS、VECU packaging、CANoe environment、XCP runtime、UDS tester executionは後工程とし、SWC Development工程ではそれらを模擬・仮定してApplication behaviorを検証するに留める。

---

# 3. Fundamental Ownership Model

本Tool Chainでは、各ツールに異なるauthorityを与える。

最も重要なルールは、

> **同じ設計情報をDaVinci DeveloperとSimulinkの双方で独立してauthorしない。**

ことである。

基本ownershipを次のように固定する。

| Engineering object                   | Source of truth                 |
| ------------------------------------ | ------------------------------- |
| ECU application composition          | DaVinci Developer               |
| SWC type                             | DaVinci Developer               |
| Port / PortInterface                 | DaVinci Developer               |
| Data type contract                   | DaVinci Developer               |
| Runnable definition                  | DaVinci Developer               |
| Runnable trigger/event               | DaVinci Developer               |
| RTE access contract                  | DaVinci Developer               |
| PIM / calibration interface identity | DaVinci Developer               |
| Algorithm behavior                   | Simulink                        |
| State machine behavior               | Stateflow                       |
| Fault-detection algorithm            | Simulink / Stateflow            |
| Control calculation                  | Simulink                        |
| Application arbitration              | Simulink / Stateflow            |
| AUTOSAR ↔ Simulink mapping           | AUTOSAR Blockset                |
| Application C generation             | Embedded Coder                  |
| Production RTE                       | DaVinci Configurator / MICROSAR |
| BSW configuration                    | DaVinci Configurator            |
| OS configuration                     | DaVinci Configurator            |

Reviewed Knowledgeでも、DaVinci DeveloperはSWC、composition、ports/interfaces、runnable、data type等のsoftware-design側を担当し、Developer単独がBSW/RTE生成を所有するものではない。

---

# 4. Canonical SWC Development Flow

SWC Developmentのcanonical flowを以下とする。

```text
Project Requirements
        │
        ▼
DaVinci Developer
  AUTOSAR Application Architecture
        │
        │ SWC Contract ARXML
        ▼
AUTOSAR Blockset
        │
        ▼
Simulink / Stateflow
  SWC Behavior Implementation
        │
        │ AUTOSAR Mapping
        ▼
Embedded Coder
        │
        ├── Generated C / H
        ├── Implementation ARXML
        ├── Code generation metadata
        └── Code generation report
        │
        ▼
DaVinci / AUTOSAR Integration Review
        │
        ▼
SWC Delivery Package
        │
        ▼
DaVinci Configurator Classic
        │
        ▼
Production RTE / BSW / OS Integration
```

MathWorks Reviewed Knowledgeでも、ARXML import → Simulink representation → code/ARXML generation → external AUTOSAR authoring toolへのdeliveryというround-trip lifecycleが確認されている。

---

# 5. SWC Development Phases

## SWC-D0 — Requirement Decomposition

### Purpose

ECU要求を、Application SWCが所有すべきbehaviorと、RTE/BSW/OS/Networkが所有すべきbehaviorへ分解する。

### Tool

特定ツールには依存しない。

要求IDを保持したproject requirement artifactをsourceとする。

### Example

Maintenance Mode要求：

```text
Upper ECU Maintenance Request
UDS RoutineControl Maintenance Request
Upper ECU request has higher priority
```
を、

```text
Application responsibility
    Mode arbitration
    Maintenance ownership
    State transition

Diagnostic stack responsibility
    RoutineControl service decoding
    NRC transmission
```

へ分離する。

### Output

各requirementについて最低限、

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

を決定する。

---

# 6. SWC-D1 — AUTOSAR Application Architecture Definition

## Tool

**DaVinci Developer Classic**

## Purpose

Application behaviorを記述する前に、SWC contractを確定する。

### Initial Management ECU Composition

```text
ManagementECU_Application
│
├── ModeMgr
├── FuelMgr
├── AirMgr
├── ThermalMgr
├── ElectricalMgr
└── DiagMgr
```

各SWCは原則としてAtomic SWCとして定義する。

---

## 6.1 Port / Interface Definition

例：

```text
Upper ECU
    │
    ▼
ModeMgr
    │
    ├── ModeCommand
    ├── MaintenanceState
    └── SystemOperatingState
```

Driver側は例えば、

```text
FuelMgr
    │
    ├── FuelCommand
    └── FuelStatus
```

とする。

DaVinci Developerでは、

- Sender/Receiver
- Client/Server
- Mode
- Calibration
- NV data
- Trigger

等を別interface categoryとして扱える。

---

# 7. Runnable Architecture

各SWCについて、

```text
SWC
 ├── initialization runnable
 ├── cyclic runnable
 ├── event-driven runnable
 └── service-related runnable
```

を必要に応じて定義する。

周期そのものはproject requirementから決定し、本方法論では固定しない。

例：

```text
ModeMgr
 ├── ModeMgr_Init
 └── ModeMgr_Main

FuelMgr
 ├── FuelMgr_Init
 └── FuelMgr_Main
```

DiagMgrについてはApplication側の診断・故障policyのみを所有させる。

```text
DiagMgr
    owns:
        project fault confirmation
        fault latch
        FSA arbitration inputs
        indicator request
        application diagnostic policy

DCM
    owns:
        UDS protocol/service/session/security

DEM
    owns:
        event/DTC status
        event memory
```

したがって、

```text
DiagMgr != DCM
DiagMgr != DEM
```

とする。

---

# 8. Data Type and Shared Interface Governance

Management ECUで複数SWCから使用する共通型はDaVinci Developer側で定義する。

例：

```text
OperatingMode_t
MaintenanceOwner_t
FaultState_t
NodeHealth_t
BusHealth_t
FsaLevel_t
```

推奨package構造例：

```text
/ManagementECU
    /DataTypes
    /PortInterfaces
    /Components
        /ModeMgr
        /FuelMgr
        /AirMgr
        /ThermalMgr
        /ElectricalMgr
        /DiagMgr
    /Compositions
```

SWCモデル側で独自に同名型を再定義しない。

---

# 9. SWC-D2 — MathWorks Model Scaffold Generation

## Tool

- AUTOSAR Blockset
- Simulink
- Stateflow

## Input

DaVinci DeveloperからexportしたSWC ARXML。

```text
DaVinci Developer
        │
        ▼
Software Component ARXML
        │
        ▼
AUTOSAR Blockset importer
```

## Result

SWC contractに対応したSimulink AUTOSAR component modelを生成する。

MathWorksのreviewed lifecycleでは、

```text
ARXML
  → arxml.importer
  → initial Simulink representation
```

とされており、ARXML artifactそのものとSimulink representationは別identityである。

---

# 10. SWC-D3 — Behavior Implementation

## 10.1 ModeMgr

主にStateflowを使用する。

例：

```text
OperationalState
 ├── STARTUP
 ├── NORMAL
 ├── MAINTENANCE
 ├── FSA
 └── SHUTDOWN
```

ただしfault stateやcommunication stateまで一つの巨大state machineへ統合しない。

例えば、

```text
Operational Mode
Maintenance Ownership
Fault Arbitration
Communication Health
```

は別state domainとして扱う。

### Maintenance Ownership

```text
NONE
UPPER_ECU
UDS
```

Priority：

```text
UPPER_ECU > UDS
```

Upper ECU起点Maintenance中のUDS要求は、

```text
ConditionsNotCorrect
```

相当のapplication resultを返す。

実際のUDS NRC生成はDCM側で行う。

---

# 11. Fuel / Air / Thermal / Electrical Manager

これらは主としてSimulinkで記述する。

一般形：

```text
Mode / Request
       │
       ▼
Control / Coordination Logic
       │
       ▼
Driver Command
       │
       ▼
Driver Status / Feedback
```

例えばFuelMgr：

```text
Generation Demand
Operating Mode
Fuel Driver Status
Calibration
        │
        ▼
Fuel Control Logic
        │
        ▼
Fuel Command
```

状態遷移を必要とする部分だけStateflowを使用する。

---

# 12. DiagMgr

DiagMgrはproject/application-specific fault semanticsを所有する。

初期allocation候補：

```text
Communication observation
        │
        ▼
DiagMgr
 ├── message supervision
 ├── counter stuck detection
 ├── checksum judgement
 ├── node failure confirmation
 ├── bus failure latch
 ├── fault-source latch
 └── FSA / Indicator arbitration
        │
        ▼
ModeMgr
```

ただし、

```text
physical CAN error state
CAN controller BUS_OFF
CanSM communication state
DEM event memory
DCM diagnostic service
```

はDiagMgr内部behaviorとして再実装しない。

Applicationが必要とする抽象化されたstate/inputをRTE経由で受け取る設計とする。

---

# 13. Project-Specific Counter / Checksum

今回のproject mechanismはAUTOSAR E2Eとは独立して扱う。

Counter：

```text
Current == Previous
    → invalid

Current != Previous
    → valid
```

したがって、

```text
0 → 2
```

はvalidである。

Checksum：

```text
Checksum = (0x10 - W) mod 0x10
```

これは、

```text
PROJECT_SPECIFIC_DESIGN
```

であり、

```text
AUTOSAR E2E Profile
```

へ自動対応付けしない。

実装場所はSWC/application layerまたは後に決定する明示的integration componentとし、AUTOSAR E2E Transformerへ暗黙置換しない。

---

# 14. Communication Fault State Model

SWC Development側では、少なくとも次の論理状態をmodel化する。

### Node

```text
HEALTHY
      │
      ▼
FAILURE_CONFIRMING
      │
      ▼
FAILED_LATCHED
```

解除：

```text
next startup
OR
corresponding DTC clear
```

### Bus

```text
BUS_HEALTHY
      │
CAN BUS_OFF indication
      ▼
BUS_OFF_CONFIRMING
      │
confirmation time
      ▼
BUS_FAILED_LATCHED
```

解除：

```text
next startup
OR
corresponding DTC clear
```

native CAN controller BUS_OFFとproject-level `BUS_FAILED_LATCHED`は別identityとする。

---

# 15. Bus-Off Mask Behavior

native bus-off active中はnode supervision timerを、

```text
FREEZE
```

する。

```text
Timer = 70
BUS_OFF
Timer = 70  ← frozen
BUS recovery
Timer resumes from 70
```

RESETではない。

このbehaviorはSimulink / Stateflow MIL段階から検証可能である。

---

# 16. DTC Clear Interaction

Fault sourceは個別にlatchを保持する。

```text
Fault A ─┐
Fault B ─┼──► Fault Arbitration ──► FSA
Fault C ─┘
```

一つのDTCをclearしたとき、

```text
clear corresponding latch
        ↓
re-evaluate remaining fault sources
        ↓
calculate FSA / Indicator again
```

とする。

単一global fault bitを使用しない。

---

# 17. SWC-D4 — AUTOSAR Mapping

## Tool

AUTOSAR Blockset

Simulink objectとAUTOSAR contractをmappingする。

主なmapping対象：

```text
Simulink Inport
    ↔ AUTOSAR R-Port

Simulink Outport
    ↔ AUTOSAR P-Port

Function / Subsystem
    ↔ Runnable

Model Parameter
    ↔ Calibration Parameter

Data Store
    ↔ PIM where appropriate
```
このmapping工程で、

```text
algorithm model
```

を、

```text
AUTOSAR implementation model
```

へ変換する。

---

# 18. SWC-D5 — Model-Level Verification

コード生成前にSWC単体behaviorを検証する。

最低限のtest category：

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

ModeMgrでは特に、

```text
Upper request
UDS request
simultaneous request
fault during Maintenance
fault clear
startup reset
```

を確認する。

---

# 19. MIL / SIL Separation

SWC Developmentでは少なくとも、

```text
MIL
    model behavior

SIL
    generated implementation behavior
```

を分離する。

```text
MIL PASS
    !=
SIL PASS
```

とする。

後続のVECU executionもSIL結果とは別verification stageである。

---

# 20. SWC-D6 — Production-Intent Code Generation

## Tool

Embedded Coder

生成物：

```text
Simulink AUTOSAR Model
        │
        ▼
Embedded Coder
        │
        ├── C source
        ├── H headers
        ├── AUTOSAR ARXML
        ├── build metadata
        └── code generation report
```

Reviewed MathWorks knowledgeでも、

```text
code generation
!= compile
!= link
```

が明確に分離されている。

---

# 21. Production RTE Boundary

Embedded Coderが生成するApplication codeはRTE APIを使用する。

例：

```c
Rte_Read_...
Rte_Write_...
Rte_Call_...
```

MathWorks local buildではRTE stubを使用できるが、

```text
MathWorks RTE stub
    !=
production MICROSAR RTE
```

である。

Reviewed Knowledgeでもproduction ECU integrationではMathWorks stubをexternal production RTE generator outputへ置き換える必要がある。

Management ECUではproduction RTEを、

```text
DaVinci Configurator
+
MICROSAR
```

側で生成する。

---

# 22. SWC-D7 — AUTOSAR Contract Reconciliation

コード生成後、MathWorksから得たARXMLをそのまま無条件にDaVinci projectへ上書きしない。

必ず、

```text
Original DaVinci contract
        │
        ├──── compare
        │
Generated MathWorks ARXML
        │
        ▼
Integration decision
```

を行う。

チェック対象：

- SWC identity
- port identity
- interface identity
- datatype identity
- runnable identity
- event mapping
- calibration identity
- PIM identity
- AUTOSAR schema version
- package path
- unexpected newly generated AUTOSAR object
MathWorksのround-tripはstructure/element/UUID等のpreservationをサポートするが、byte-for-byte identityやuniversal automatic mergeではない。

---

# 23. Change Management Rules

## 23.1 Behavior-Only Change

例：

```text
Fuel calculation変更
State transition condition変更
Fault confirmation logic変更
```

Flow：

```text
Simulink / Stateflow
    ↓
MIL
    ↓
SIL
    ↓
Code generation
```

DaVinci contractは変更しない。

---

## 23.2 Interface Change

例：

```text
Port追加
Signal追加
Datatype変更
Runnable追加
```

Flow：

```text
Change Request
    ↓
DaVinci Developer
    ↓
new ARXML
    ↓
AUTOSAR Blockset update/import
    ↓
Simulink model adaptation
```

**Simulink側だけでarchitectureを追加してDaVinciへ押し戻すことを原則禁止する。**

---

# 24. Shared Definition Change

例えば、

```text
OperatingMode_t
```

を変更する場合：

```text
DaVinci Developer
        ↓
shared ARXML
        ↓
MathWorks update
        ↓
affected model validation
        ↓
regeneration
```

とする。

全SWCへの影響を明示的に確認する。

---

# 25. Calibration Change

Calibrationについては二つを分離する。

### Contract

```text
parameter identity
datatype
range/unit where contractually defined
AUTOSAR calibration exposure
```

→ architecture/integration control

### Project calibration value

```text
X
Y
Z
threshold
confirmation time
```

→ project calibration data

例えばSecurityAccessの、

```text
X
Y
Z
```

はproject-specific calibrationである。

SWC Developmentではalgorithmとparameter accessを実装するが、実runtime calibrationは後続XCP/CANape工程で扱う。

---

# 26. Recommended SWC-Specific Allocation

| SWC           | Primary modeling approach     | Major responsibility                                     |
| ------------- | ----------------------------- | -------------------------------------------------------- |
| ModeMgr       | Stateflow + Simulink          | operating state / Maintenance arbitration / FSA reaction |
| FuelMgr       | Simulink                      | fuel coordination/control                                |
| AirMgr        | Simulink                      | air coordination/control                                 |
| ThermalMgr    | Simulink + optional Stateflow | thermal coordination/control                             |
| ElectricalMgr | Simulink + optional Stateflow | electrical coordination/control                          |
| DiagMgr       | Stateflow + Simulink          | project fault confirmation/latching/arbitration          |

---

# 27. Artifact Baseline

SWC Developmentでは成果物identityを分離して管理する。

```text
Requirement
    ↓
AUTOSAR SWC Contract
    ↓
Simulink Model
    ↓
Generated C
    ↓
Generated ARXML
```

これらを同一artifactとして扱わない。

特に、

```text
Simulink model
    !=
AUTOSAR contract

AUTOSAR contract
    !=
generated C

generated C
    !=
production ECU integration
```

を維持する。

---

# 28. Recommended Repository Layout

例：

```text
management-ecu/
│
├── requirements/
│
├── autosar/
│   ├── architecture/
│   ├── shared/
│   └── swc/
│
├── models/
│   ├── ModeMgr/
│   ├── FuelMgr/
│   ├── AirMgr/
│   ├── ThermalMgr/
│   ├── ElectricalMgr/
│   └── DiagMgr/
│
├── generated/
│   ├── code/
│   └── arxml/
│
├── tests/
│   ├── mil/
│   └── sil/
│
├── reports/
│
└── integration/
```

`generated/`はderived artifactとして扱い、人手編集しない。

---

# 29. Tool Version Pinning

各baselineでは最低限、

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

を固定する。

現在のReviewed Knowledge baselineは、

- DaVinci Developer Classic: 4.18 SP3 family
- DaVinci Configurator Classic: 6.3.10
- MathWorks: R2025b

である。

実プロジェクトで異なるreleaseを使用する場合は、そのrelease combinationについてcompatibilityを別途固定する。

---

# 30. SWC Delivery Package

一つのSWCの完了成果物は最低限以下とする。

```text
SWC Delivery
│
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

Delivery Manifestには、

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

を保持する。

---

# 31. Definition of Done — SWC Development

各SWCについて以下を満たした時点でSWC Developmentを完了とする。

### Contract

- DaVinci Developer上でSWC contractが確定している
- Port / Interface / Datatypeが確定している
- Runnable / Eventが確定している
- RTE access contractが確定している

### Model

- ARXMLからmodel scaffoldが成立している
- AUTOSAR mappingが完成している
- Application behaviorが実装されている

### Verification

- Requirement traceabilityが存在する
- MILがPASSしている
- SILがPASSしている
- major state/fault transitionが検証されている

### Generation

- Embedded Coder generationがPASSしている
- C/Hが生成されている
- implementation ARXMLが生成されている
- code-generation reportが生成されている

### Reconciliation

- DaVinci contractとgenerated ARXMLの差分を確認している
- unintended architecture changeがない
- unresolved AUTOSAR mappingがない

### Delivery

- SWC Delivery Packageがversion-fixedである
- DaVinci Configuratorへのhandoff readinessが確認されている

---

# 32. Boundary to the Next VECU Phase

SWC Development完了時点では、まだVECUではない。

```text
SWC Development Complete
        │
        ▼
C + ARXML
        │
        ▼
DaVinci Configurator
        │
        ▼
MICROSAR
  RTE
  COM
  PduR
  CanIf
  CanSM
  ComM
  EcuM
  BswM
  DCM
  DEM
  NvM
  OS
        │
        ▼
Integrated ECU Software
        │
        ▼
vVIRTUALtarget
        │
        ▼
Management ECU VECU
```

DaVinci Configuratorのreviewed roleはMICROSAR Classic BSW/RTE configuration、OS/task configuration、validationおよびgenerationである。

したがって、

> **SWC Developmentの終了点は「VECUが動くこと」ではなく、「production RTE/BSW/OSへ統合可能な、検証済みApplication SWC implementationが完成していること」**

と定義する。

---

# 33. Canonical Development Principle

Management ECUのVector + MathWorks Tool Chainでは、最終的に以下のownershipを維持する。

```text
Requirements
    │
    ▼
DaVinci Developer
AUTOSAR Application Contract
    │
    ▼
Simulink / Stateflow
Application Behavior
    │
    ▼
Embedded Coder
Generated Implementation
    │
    ▼
DaVinci Configurator / MICROSAR
Production ECU Integration
    │
    ▼
vVIRTUALtarget
Virtual ECU Runtime
    │
    ▼
CANoe / vTESTstudio / CANape
System Verification
```

これは、

```text
Application architecture
    !=
AUTOSAR contract
    !=
behavior model
    !=
generated implementation
    !=
production RTE / BSW / OS
    !=
VECU runtime
```

という境界を維持しながら、各ツールをその最も強い役割で利用する開発方法論である。