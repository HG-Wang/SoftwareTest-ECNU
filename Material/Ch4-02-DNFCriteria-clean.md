# Ch4.2 基于DNF的语法逻辑覆盖标准

> **Syntactic Logic Coverage Criteria — DNF (Disjunctive Normal Form)**

---

## 1. DNF 基本概念

### 1.1 字 (Literal)

> **定义：** 字 (Literal) 是一个子句 (clause) 或其否定形式。
> 例如：`a` 和 `ā`（即 `¬a`）都是字。

### 1.2 项 (Term)

> **定义：** 项 (Term) 是由逻辑"与" (AND, ∧) 连接的一组字。
> 例如：`ab` 表示 `a ∧ b`，`ābc` 表示 `¬a ∧ b ∧ c`。

### 1.3 蕴含项 (Implicant)

> **定义：** 一个析取范式 (DNF) 的谓词是由逻辑"或" (OR, ∨) 连接的一组项组成的。项也被称为 **蕴含项 (Implicant)**。

**示例：**

```
f = abc + ab + ac
```

- 此处有三个蕴含项：`abc`、`ab`、`ac`
- 每个蕴含项由若干字通过 AND 连接
- 所有蕴含项通过 OR 连接构成完整的 DNF 表达式

---

## 2. IC — 蕴含项覆盖 (Implicant Coverage)

> **定义：** 蕴含项覆盖 (IC) 要求测试用例使得每个蕴含项 (implicant) 至少求值为 **真 (True)**。

**示例：** 对于 `f = ab + bc`：

- 需要同时考虑 `f` 及其否定 `f̄` 的 DNF 表示
- `f̄ = b + āc`
- 所有蕴含项集合：`{ab, bc, b, āc}`
- 测试用例需使每个蕴含项至少为真一次

| 蕴含项 | 使为真的测试用例示例 |
|--------|----------------------|
| `ab`   | `a=T, b=T`           |
| `bc`   | `b=T, c=T`           |
| `b`    | `b=T`                |
| `āc`   | `a=F, c=T`           |

---

## 3. 真子项、主蕴含项、冗余蕴含项与最小DNF

### 3.1 真子项 (Proper Subterm)

> **定义：** 真子项 (Proper Subterm) 是从一个项中移除一个或多个字后得到的项。

**示例：** 项 `abc` 共有 **6 个**真子项：

```
abc 的真子项：a, b, c, ab, ac, bc
```

| 移除的字数 | 真子项          |
|-----------|----------------|
| 移除 2 个  | `a`, `b`, `c`  |
| 移除 1 个  | `ab`, `ac`, `bc` |

### 3.2 主蕴含项 (Prime Implicant)

> **定义：** 主蕴含项 (Prime Implicant) 是指不存在任何一个真子项同时也是蕴含项的蕴含项。
> 即：不能通过移除任何字来"扩大"其覆盖范围，同时仍保持为蕴含项。

### 3.3 冗余蕴含项 (Redundant Implicant)

> **定义：** 冗余蕴含项 (Redundant Implicant) 是指可以从谓词中移除而不改变谓词值的蕴含项。

### 3.4 最小DNF (Minimal DNF)

> **定义：** 最小DNF (Minimal DNF) 仅包含主蕴含项 (prime implicant)，且不含冗余蕴含项 (redundant implicant)。

---

## 4. 唯真点 (UTP) 与 MUTP 覆盖

### 4.1 唯真点 (Unique True Point, UTP)

> **定义：** 唯真点 (UTP) 是一个测试点，在该点上给定的蕴含项 `i` 为 **真**，而所有其他蕴含项均为 **假**。

### 4.2 MUTP 覆盖

> **定义：** MUTP (Multiple Unique True Point) 覆盖要求：对每个蕴含项 `i`，选择 UTP，使得不在 `i` 中的子句 (clause) 分别取 **T** 和 **F** 值。

**示例：** `f = ab + bc`

| 蕴含项 | UTP（不在该蕴含项中的子句取不同值） |
|--------|-------------------------------------|
| `ab`   | `TTT`（c=T）                        |
| `bc`   | `FTF`（a=F）                        |

- 对于 `ab`：`a=T, b=T, c=T` → `ab=T, bc=T`... 需注意 UTP 要求其他蕴含项为假
- 对于 `bc`：`a=F, b=T, c=F` → `bc=T`，而 `ab=F`

---

## 5. 近假点 (NFP) 与 CUTPNFP 覆盖

### 5.1 近假点 (Near False Point, NFP)

> **定义：** 近假点 (NFP) 是一个测试点，在该点上 `f` 为 **假**，但如果将某个子句 `c` 取反，则蕴含项 `i`（从而 `f`）变为 **真**。
>
> 在 NFP 处，子句 `c` 决定了 `f` 的值 → 与 ACC (Active Clause Coverage) 的关系。

### 5.2 CUTPNFP 覆盖

> **定义：** CUTPNFP (Clause Coverage in UTP and NFP Pair) 覆盖要求：对每个蕴含项 `i` 中的每个子句 `c`，将 `i` 的一个 UTP 与 `c` 的一个 NFP 配对，两者仅在 `c` 的值上不同。

**示例：** `f = ab + cd`

CUTPNFP 测试集 = `{TTFF, FFTT, TFFF, FTFF, FFTF, FFFT}`

