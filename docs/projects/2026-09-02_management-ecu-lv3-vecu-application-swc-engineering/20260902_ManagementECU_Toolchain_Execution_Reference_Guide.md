# Management ECU Lv3 VECU — Toolchain Execution & Reference Guide

**Date:** 2026-09-02  
**Scope:** task-oriented tool/reference navigation  
**Machine-readable companion:** `20260902_ManagementECU_Tool_Task_Reference_Matrix.yaml`

## 1. この文書の目的

このGuideの目的はSWCそのものを設計することではない。

利用者が、

> 「いま何をしたいのか」

から出発して、

```text
やりたいこと
  ↓
工程 / lifecycle phase
  ↓
使用するtool
  ↓
toolで行うengineering operation
  ↓
事前に読むReviewed Knowledge
  ↓
必要input
  ↓
output artifact
  ↓
exit condition
  ↓
次のtool / phase
```

を一意に辿れるようにする。

技術authorityそのものは本Guideではなく、`20260902_ManagementECU_SWC_Reference_Index.yaml` と `references/*/reference-locators.yaml` に記録されたexact-pinned Reviewed Knowledgeである。

## 2. 最初に使うファイル

目的別に以下を使い分ける。

| 欲しいもの | 開くファイル |
|---|---|
| SWC開発の所有権・境界・原則 | `20260902_ManagementECU_SWC_Development_Methodology.md` |
| SWC-D0〜D7を工程順に読む | `20260902_ManagementECU_SWC_Development_Step_by_Step_Guide.md` |
| 「何をしたいか」から逆引きする | **本Guide** |
| 機械可読なtask/tool/input/output/reference関係 | `20260902_ManagementECU_Tool_Task_Reference_Matrix.yaml` |
| exact repository / commit / path / sectionを調べる | `20260902_ManagementECU_SWC_Reference_Index.yaml` → `references/<plane>/reference-locators.yaml` |
| 未確定project requirement/tool/calibrationを確認する | `references/project/*.yaml` |

## 3. Referenceの読み方

本Guideでは `V-001`, `MW-002`, `AS-003`, `DS-004` のようなlocator IDを使用する。

```text
locator ID
  ↓
20260902_ManagementECU_SWC_Reference_Index.yaml
  ↓
references/vector|mathworks|autosar|downstream/reference-locators.yaml
  ↓
exact repository
exact commit/ref
Reviewed Knowledge path
section / locator
```

floating `main`、現在のvendor Web、一般知識で置換しない。

## 4. 全体ルート

### Application SWC Development

```text
Project Requirement / Tool Baseline
       │
       ▼
SWC-D0  Requirement Decomposition
       │  tool-neutral
       ▼
SWC-D1  AUTOSAR SWC Contract
       │  DaVinci Developer Classic
       │
       │  SWC Contract ARXML
       ▼
SWC-D2  Model Scaffold
       │  AUTOSAR Blockset / Simulink
       ▼
SWC-D3  Behavior
       │  Simulink / Stateflow
       ▼
SWC-D4  AUTOSAR Mapping
       │  AUTOSAR Blockset
       ▼
SWC-D5  MIL
       │  Simulink / MathWorks test environment
       ▼
SWC-D6  Production-intent Generation
       │  Embedded Coder
       ▼
SIL     generated implementation verification
       │
       ▼
SWC-D7  Contract Reconciliation
       │  DaVinci + MathWorks artifact comparison
       ▼
SWC Delivery Package
```

### その後

```text
SWC Delivery Package
       ↓
DaVinci Configurator / MICROSAR
       ↓
Production RTE / BSW / OS Integration
       ↓
vVIRTUALtarget
       ↓
Lv3 VECU
       ↓
CANoe / vTESTstudio
       ↓
Virtual Integration / Verification
       ↓
XCP / A2L runtime measurement-calibration
```

後半は現行SWC Methodologyのscope外であるため、現在はrole/handoff navigationまでとする。

## 5. 目的別 Quick Lookup

