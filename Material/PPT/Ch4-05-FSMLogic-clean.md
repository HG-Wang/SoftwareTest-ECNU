# Ch4.5 有限状态机的逻辑覆盖 (Logic Coverage of FSMs)

## 概述

> **核心思想**：有限状态机（FSM）本质上是图结构，节点表示状态（states），边表示转换（transitions），每条边带有逻辑守卫条件（logical guards）。对 FSM 应用逻辑覆盖准则，就是对这些守卫条件进行覆盖测试。

FSM 广泛用于**嵌入式软件**（embedded software）的建模，如控制系统、协议、用户界面等。

---

## FSM 的基本结构

| 组成部分 | 含义 | 逻辑覆盖中的角色 |
|----------|------|------------------|
| 节点 (Node) | 系统状态 | 测试的起点和终点 |
| 边 (Edge) | 状态转换 | 包含逻辑谓词（守卫条件） |
| 守卫条件 (Guard) | 转换发生的逻辑条件 | 逻辑覆盖的目标 |
| 初始状态 | 系统起始状态 | 测试的起始点 |
| 终止状态 | 系统结束状态 | 测试的验证点 |

---

## 示例：地铁列车系统 (Subway Train Example)

### 状态定义

地铁列车系统有以下4个状态：

| 状态 | 含义 |
|------|------|
| All Doors Open | 所有门打开 |
| Left Doors Open | 左侧门打开 |
| Right Doors Open | 右侧门打开 |
| All Doors Closed | 所有门关闭 |

### 守卫条件中的子句

守卫条件涉及以下6个子句：

| 子句 | 含义 | 变量名 |
|------|------|--------|
| 列车速度为0 | trainSpeed = 0 | A |
| 站台在左侧 | platform = left | B |
| 位置在站内 | location = inStation | C |
| 紧急停车 | emergencyStop = true | D |
| 强制开门 | overrideOpen = true | E |
| 位置在隧道内 | location = inTunnel | F |

### 守卫条件（谓词）

从 **All Doors Closed** 到 **Left Doors Open** 的转换守卫条件：

```
P = (trainSpeed = 0) ∧ (platform = left) ∧ (location = inStation 
    ∨ (emergencyStop ∧ overrideOpen ∧ location = inTunnel))
```

用变量表示：

```
P = A ∧ B ∧ (C ∨ (D ∧ E ∧ F))
```

> **结构分析**：
> - 外层是合取（AND）：A、B 和一个析取项必须同时为真
> - 内层是析取（OR）：可以在站内（C），或者在隧道内且紧急停车且强制开门（D∧E∧F）

---

## 确定性分析 (Determination Analysis)

使用 **XOR 方法**对每个子句进行确定性分析，确定主主动子句（major clause）的测试需求。

### 子句 A (trainSpeed = 0)

主主动条件：当 B=T, C=T 时（使其他子句满足）

| 测试 | A | B | C | D | E | F | P |
|------|---|---|---|---|---|---|---|
| t1 | T | T | T | - | - | - | T |
| t2 | F | T | T | - | - | - | F |

> A 改变时 P 改变，确定性满足。

### 子句 B (platform = left)

主主动条件：当 A=T, C=T 时

| 测试 | A | B | C | D | E | F | P |
|------|---|---|---|---|---|---|---|
| t3 | T | T | T | - | - | - | T |
| t4 | T | F | T | - | - | - | F |

### 子句 C (location = inStation)

主主动条件：当 A=T, B=T 时

| 测试 | A | B | C | D | E | F | P |
|------|---|---|---|---|---|---|---|
| t5 | T | T | T | - | - | - | T |
| t6 | T | T | F | - | - | - | ? |

> **关键问题**：当 C=F 时，P 的值取决于 D∧E∧F。这不是简单的 true/false 变化。

### 子句 D (emergencyStop)

主主动条件：当 A=T, B=T, C=F, E=T, F=T 时

| 测试 | A | B | C | D | E | F | P |
|------|---|---|---|---|---|---|---|
| t7 | T | T | F | T | T | T | T |
| t8 | T | T | F | F | T | T | F |

### 子句 E (overrideOpen)

主主动条件：当 A=T, B=T, C=F, D=T, F=T 时

| 测试 | A | B | C | D | E | F | P |
|------|---|---|---|---|---|---|---|
| t9 | T | T | F | T | T | T | T |
| t10 | T | T | F | T | F | T | F |

### 子句 F (location = inTunnel)

主主动条件：当 A=T, B=T, C=F, D=T, E=T 时

| 测试 | A | B | C | D | E | F | P |
|------|---|---|---|---|---|---|---|
| t11 | T | T | F | T | T | T | T |
| t12 | T | T | F | T | T | F | F |

---

## CACC 测试真值赋值

根据 CACC 准则，整理所有测试的真值赋值：

| 测试 | A | B | C | D | E | F | P | 主动子句 |
|------|---|---|---|---|---|---|---|----------|
| t1 | T | T | T | F | F | F | T | A,B,C |
| t2 | F | T | T | F | F | F | F | A |
| t3 | T | T | T | F | F | F | T | (重复 t1) |
| t4 | T | F | T | F | F | F | F | B |
| t5 | T | T | T | F | F | F | T | (重复 t1) |
| t6 | T | T | F | T | T | T | T | C (通过D∧E∧F) |
| t7 | T | T | F | T | T | T | T | (重复 t6) |
| t8 | T | T | F | F | T | T | F | D |
| t9 | T | T | F | T | T | T | T | (重复 t6) |
| t10 | T | T | F | T | F | T | F | E |
| t11 | T | T | F | T | T | T | T | (重复 t6) |
| t12 | T | T | F | T | T | F | F | F |

