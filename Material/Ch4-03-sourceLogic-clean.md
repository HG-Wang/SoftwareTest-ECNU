# Ch4.3 源代码的逻辑覆盖 (Logic Coverage for Source Code)

## 概述

> **核心思想**：将逻辑覆盖准则应用于程序源代码，通过分析源代码中的谓词（predicates）来生成测试用例。

对源代码应用逻辑覆盖准则的过程与规约（specifications）有所不同。源代码中的谓词通常包含**内部变量**（internal variables），这些变量的值由程序的前置计算决定，使得约束求解更加复杂。

---

## 应用逻辑覆盖的步骤

对源代码应用逻辑覆盖准则的一般步骤如下：

| 步骤 | 操作 | 说明 |
|------|------|------|
| 1 | 提取谓词 (Extract Predicates) | 从源代码的条件语句中提取逻辑谓词 |
| 2 | 分析可达性 (Analyze Reachability) | 确定谓词所在代码路径的可达性约束 |
| 3 | 求解内部变量 (Solve Internal Variables) | 确定内部变量的取值方式 |
| 4 | 求解可达性约束 (Solve Reachability Constraints) | 结合可达性约束生成满足条件的输入 |
| 5 | 推导测试用例 (Derive Test Cases) | 根据求解结果生成具体的测试输入和预期输出 |

---

## 示例1：三角形问题 (Triangle Example)

### 提取谓词

三角形程序中的典型 `if` 语句：

```java
if (a + b > c && a + c > b && b + c > a) {
    triOut = "TRIANGLE";
    // 进一步判断类型
    if (a == b && b == c) {
        triOut = "EQUILATERAL";
    } else if (a == b || b == c || a == c) {
        triOut = "ISOSCELES";
    } else {
        triOut = "SCALENE";
    }
} else {
    triOut = "NOT_A_TRIANGLE";
}
```

提取出的谓词结构：

> **谓词1**：`P = (a + b > c) ∧ (a + c > b) ∧ (b + c > a)`
>
> **谓词2**：`Q = (a == b) ∧ (b == c)`
>
> **谓词3**：`R = (a == b) ∨ (b == c) ∨ (a == c)`

### 分析可达性

- 谓词 `Q` 仅在 `P` 为 `true` 时可达
- 谓词 `R` 仅在 `P` 为 `true` 且 `Q` 为 `false` 时可达

### 求解内部变量

关键问题：内部变量 `triOut` 的值取决于谓词的求值路径。

> **难点**：`triOut` 不是输入变量，而是由程序逻辑赋值的内部变量。测试用例需要通过控制输入变量 `(a, b, c)` 来使得 `triOut` 取期望的值。

对于 CACC 准则，需要：
- 对于谓词 `P` 的每个子句，生成使其为主动子句（major clause）的测试
- 确保 `triOut` 的值与谓词求值路径一致

### 达到性约束求解示例

要测试谓词 `P` 中子句 `(a + b > c)` 的 CACC：

| 测试 | a+b>c | a+c>b | b+c>a | P | 期望 triOut |
|------|-------|-------|-------|---|-------------|
| t1 | T | T | T | T | TRIANGLE |
| t2 | F | T | T | F | NOT_A_TRIANGLE |
| t3 | F | T | T | F | NOT_A_TRIANGLE |
| t4 | F | F | F | F | NOT_A_TRIANGLE |

---

## 示例2：恒温器问题 (Thermostat Example)

### 简化谓词

恒温器程序中的典型谓词：

```java
if (temp < setPoint - delta && mode == HEAT) {
    heaterOn = true;
} else if (temp > setPoint + delta && mode == COOL) {
    coolerOn = true;
} else {
    heaterOn = false;
    coolerOn = false;
}
```

提取的谓词：

> **谓词**：`P = (temp < setPoint - delta) ∧ (mode == HEAT)`

### 可达性分析

- 第二个 `else if` 分支仅在第一个条件为 `false` 时可达
- `else` 分支在两个条件均为 `false` 时可达