| 测试点 | a | b | c | d | f  | 说明                  |
|--------|---|---|---|---|----|-----------------------|
| TTFF   | T | T | F | F | T  | UTP for `ab`          |
| FFTT   | F | F | T | T | T  | UTP for `cd`          |
| TFFF   | T | F | F | F | F  | NFP for `ab`, c 相关  |
| FTFF   | F | T | F | F | F  | NFP for `ab`, d 相关  |
| FFTF   | F | F | T | F | F  | NFP for `cd`, a 相关  |
| FFFT   | F | F | F | T | F  | NFP for `cd`, b 相关  |

---

## 6. MNFP 与 MUMCUT 覆盖

### 6.1 MNFP 覆盖

> **定义：** MNFP (Multiple Near False Point) 覆盖要求：对每个蕴含项 `i` 中的每个字 `c`，选择 NFP，使得不在 `i` 中的子句分别取 **T** 和 **F** 值。

### 6.2 MUMCUT 覆盖

> **定义：** MUMCUT 覆盖是 **MUTP + CUTPNFP + MNFP** 三种覆盖标准的组合。

```
MUMCUT = MUTP ∪ CUTPNFP ∪ MNFP
```

---

## 7. DNF 故障类 (DNF Fault Classes)

| 缩写   | 全称                          | 中文名称           | 说明                         |
|--------|-------------------------------|--------------------|------------------------------|
| **ENF** | Expression Negation Fault     | 表达式取反故障     | 整个表达式被取反             |
| **TNF** | Term Negation Fault           | 项取反故障         | 某个项被取反                 |
| **TOF** | Term Omission Fault           | 项遗漏故障         | 某个项被遗漏                 |
| **LNF** | Literal Negation Fault        | 字取反故障         | 某个字被取反（如 `a` 变 `ā`）|
| **LRF** | Literal Reference Fault       | 字引用故障         | 某个字被替换为另一个字       |
| **LOF** | Literal Omission Fault        | 字遗漏故障         | 某个字从项中被遗漏           |
| **LIF** | Literal Insertion Fault       | 字插入故障         | 某个字被插入到项中           |
| **ORF+** | Operator Reference Fault (+) | 运算符引用故障(+） | OR 运算符被替换（逻辑错误）  |
| **ORF*** | Operator Reference Fault (*) | 运算符引用故障(*)  | AND 运算符被替换（逻辑错误） |

---

## 8. 故障检测关系

### 8.1 MUTP 检测 LIF

> **定理：** MUTP 覆盖标准能够检测所有 **字插入故障 (LIF)**。

### 8.2 CUTPNFP 检测 LOF

> **定理：** CUTPNFP 覆盖标准能够检测所有 **字遗漏故障 (LOF)**。

### 8.3 故障检测能力对比

| 覆盖标准   | 可检测的故障类                               | 特点                     |
|------------|---------------------------------------------|--------------------------|
| RACC       | TNF, ENF（约占 1/3 的故障）                 | 成本较低                 |
| MUTP       | LIF + RACC 检测的故障                       | 检测字插入故障           |
| CUTPNFP    | LOF + RACC 检测的故障                       | 检测字遗漏故障           |
| **MUMCUT** | MUTP + CUTPNFP + MNFP 可检测的所有故障      | 最全面，但成本更高       |

### 8.4 选择建议

> **MUMCUT** 比 RACC 更昂贵但能检测更多故障。当 **失败后果严重** 时，应使用 MUMCUT。

---

## 9. 卡诺图 (Karnaugh Map) 辅助测试

卡诺图 (K-Map) 可用于辅助确定以下内容：

- 子句 (Clauses)
- 否定形式 (Negation)
- 主蕴含项与冗余蕴含项 (Prime/Redundant Implicants)
- UTP
- UTP/NFP 配对

### 9.1 用卡诺图确定子句

**示例：** `f = b + ac + āc̄`

通过卡诺图分析可以确定 `f` 依赖哪些子句，以及各子句对结果的影响。

### 9.2 用卡诺图确定否定

**示例：** `f = ab + bc`

利用卡诺图可以直观得到 `f̄` 的 DNF 表示。

### 9.3 用卡诺图确定主蕴含项

**示例：** `f = abc + abd + abcd̄ + āb̄cd + acd`

通过卡诺图中的相邻最小项合并，可以识别哪些项是主蕴含项，哪些是冗余的。

### 9.4 用卡诺图确定 UTP 和 CUTPNFP

**示例：** `f = ab + cd`

| 步骤 | 说明                                                         |
|------|--------------------------------------------------------------|
| 1    | 在卡诺图中标出各蕴含项的覆盖区域                             |
| 2    | 为每个蕴含项找到只被其覆盖（不被其他蕴含项覆盖）的单元格 → UTP |
| 3    | 找到 UTP 与 NFP 仅在一个子句上不同的配对 → CUTPNFP           |

---

## 10. 总结

| 层次       | 概念                                                        |
|------------|-------------------------------------------------------------|
| 基础概念    | 字 (Literal) → 项 (Term) → 蕴含项 (Implicant) → DNF        |
| 项的性质    | 真子项、主蕴含项、冗余蕴含项、最小DNF                        |
| 测试点      | UTP（唯真点）、NFP（近假点）                                |
| 覆盖标准    | IC → MUTP → CUTPNFP → MNFP → MUMCUT（逐步增强）            |
| 故障类      | ENF, TNF, TOF, LNF, LRF, LOF, LIF, ORF+, ORF*              |
| 关键定理    | MUTP 检测所有 LIF；CUTPNFP 检测所有 LOF                     |
| 工具        | 卡诺图 (K-Map) 辅助分析                                     |
| 实践建议    | 后果严重时使用 MUMCUT；一般情况 RACC 即可                   |