| やりたいこと | Task | 工程 | 主tool |
|---|---|---|---|
| 実projectのtool versionを固定したい | `TTR-000` | Pre-SWC | Project CM |
| ECU要求をSWC責務へ分解したい | `TTR-001` | SWC-D0 | Tool-neutral |
| SWCのports/interfaces/runnablesを定義したい | `TTR-002` | SWC-D1 | DaVinci Developer |
| SWC contractをARXMLで渡したい | `TTR-003` | D1→D2 | DaVinci Developer |
| ARXMLからSimulink modelを作りたい | `TTR-004` | SWC-D2 | AUTOSAR Blockset |
| algorithm/state machineを実装したい | `TTR-005` | SWC-D3 | Simulink / Stateflow |
| Simulink↔AUTOSAR mappingを設定したい | `TTR-006` | SWC-D4 | AUTOSAR Blockset |
| model behaviorをMILで検証したい | `TTR-007` | SWC-D5 | Simulink / test environment |
| C/H/implementation ARXMLを生成したい | `TTR-008` | SWC-D6 | Embedded Coder |
| generated implementationをSILで確認したい | `TTR-009` | SIL | MathWorks SIL workflow |
| DaVinci contractとgenerated ARXMLを照合したい | `TTR-010` | SWC-D7 | DaVinci + MathWorks review |
| integrationへ渡すSWC packageをまとめたい | `TTR-011` | Delivery | Project CM |
| algorithm/stateだけ変更したい | `TTR-012` | Change | Simulink / Stateflow |
| port/interface/runnableを変更したい | `TTR-013` | Change | DaVinci Developer |
| calibration contract/valueを変更したい | `TTR-014` | Change | Architecture / calibration control |
| production RTE/BSW/OSへ統合したい | `TTR-N01` | Next phase | Configurator / MICROSAR |
| Lv3 VECUを作りたい | `TTR-N02` | Next phase | vVIRTUALtarget |
| VECUをCANoeで統合・試験したい | `TTR-N03` | Next phase | CANoe / vTESTstudio |
| XCP/A2Lでmeasurement/calibrationしたい | `TTR-N04` | Next phase | CANape / XCP client |

## 6. DaVinci Developer Classicを使う場面

### 6.1 何のために使うか

Application SWCの**software-design contract**を所有する。

主対象:

```text
SWC/component identity
Ports
PortInterfaces
DataTypes
Runnables
RTEEvents / activation contract
RTE access contract
PIM / calibration identity
```

参照:

- `DS-001`
- `V-001`
- `V-004`
- `AS-001`
- `AS-003`

### 6.2 何をするか

1. accepted requirement allocationを読む。
2. Atomic SWC/componentを定義する。
3. requirementに必要なP/R PortとPortInterfaceを定義する。
4. shared datatypeをproject governanceに従い参照または定義する。
5. RunnableEntityとactivation/event contractを定義する。
6. required RTE data/service accessを定義する。
7. 必要ならPIM/calibration contract identityを定義する。
8. controlled SWC Contract ARXMLをexportする。

### 6.3 何をしないか

```text
DaVinci contract
    != Simulink behavior
    != generated implementation
    != production RTE/BSW/OS
```

Simulink側で同じarchitectureを独立再作成しない。

## 7. AUTOSAR Blocksetを使う場面

### 7.1 DaVinci ARXMLをSimulinkへ持ち込む

Task: `TTR-004`

参照:

- `MW-001` — model / architecture ownership
- `MW-002` — ARXML lifecycle
- `MW-003` — AUTOSAR mapping
- `AS-001` — SW-C ports/interfaces
- `AS-003` — Runnable/RTEEvent boundary

operation:

```text
DaVinci SWC Contract ARXML
      ↓
AUTOSAR ARXML importer workflow
      ↓
initial/update Simulink AUTOSAR representation
```

重要:

```text
ARXML artifact != Simulink representation
```

input ARXML revisionとinitial import / changed-ARXML updateの別を記録する。

### 7.2 AUTOSAR mappingを設定・確認する

Task: `TTR-006`

代表関係:

```text
Simulink Inport     ↔ AUTOSAR R-Port
Simulink Outport    ↔ AUTOSAR P-Port
Function/Subsystem  ↔ Runnable
Model Parameter     ↔ Calibration
Data Store          ↔ PIM where appropriate
```

実際のmappingはimport済みcontractとproject requirementを基準に確認する。

## 8. Simulink / Stateflowを使う場面

Task: `TTR-005`

### Simulink

主にalgorithm / calculation / coordination logicを実装する。

### Stateflow

明示的なstate / event / transition logicを実装する。

参照:

- `MW-005` — Stateflow behavior identity
- `MW-015` — fault injection/evidence boundary
- DiagMgr関連では `MW-012`, `AS-005`, `AS-006`, `AS-007`

重要な非collapse:

```text
Stateflow source behavior != generated implementation
DiagMgr != DCM != DEM
project counter/checksum != AUTOSAR E2E
native BUS_OFF != project BUS_FAILED_LATCHED
```

## 9. MILを行う場面

Task: `TTR-007`

参照:

- `MW-006` — MIL/SIL/PIL identity
- `MW-007` — test definition/execution/result
- `MW-008` — requirement traceability
- `MW-009` — coverage semantics
- `MW-015` — fault test/evidence boundary