### CACC 测试推导（6个测试）

对谓词 `P = A ∧ B`，其中：
- `A = (temp < setPoint - delta)`
- `B = (mode == HEAT)`

| 测试 | A | B | P | heaterOn | coolerOn | 说明 |
|------|---|---|---|----------|----------|------|
| t1 | T | T | T | true | false | 两个子句均为主动 |
| t2 | F | T | F | false | false | A 为主动子句 |
| t3 | F | T | F | false | false | A 的否定对测试 |
| t4 | T | F | F | false | false | B 为主动子句 |
| t5 | T | F | F | false | false | B 的否定对测试 |
| t6 | F | F | F | false | false | 两个子句均为 false |

> **关键点**：6个测试用例涵盖了所有子句的 CACC 要求。每个子句作为主主动子句时，其他子句的取值固定，通过改变主主动子句的值来观察谓词结果的变化。

---

## 程序变换问题 (Program Transformation Issues)

当谓词结构复杂时，开发者可能会对代码进行变换。但这种变换可能引入新的问题。

### 原始谓词

```java
if ((a && b) || c) {
    // ...
}
```

### 变换1：嵌套 if-else

```java
if (a) {
    if (b) {
        // 执行目标代码
    } else {
        if (c) {
            // 执行目标代码
        }
    }
} else {
    if (c) {
        // 执行目标代码
    }
}
```

> **问题分析**：
> - **维护更困难**：原本一个条件变成了多个分支，代码结构更复杂
> - **可达性更难分析**：需要分析多个嵌套路径的可达性
> - **PC 不兼容**：对变换后代码应用 PC（Predicate Coverage）准则，**不等于**对原始代码应用 CACC 准则

### 变换2：引入中间变量

```java
boolean temp1 = a && b;
boolean temp2 = temp1 || c;
if (temp2) {
    // 执行目标代码
}
```

> **问题分析**：
> - 复杂性被转移到了计算过程中
> - 逻辑覆盖准则对计算（computations）效果不佳
> - 谓词的逻辑结构被隐藏，难以直接应用 CACC 等准则

### 变换准则总结

| 变换方式 | 优点 | 缺点 |
|----------|------|------|
| 嵌套 if-else | 结构清晰 | 维护困难，可达性复杂，PC ≠ CACC |
| 中间变量 | 简化单个条件 | 隐藏逻辑结构，准则效果降低 |
| 不变换 | 保持原始结构 | 需要处理复杂谓词 |

---

## 谓词中的副作用 (Side Effects in Predicates)

某些情况下，谓词的求值可能产生**副作用**，改变变量的值。

### 示例

```java
if (A && (B || A)) {
    // ...
}
```

如果 `B` 的求值会改变 `A` 的值（例如 `B` 是一个方法调用，修改了 `A` 引用的对象状态），则：

> **问题**：
> - 第一次出现的 `A` 和第二次出现的 `A` 可能具有不同的值
> - 逻辑等价变换（如短路求值）可能改变程序行为
> - 覆盖准则需要考虑求值顺序的影响

### 建议

- 避免在谓词中包含有副作用的表达式
- 如果无法避免，需要记录变量在谓词求值过程中的变化
- 测试用例需要验证副作用的正确性

---

## 总结

> **核心要点**：
>
> 1. **大多数谓词的子句数量少于4个**，因此逻辑覆盖准则的计算复杂度通常可控
> 2. **最困难的部分是求解内部变量**——确定输入值使得内部变量取期望的值
> 3. **避免使用隐藏谓词结构的程序变换**——变换可能使覆盖准则失去有效性
> 4. **注意谓词中的副作用**——副作用可能导致逻辑等价假设不成立

| 关键挑战 | 应对策略 |
|----------|----------|
| 内部变量求解 | 使用符号执行或约束求解技术 |
| 可达性分析 | 从入口点开始，逐步分析路径条件 |
| 副作用 | 避免或显式处理，记录变量变化 |
| 代码变换 | 保持谓词原始结构，不进行不必要的变换 |