去重后的最小测试集：

| 测试 | A | B | C | D | E | F | P |
|------|---|---|---|---|---|---|---|
| t1 | T | T | T | F | F | F | T |
| t2 | F | T | T | F | F | F | F |
| t4 | T | F | T | F | F | F | F |
| t6 | T | T | F | T | T | T | T |
| t8 | T | T | F | F | T | T | F |
| t10 | T | T | F | T | F | T | F |
| t12 | T | T | F | T | T | F | F |

---

## 问题：不可行的子句组合

> **关键问题**：`inStation` 和 `inTunnel` 不能同时为 false。

在模型中，列车只有两个位置：**在站内**（inStation）或**在隧道内**（inTunnel）。因此：

```
C = inStation, F = inTunnel
¬C → F  (不在站内 → 必在隧道内)
¬F → C  (不在隧道内 → 必在站内)
```

这意味着 `C=F ∧ F=F` 的组合**不可行**（infeasible），因为列车必须在某个位置。

### 影响

某些测试用例可能因为这种约束而无法构造，需要：
- 识别不可行的组合
- 调整测试策略
- 记录不可行测试的原因

---

## 从 FSM 预期结果

### 主主动子句为 true 时

> 当主主动子句的值使谓词为 **true** 时，对应的**转换被触发**（transition taken）。

例如：测试 t1 中，P=true，列车从 "All Doors Closed" 转换到 "Left Doors Open"。

### 主主动子句为 false 时

> 当主主动子句的值使谓词为 **false** 时，对应的**转换不被触发**（transition not taken）。

例如：测试 t2 中，P=false，列车保持在 "All Doors Closed" 状态。

---

## 意外转换 (Accidental Transitions)

> **问题**：一个转换的 false 值可能是另一个转换的 true 值。

在 FSM 中，同一状态可能有多条出边（outgoing transitions），每条边有不同的守卫条件。

### 示例

从 "All Doors Closed" 状态：

| 转换 | 目标状态 | 守卫条件 |
|------|----------|----------|
| T1 | Left Doors Open | A ∧ B ∧ (C ∨ (D ∧ E ∧ F)) |
| T2 | Right Doors Open | A ∧ ¬B ∧ (C ∨ (D ∧ E ∧ F)) |
| T3 | All Doors Open | 特殊条件 |

当测试 T1 的守卫条件为 false 时（如 B=false），可能恰好满足了 T2 的守卫条件（¬B=true），导致**意外转换**。

### 应对策略

- 测试时需要记录**所有**可能发生的转换
- 验证只有预期的转换被触发
- 检查是否有意外的状态变化

---

## 测试自动化问题

将 FSM 逻辑覆盖应用于实际测试时，面临以下挑战：

### 1. 映射问题 (Mapping Problem)

| FSM 层面 | 程序层面 | 问题 |
|----------|----------|------|
| 状态名 | 程序变量/标志 | 命名可能不一致 |
| 守卫条件 | if/switch 条件 | 表达式形式可能不同 |
| 转换 | 方法调用/事件处理 | 触发机制可能不同 |

### 2. 可达性问题 (Reachability)

> 需要通过一系列转换才能到达测试的起始状态。

例如：要测试 "All Doors Closed → Left Doors Open"，需要先让列车到达 "All Doors Closed" 状态。

### 3. 可控性问题 (Controllability)

> 需要能够控制守卫条件中的变量值。

例如：`trainSpeed = 0` 需要能够控制列车速度，`platform = left` 需要能够设置站台位置。

---

## 复杂化问题

实际应用中，FSM 测试还会遇到以下复杂情况：

### 1. 同时按键 (Simultaneous Button Presses)

> 多个输入可能同时发生，导致守卫条件的求值顺序不确定。

### 2. 可达性前缀 (Prefix for Reachability)

> 为了到达测试起始状态，需要执行一系列前置转换（prefix sequence）。

```
初始状态 → [prefix] → 测试起始状态 → [被测转换] → 验证结束状态
```

### 3. 退出到终止状态 (Exit to End State)

> 测试完成后，需要通过一系列转换退出到终止状态或已知状态。

```
验证结束状态 → [suffix] → 终止状态/重置状态
```

### 完整测试序列结构

```
[初始化] → [前缀序列: 到达起始状态] → [被测转换] → [验证结果] → [后缀序列: 退出]
```

---

## 总结

> **核心要点**：
>
> 1. **FSM 广泛使用**：特别是在嵌入式软件中
> 2. **谓词通常显式存在于转换上**：守卫条件直接给出了逻辑表达式
> 3. **常见于嵌入式软件**：控制系统、协议、用户界面等

| 挑战 | 说明 | 应对策略 |
|------|------|----------|
| 不可行组合 | 某些子句值的组合在物理上不可能 | 识别并排除，记录原因 |
| 意外转换 | false 值可能触发其他转换 | 验证所有出边的触发情况 |
| 映射问题 | FSM 名称与程序名称不一致 | 建立明确的映射关系 |
| 可达性 | 需要前置序列到达起始状态 | 计算并执行前缀序列 |
| 可控性 | 需要控制守卫条件中的变量 | 使用测试桩（stubs）或模拟器 |
| 同时输入 | 多个输入同时发生 | 定义明确的优先级和求值顺序 |