基本形:

```text
Requirement
   ↓
Test definition / harness
   ↓
normal model simulation (MIL workflow)
   ↓
MIL result
   ├── verdict
   └── coverage where collected
```

```text
verdict != coverage
MIL result != SIL result
```

## 10. Embedded Coderを使う場面

Task: `TTR-008`

参照:

- `MW-004`
- `AS-002`

生成対象:

```text
C source
H headers
implementation ARXML
code-generation metadata
code-generation report
```

境界:

```text
code generation != compile != link
local RTE stub != production MICROSAR RTE
```

A2L生成を使用する場合も、A2Lはgenerated codeやlive XCP sessionとは別artifact identityとして扱う。参照 `MW-013`。

## 11. SILを行う場面

Task: `TTR-009`

参照:

- `MW-006`
- `MW-007`
- `MW-009`

normal model simulationではなくgenerated implementationをSIL identityで実行し、MILと別のresultを残す。

```text
MIL PASS != SIL PASS != VECU/HIL PASS
```

## 12. DaVinci contractとMathWorks生成物を照合する場面

Task: `TTR-010`

参照:

- `DS-004`
- `V-003`
- `V-004`
- `MW-002`
- `MW-004`

比較対象:

```text
SWC identity
ports / interfaces
datatypes
runnables / events
calibration / PIM
schema / package
unexpected AUTOSAR objects
```

round tripをbyte-for-byte identityと解釈しない。generated ARXMLを無条件にDaVinci source contractへ上書きしない。

## 13. 変更要求が来たときのtool選択

### Algorithm / state transition

```text
Simulink / Stateflow
  ↓
MIL
  ↓
Embedded Coder
  ↓
SIL
  ↓
Contract reconciliation
```

Task: `TTR-012`

### Port / Interface / Datatype / Runnable

```text
DaVinci Developer
  ↓
new ARXML revision
  ↓
AUTOSAR Blockset changed-ARXML update/import
  ↓
Simulink adaptation
```

Task: `TTR-013`

### Calibration

contract identity変更とvalue変更を分ける。

Task: `TTR-014`

## 14. SWC Development後のtoolchain

### DaVinci Configurator Classic / MICROSAR

Task: `TTR-N01`

既知role:

```text
SWC Delivery Package
   ↓
production RTE / BSW / OS integration
```

参照:

- `DS-003`
- `V-002`
- `AS-002`

ただし、Management ECU固有のConfigurator GUI/API手順やMICROSAR build sequenceは現時点で未compiled。

### vVIRTUALtarget

Task: `TTR-N02`

参照:

- `V-005`
- `V-006`
- `DS-011`

既知roleはbuild/package/executionとvirtual-SUT handoff。Management ECU固有のpackage recipeは未compiled。

### CANoe / vTESTstudio

Task: `TTR-N03`

参照:

- `V-006`
- `V-007`
- `V-010`

既知roleはdescription/data binding、virtual SUT integration、simulation/test。Management ECU固有configuration procedureは未compiled。

### CANape / XCP / A2L

Task: `TTR-N04`

参照:

- `DS-012`
- `DS-016`
- `V-011`
- `MW-011`
- `MW-013`
- `MW-014`

現時点ではCANape-specific runtime consumer authorityが `DS-016 = UNRESOLVED_AUTHORITY`。

したがって、CANoe/VNT/XCP類似性からCANape手順を推測してはいけない。

## 15. 現在の完成度

### できること

Application SWC Developmentについては、

- 何をしたいか
- どの工程か
- どのtoolを使うか
- そのtoolで扱うengineering object / operation
- 何をinputにするか
- 何をoutputするか
- どのReviewed Knowledgeを先に読むか
- 何ができたら次へ進むか

をtask単位で辿れる。

### まだできないこと

現在のauthority compilationは、すべてのtoolについて次の粒度まで保証してはいない。

```text
Menu A
  → Dialog B
  → Tab C
  → Property D = xxx
  → button E
```

または、

```text
exact API call 1
exact API call 2
exact command line
```

という**version-specific procedure**である。

この粒度が必要なら、次のresearch/work unitは設計作業ではなく、

> Tool Procedure Compilation

とし、各taskについてexisting exact-pinned Reviewed KnowledgeからGUI/API procedureを回収するのが適切である。

## 16. Stop Rule

このGuideを使用している段階では、project requirementが未入力であることを理由に具体的SWC設計を創作しない。

まず「どのtaskを実行するか」「どのtoolを開くか」「何を読むか」を確定し、その後に実project inputを適用する。