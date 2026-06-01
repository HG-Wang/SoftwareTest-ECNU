# Ch4.4 规约的逻辑覆盖 (Logic Coverage for Specifications)

## 概述

> **核心思想**：将逻辑覆盖准则应用于软件规约（specifications），从规约中的逻辑表达式推导测试用例。

规约可以是**形式化的**（formal）或**非形式化的**（informal）。无论哪种形式，规约中通常包含可以用逻辑表达式表示的约束和条件。

---

## 规约中的逻辑表达式

### 前置条件作为逻辑表达式

规约中的前置条件（preconditions）天然就是逻辑表达式。

> **示例：地址保存功能**
>
> 规约：用户保存地址时，系统验证地址格式并存储。
>
> **前置条件**：
> ```
> P = (street ≠ null) ∧ (city ≠ null) ∧ (zipCode ≠ null)
>     ∧ (zipCode matchesPattern "^[0-9]{5}$")
>     ∧ (country ∈ validCountries)
> ```
>
> 每个子句都是一个可测试的条件，可以直接应用逻辑覆盖准则。

---

## CNF 谓词的快捷方法 (Shortcut for CNF Predicates)

### 原理

对于**合取范式**（CNF, Conjunctive Normal Form）的谓词：

> **关键观察**：在 CNF 谓词 `P = A₁ ∧ A₂ ∧ A₃ ∧ ... ∧ Aₙ` 中，主主动子句（major clause）在**所有其他子句均为 true** 时最易被激活。

### 测试生成规则

对于 CNF 谓词 `P = A₁ ∧ A₂ ∧ ... ∧ Aₙ`，测试集为：

| 测试 | A₁ | A₂ | A₃ | ... | Aₙ | P |
|------|----|----|----|-----|----|---|
| t₀ (全真) | T | T | T | ... | T | T |
| t₁ (A₁为假) | **F** | T | T | ... | T | F |
| t₂ (A₂为假) | T | **F** | T | ... | T | F |
| t₃ (A₃为假) | T | T | **F** | ... | T | F |
| ... | ... | ... | ... | ... | ... | ... |
| tₙ (Aₙ为假) | T | T | T | ... | **F** | F |

> **模式**：1个"全真"测试 + n个"对角线为假"测试 = **n+1个测试**

### 示例

```java
// 前置条件：用户注册
// P = (username.length > 0) ∧ (password.length >= 8) ∧ (email.contains("@"))
```

| 测试 | username.length > 0 | password.length >= 8 | email.contains("@") | P | 说明 |
|------|---------------------|----------------------|---------------------|---|------|
| t₀ | T | T | T | T | 全真 |
| t₁ | F | T | T | F | username 为主动子句 |
| t₂ | T | F | T | F | password 为主动子句 |
| t₃ | T | T | F | F | email 为主动子句 |

---

## DNF 谓词的快捷方法 (Shortcut for DNF Predicates)

### 原理

对于**析取范式**（DNF, Disjunctive Normal Form）的谓词：

> **关键观察**：在 DNF 谓词 `P = D₁ ∨ D₂ ∨ D₃ ∨ ... ∨ Dₙ` 中，主主动子句在**所有其他子句均为 false** 时最易被激活。

### 测试生成规则

对于 DNF 谓词 `P = D₁ ∨ D₂ ∨ ... ∨ Dₙ`，测试集为：

| 测试 | D₁ | D₂ | D₃ | ... | Dₙ | P |
|------|----|----|----|-----|----|---|
| t₀ (全假) | F | F | F | ... | F | F |
| t₁ (D₁为真) | **T** | F | F | ... | F | T |
| t₂ (D₂为真) | F | **T** | F | ... | F | T |
| t₃ (D₃为真) | F | F | **T** | ... | F | T |
| ... | ... | ... | ... | ... | ... | ... |
| tₙ (Dₙ为真) | F | F | F | ... | **T** | T |

> **模式**：1个"全假"测试 + n个"对角线为真"测试 = **n+1个测试**

### 示例

