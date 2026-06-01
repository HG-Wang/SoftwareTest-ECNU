# Ch5.2 Program-based Grammars（基于程序的文法）

## 课程目标

- 明确在程序中应用变异测试的过程；能说出变异测试的特点
- 明确被测程序（基本串）、变体和测试之间的关系
- 明确变体的种类和基本的变异运算符
- 明确强杀死变体、弱杀死变体的含义及它们与 RIPR 模型间的关联
- 能针对变体分析到达、感染、传播条件
- 能针对程序分析满足强杀死变体或弱杀死变体的测试用例

---

## 1. 概述

- 基于语法的标准起源于程序，且主要用于程序
- BNF 标准最常用于**测试编译器**
- 变异测试标准最常用于类的**单元测试**和**集成测试**

---

## 2. BNF 测试用于编译器（5.2.1）

- 测试编译器非常复杂：数百万个正确程序！编译器必须识别并拒绝错误程序
- BNF 标准可用于生成程序以测试编译器必须处理的所有语言特性
- 这是一种非常专业化的应用

---

## 3. 基于程序的变异测试（5.2.2）

### 3.1 基本流程

- 基于语法测试最原始和最广为人知的应用是**修改程序**
- 运算符修改基本字符串（被测程序）以创建**变体程序**
- 变体程序必须能正确编译（有效字符串）
- 变体不是测试，而是用于**寻找测试**
- 一旦定义了变体，必须找到测试使变体在执行时失败 → 即"杀死变体"

### 3.2 变体的分类

| 类型 | 说明 |
|------|------|
| **Dead mutant（死亡变体）** | 已被某测试用例杀死 |
| **Stillborn mutant（夭折变体）** | 语法不合法 |
| **Trivial mutant（平凡变体）** | 几乎任何测试都能杀死 |
| **Equivalent mutant（等价变体）** | 没有测试能杀死（行为与原程序相同） |

### 3.3 杀死变体的定义

> 给定基本字符串程序 P 的变体 m∈M 和测试 t，当且仅当 t 在 P 上的输出与 t 在 m 上的输出**不同**时，称 t 杀死 m。

---

## 4. 示例：Min() 函数

### 4.1 原始程序

```java
int Min(int A, int B) {
    int minVal;
    minVal = A;
    if (B < A) {
        minVal = B;
    }
    return (minVal);
}
```

### 4.2 嵌入变体的程序

```java
int Min(int A, int B) {
    int minVal;
    minVal = A;
    Δ1  minVal = B;           // 变体1：额外赋值
    if (B < A)
    Δ2  if (B > A)            // 变体2：条件反转
    Δ3  if (B < minVal)       // 变体3：替换条件
    {
        minVal = B;
    Δ4      Bomb();           // 变体4：插入炸弹
    Δ5      minVal = A;       // 变体5：赋值替换
    Δ6      minVal = failOnZero(B); // 变体6：函数替换
    }
    return (minVal);
}
```

---

## 5. RIPR 模型与变异覆盖

### 5.1 变异覆盖 (MC)

> **变异覆盖 (MC)：** 对于每个 m∈M，TR 恰好包含一个需求 — 杀死 m。

### 5.2 RIPR 模型

| 条件 | 含义 |
|------|------|
| **Reachability（到达）** | 测试导致被变异的语句被执行 |
| **Infection（感染）** | 测试导致被变异语句产生不正确的状态 |
| **Propagation（传播）** | 不正确的状态传播到不正确的输出 |
| **Revealability（可观察性）** | 测试者必须观察到部分不正确输出 |

### 5.3 强杀死与弱杀死

#### 强杀死（Strongly Killing）

> 给定程序 P 的变体 m∈M 和测试 t，当且仅当 t 在 P 上的**输出**与 t 在 m 上的**输出不同**时，称 t **强杀死** m。
>
> → 满足 Reachability + Infection + Propagation + Revealability

#### 弱杀死（Weakly Killing）

> 给定修改程序 P 中位置 l 的变体 m∈M 和测试 t，当且仅当 P 在 t 上执行到 l **之后**的状态与 m 在 t 上执行到 l **之后**的状态**不同**时，称 t **弱杀死** m。
>
> → 满足 Reachability + Infection，**不需满足** Propagation

#### 弱变异覆盖 (WMC)

> **弱变异覆盖 (WMC)：** 对于每个 m∈M，TR 恰好包含一个需求 — 弱杀死 m。

- "弱变异"因此命名：在此假设下更容易杀死变体
- 弱变异需要的分析更少
- 少数变体可被弱杀死但无法被强杀死（无传播路径）
- 研究发现：弱杀死所有变体的测试集通常也能强杀死大部分变体

---

## 6. 示例分析

### 6.1 弱杀死示例 — 变体 Δ1

```java
int Min(int A, int B) {
    int minVal;
    minVal = A;
    Δ1  minVal = B;    // 变体：在此之后插入 minVal = B
    if (B < A) {
        minVal = B;
    }
    return (minVal);
}
```

**RIP 条件分析：**

| 条件 | 表达式 | 说明 |
|------|--------|------|
| Reachability | `true` | 始终到达 |
| Infection | `A ≠ B` | minVal 值不同 |
| Propagation | `(B < A) = false` | 走不同分支才能传播 |

**弱杀死但非强杀死的测试：** `A = 5, B = 3`

- `B < A` 成立 → 两个程序都进入 if 分支，minVal 都被设为 B
- 状态在 Δ1 之后不同（弱杀死 ✓），但最终输出相同（未强杀死 ✗）

### 6.2 等价变体示例 — 变体 Δ3