```java
// 授课条件：满足以下任一条件即可选课
// P = (passedPrerequisite) ∨ (instructorApproval) ∨ (year >= SENIOR)
```

| 测试 | passedPrerequisite | instructorApproval | year >= SENIOR | P | 说明 |
|------|--------------------|--------------------|----------------|---|------|
| t₀ | F | F | F | F | 全假 |
| t₁ | T | F | F | T | prerequisite 为主动子句 |
| t₂ | F | T | F | T | approval 为主动子句 |
| t₃ | F | F | T | T | year 为主动子句 |

---

## CNF 与 DNF 的对比总结

| 特性 | CNF (合取范式) | DNF (析取范式) |
|------|----------------|----------------|
| **形式** | `A₁ ∧ A₂ ∧ ... ∧ Aₙ` | `D₁ ∨ D₂ ∨ ... ∨ Dₙ` |
| **激活条件** | 所有其他子句为 true | 所有其他子句为 false |
| **基准测试** | 全真 (T, T, ..., T) | 全假 (F, F, ..., F) |
| **对角线测试** | 每个子句依次为 F | 每个子句依次为 T |
| **测试数量** | n + 1 | n + 1 |
| **P 为 true 的测试数** | 1 | n |
| **P 为 false 的测试数** | n | 1 |

---

## 规约中逻辑的来源

规约中的逻辑表达式可以从多种来源提取：

### 1. 前置条件 (Preconditions)

```java
/**
 * @pre account != null && account.isActive() && amount > 0
 */
public void withdraw(Account account, double amount) { ... }
```

### 2. Java Assert 语句

```java
public void process(int[] data) {
    assert data != null : "Data array cannot be null";
    assert data.length > 0 : "Data array cannot be empty";
    // 处理逻辑...
}
```

### 3. 契约式设计 (Contracts)

```java
/**
 * @requires balance >= amount
 * @ensures balance == old(balance) - amount
 */
public double withdraw(double amount) { ... }
```

### 4. OCL (Object Constraint Language)

```
context Person::setAge(age: Integer)
  pre: age >= 0 and age <= 150
  post: self.age = age
```

### 5. 形式化语言 (Formal Languages)

使用 Z、VDM、Alloy 等形式化规约语言编写的规范，其中的逻辑表达式可以直接提取。

---

## 简化计算的优势

> **重要观察**：规约中的许多谓词以 DNF 或 CNF 形式出现，这大大简化了测试生成的计算。

| 来源 | 典型形式 | 原因 |
|------|----------|------|
| 前置条件 | CNF | 多个条件必须同时满足 |
| 授权规则 | DNF | 多种途径均可授权 |
| 业务规则 | CNF 或 DNF | 取决于规则的逻辑结构 |
| 错误条件 | DNF | 任一错误条件触发即报错 |

### 为什么规约比源代码更易处理？

1. **无内部变量**：规约中的变量通常是输入变量或状态变量，不需要求解中间计算
2. **无可达性问题**：规约描述的是整体约束，不涉及程序路径
3. **结构更清晰**：CNF/DNF 形式使得测试生成有规律可循
4. **无副作用**：规约中的逻辑表达式通常不包含副作用

---

## 总结

> **核心要点**：
>
> 1. 规约中的逻辑表达式可以直接应用覆盖准则
> 2. CNF 谓词的快捷测试：**全真 + 每个子句依次为假**（共 n+1 个测试）
> 3. DNF 谓词的快捷测试：**全假 + 每个子句依次为真**（共 n+1 个测试）
> 4. 规约中的谓词通常比源代码中的谓词更容易处理
> 5. 逻辑表达式的来源多样：前置条件、断言、契约、OCL、形式化语言

| 准则 | CNF 测试数 | DNF 测试数 | 备注 |
|------|-----------|-----------|------|
| PC | 2 | 2 | 最基本覆盖 |
| ICC | n+1 | n+1 | 快捷方法直接满足 |
| CACC | n+1 | n+1 | 快捷方法直接满足 |
| MACC | 可能更多 | 可能更多 | 需要额外的组合 |
| GACC | n+1 | n+1 | 与 CACC 类似 |