```java
int Min(int A, int B) {
    int minVal;
    minVal = A;
    if (B < A)
    Δ3  if (B < minVal)   // 变体：B < A → B < minVal
    {
        minVal = B;
    }
    return (minVal);
}
```

**等价性证明：**

- 前一条语句：`minVal = A`
- Infection 条件：`(B < A) ≠ (B < minVal)`
- 代入：`(B < A) ≠ (B < A)` → **矛盾**
- 因此该变体是**等价变体**

---

## 7. 强变异 vs 弱变异对比示例

```java
boolean isEven(int X) {
    if (X < 0)
        X = 0 - X;
    Δ4    X = 0;            // 变体4
    if ((double)(X/2) == ((double)X) / 2.0)
        return (true);
    else
        return (false);
}
```

- `X = -6` 将在弱变异下杀死变体4（到达后状态不同）
- 需要进一步分析是否能强杀死

---

## 8. 变异测试为什么有效

### 基本前提（Fundamental Premise of Mutation Testing）

> 如果软件包含一个故障，通常会存在一组变体，只有能检测到该故障的测试用例才能杀死这些变体。

- 这不是绝对的！变体引导测试者找到有效的测试集
- 一个有挑战性的问题：找到一个故障和一组变异充分的测试，使得这些测试**不能**发现该故障 → 这取决于变异运算符的设计

---

## 9. 变异运算符的设计

### 9.1 设计原则

- 方法级变异运算符在不同编程语言中相似
- 变异运算符做两件事之一：
  - 模拟典型的程序员错误（如错误的变量名）
  - 鼓励常见的测试启发式方法（如使表达式为 0）
- 研究者设计大量运算符，然后通过实验选择最有用的

### 9.2 有效变异运算符集

> 如果专门为杀死由运算符集 O = {o1, o2, ...} 创建的变体而设计的测试，也能以极高的概率杀死由所有剩余变异运算符创建的变体，则 O 定义了一个**有效的变异运算符集**。

---

## 10. Java 变异运算符

### 10.1 运算符一览

| 运算符 | 全称 | 说明 |
|--------|------|------|
| **ABS** | Absolute Value Insertion | 插入绝对值 |
| **AOR** | Arithmetic Operator Replacement | 算术运算符替换 |
| **ROR** | Relational Operator Replacement | 关系运算符替换 |
| **COR** | Conditional Operator Replacement | 条件运算符替换 |
| **SOR** | Shift Operator Replacement | 移位运算符替换 |
| **LOR** | Logical Operator Replacement | 逻辑运算符替换 |
| **ASR** | Assignment Operator Replacement | 赋值运算符替换 |
| **UOI** | Unary Operator Insertion | 一元运算符插入 |
| **UOD** | Unary Operator Deletion | 一元运算符删除 |
| **SVR** | Scalar Variable Replacement | 标量变量替换 |
| **BSR** | Bomb Statement Replacement | 炸弹语句替换 |

### 10.2 运算符分类与示例

#### 语句变异（Statement Mutations）

#### 运算符变异（Operator Mutations）

**AOR — 算术运算符替换：**
```java
// 原始
a = m * (o + p);
// 变体
Δ1  a = m + (o + p);
Δ2  a = m * (o * p);
Δ3  a = m leftOp (o + p);
```

**ROR — 关系运算符替换：**
```java
// 原始
if (X <= Y)
// 变体
Δ1  if (X > Y)
Δ2  if (X < Y)
Δ3  if (X falseOp Y)   // 始终返回 false
```

**COR — 条件运算符替换：**
```java
// 原始
if (X <= Y && a > 0)
// 变体
Δ1  if (X <= Y || a > 0)
Δ2  if (X <= Y leftOp a > 0)   // 返回左操作数结果
```

**SOR — 移位运算符替换：**
```java
// 原始
b = b >> 2;
// 变体
Δ1  b = b << 2;
Δ2  b = b leftOp 2;    // 结果为 b
```

**LOR — 逻辑运算符替换：**
```java
// 原始
int c = a & b;
// 变体
Δ1  int c = a | b;
Δ2  int c = a rightOp b;   // 结果为 b
```

**ASR — 赋值运算符替换：**
```java
// 原始
a = m * (o + p);
// 变体
Δ1  a += m * (o + p);
Δ2  a *= m * (o + p);
```

**UOI — 一元运算符插入：**
```java
// 原始
a = m * (o + p);
// 变体
Δ1  a = m * -(o + p);
Δ2  a = -(m * (o + p));
```

**UOD — 一元运算符删除：**
```java
// 原始
if (!(X <= Y && !Z))
// 变体
Δ1  if (X > Y && !Z)
Δ2  if (!(X < Y && Z))
```

#### 变量变异（Variable Mutations）

**SVR — 标量变量替换：**
```java
// 原始
a = m * (o + p);
// 变体
Δ1  a = o * (o + p);
Δ2  a = m * (m + p);
Δ3  a = m * (o + o);
Δ4  p = m * (o + p);
```

#### 常量变异（Constant Mutations）

**BSR — 炸弹语句替换：**
```java
// 原始
a = m * (o + p);
// 变体
Δ1  Bomb();   // 到达时抛出异常
```

---

## 11. 总结：变异包含其他标准

- 变异被广泛认为是**最强**的测试标准
  - 也是**最昂贵**的！测试需求最多（每个变体），通常测试用例也最多
- 变异通过包含特定的变异运算符来**包含**其他标准
- 包含关系只能对**弱变异**定义 — 其他标准只施加局部需求
  - ✅ 节点覆盖、边覆盖、子句覆盖
  - ✅ 一般主动子句覆盖（对单个测试的需求）
  - ❌ 关联主动子句覆盖（对测试对的需求）
  - ✅ 全定义数据流覆盖
