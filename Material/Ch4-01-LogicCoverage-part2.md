## Slide 1

- **Chapter 4 Logic Coverage**
- **8.1Logic Coverage**

## Slide 2

- **Objectives**
- **1. Identify inactive clauses (when a clause cannot determine the predicate)2. Formulate test requirements for GICC / RICC using truth-table pairs3. Compute conditions under which a clause determines the predicate4. Systematically derive test cases from logic coverage criteria**
- **2**

## Slide 3

- **Inactive Clause Coverage (8.1.3)**
- **The active clause coverage criteria ensure that “major” clauses do affect the predicates**
- **Inactive clause coverage takes the opposite approach – major clauses do not affect the predicates**
- **3**
- **Inactive Clause Coverage (ICC) : For each p in P and each major clause ci in Cp, choose minor clauses cj, j != i, so that ci does not determine p.  TR has four requirements for each ci : (1) ci evaluates to true with p true, (2) ci evaluates to false with p true, (3) ci evaluates to true with p false, and (4) ci evaluates to false with p false.**

## Slide 4

- **4**
- **General and Restricted ICC**
- **Unlike ACC, the notion of correlation is not relevant**
  - ci does not determine p, so cannot correlate with p
- **Predicate coverage is always guaranteed**
- **General Inactive Clause Coverage (GICC) : For each p in P and each major clause ci in Cp, choose minor clauses cj , j != i, so that ci does not determine p.  The values chosen for the minor clauses cj do not need to be the same when ci is true as when ci is false, that is, cj(ci = true) = cj(ci = false) for all cj OR cj(ci = true) != cj(ci = false) for all cj.**
- **Restricted Inactive Clause Coverage (RICC) : For each p in P and each major clause ci in Cp, choose minor clauses cj, j != i, so that ci does not determine p.  The values chosen for the minor clauses cj must be the same when ci is true as when ci is false, that is, it is required that cj(ci = true) = cj(ci = false) for all cj.**

## Slide 5

- **5**
- **Infeasibility & Subsumption (8.1.4)**
- **Consider the predicate:**
- **(a > b  b > c)  c > a**
- **(a > b) = true, (b > c) = true, (c > a) = true is infeasible**
- **As with graph-based criteria, infeasible test requirements have to be recognized and ignored**
- **Recognizing infeasible test requirements is hard, and in general, undecidable**
- **Software testing is inexact – engineering, not science**

## Slide 6

- **6**
- **Logic Criteria Subsumption**

## Slide 7

- **GACC不能包含PC的例子**
- **对于有异或运算的谓词表达式，如p = a ⊕ b，GACC能包含谓词覆盖 PC吗？请给出理由。**
- **对子句a，GACC测试需求为{1, 2}×{3, 4}，即(1, 3), (1, 4) , (2, 3), (2, 4)。CACC测试需求为(1, 3), (2, 4)。**
- **对子句b，GACC测试需求为{1, 3}×{2, 4}，即(1, 2), (1, 4) , (3, 2), (3, 4)。CACC测试需求为(1, 2), (3, 4)。**
- **若选择行对（1，4）或（2，3）即可满足GACC，但无法满足PC（因此也无法满足CACC）。**
| No. | a | b | p = a ⊕ b | pa | pb |
| --- | --- | --- | --- | --- | --- |
| 1 | T | T | F | T | T |
| 2 | T | F | T | T | T |
| 3 | F | T | T | T | T |
| 4 | F | F | F | T | T |


## Slide 8

- **Making Clauses Determine a Predicate (8.1.5)**
- **Finding values for minor clauses cj is easy for simple predicates**
- **But how to find values for more complicated predicates ?**
- **Definitional approach:**
  - pc=true is predicate p with every occurrence of c replaced by true
  - pc=false is predicate p with every occurrence of c replaced by false
- **To find values for the minor clauses, connect pc=true and pc=false with exclusive OR**
- **pc  =  pc=true  pc=false**
- **After solving,  pc describes exactly the values needed for c to determine p**
- **8**

## Slide 9

- **9**
- **Examples**
- **p = a  b**
- **pa = pa=true   pa=false**
- **= (true  b) XOR (false  b)**
- **= true XOR b**
- **= ¬ b**
- **p = a  b**
- **pa = pa=true   pa=false**
- **= (true  b)  (false  b)**
- **= b   false**
- **= b**
- **p = a  (b  c)**
- **pa = pa=true   pa=false**
- **= (true  (b  c))  (false  (b  c))**
- **= true  (b  c)**
- **= ¬ (b  c)**
- **= ¬  b  ¬ c**
- **“NOT b  NOT c” means either b or c can be false**
- **RACC requires the same choice for both values of a,  CACC does not**

## Slide 10

- **XOR Identity Rules**
- **10**
- **Exclusive-OR (xor, ) means both cannot be true**
- **That is, A xor B means**
- **“A or B is true, but not both”**
- **p = A  A  b**
- **= A  ¬ b**
- **p = A  A  b**
- **= ¬ A  b**
- **p = A xor (A and b)**
- **= A and !b**
- **p = A xor (A or b)**
- **= !A and b**
- **with fewer symbols …**

## Slide 11

- **11**
- **Repeated Variables**
- **The definitions in this chapter yield the same tests no matter how the predicate is expressed**
- **(a  b)  (c  b) == (a  c)  b**
- **(a  b)  (b  c)  (a  c)**
  - Only has 8 possible tests, not 64
- **Use the simplest form of the predicate, and ignore contradictory truth table assignments**

## Slide 12

- **12**
- **A More Subtle Example**
- **p = ( a  b )  ( a  ¬ b)**
- **pa = pa=true   pa=false**
- **= ((true  b)  (true  ¬ b))  ((false  b)  (false  ¬ b))**
- **= (b  ¬ b)  false**
- **= true  false**
- **= true**
- **a always determines the value of this predicate**
- **b never determines the value – b is irrelevant !**
- **p = ( a  b )  ( a  ¬ b)**
- **pb = pb=true   pb=false**
- **= ((a  true)  (a  ¬ true))  ((a  false)  (a  ¬ false))**
- **= (a  false)  (false  a)**
- **= a  a**
- **= false**

## Slide 13

- **b & c are the same, a differs, and p differs … thus TTT and FTT cause a to determine the value of p**
- **Again, b & c are the same, so TTF and FTF cause a to determine the value of p**
- **Tabular Method for Determination**
- **The math sometimes gets complicated**
- **A truth table can sometimes be simpler**
- **Example**
- **13**
|  | a | b | c | a  (b  c) |
| --- | --- | --- | --- | --- |
| 1 | T | T | T | T |
| 2 | T | T | F | T |
| 3 | T | F | T | T |
| 4 | T | F | F | F |
| 5 | F | T | T | F |
| 6 | F | T | F | F |
| 7 | F | F | T | F |
| 8 | F | F | F | F |

| pa | pb | pc |
| --- | --- | --- |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |
|  |  |  |

- **In sum, three separate pairs of rows can cause a to determine the value of p, and only one pair each for b and c**
- **Finally, this third pair, TFT and FFT, also cause a to determine the value of p**
- **For clause b, only one pair, TTF and TFF cause b to determine the value of p**
- **Likewise, for clause c, only one pair, TFT and TFF, cause c to determine the value of p**

## Slide 14

- **Test Requirements Analysis**
- **For p = a  (b  c)**
  - pa= b  c
  - pb= a ¬c
  - pc= a ¬b
- **14**
|  | a | b | c | a  (b  c) |
| --- | --- | --- | --- | --- |
| 1 | T | T | T | T |
| 2 | T | T | F | T |
| 3 | T | F | T | T |
| 4 | T | F | F | F |
| 5 | F | T | T | F |
| 6 | F | T | F | F |
| 7 | F | F | T | F |
| 8 | F | F | F | F |

| pa | pb | pc |
| --- | --- | --- |
| T |  |  |
| T | T |  |
| T |  | T |
|  | T | T |
| T |  |  |
| T |  |  |
| T |  |  |
|  |  |  |

| 子句 | GACC | CACC | RACC | GICC | RICC |
| --- | --- | --- | --- | --- | --- |
| a | {1, 2, 3}× {5, 6, 7} | {1, 2, 3}× {5, 6, 7} | (1, 5), (2, 6), (3, 7) | p=F: (4, 8) | p=F: (4, 8) |
| b | (2, 4) | (2, 4) | (2, 4) | p=F: {5, 6} ×{7, 8}, p=T:  (1, 3) | p=F: (5, 7) (6, 8}, p=T:  (1, 3) |
| c | (3, 4) | (3, 4) | (3, 4) | p=F: {5, 7} ×{6, 8}, p=T:  (1, 2) | p=F: (5, 6) (7, 8}, p=T:  (1, 2) |


## Slide 15

- **General Description of TR for ACC**
- **We assume p is the predicate, ci is the major clause, cj , j ≠ i are the minor clauses, and pci is the conditions under which ci determines p**
- **For each i, GACC has two test requirements:**
  - ci = T ∧ pci = T and ci = F ∧ pci = T.
  - Note that the values of the minor clauses cj may differ between the two tests.
- **For each i, CACC has two test requirements:**
  - ci = T ∧ pci = T and ci = F ∧ pci = T. Additionally, the value of p resulting from the first test must differ from the value of p resulting from the second.
  - Note that the values of the minor clauses cj may differ between the two tests.
- **For each i, RACC has two test requirements:**
  - ci = T ∧ pci = T and ci = F ∧ pci = T. Additionally, ci is the only difference between the two tests. That is, the values of the minor clauses cj must be identical on the two tests.
- **15**

## Slide 16

- **General Description of TR for ICC**
- **For each i, GICC has two pairs of test requirements:**
  - Pair 1: ci = T ∧ pci = F ∧ p = T. ci = F ∧ pci = F ∧ p = T.
  - Pair 2: ci = T ∧ pci = F ∧ p = F. ci = F ∧ pci = F ∧ p = F.
  - The minor clauses cj may differ between the two tests. Often, one of the pairs is infeasible.
- **For each i, RICC has two pairs of test requirements:**
  - Pair 1: ci = T ∧ pci = F ∧ p = T. ci = F ∧ pci = F ∧ p = T.
  - Pair 2: ci = T ∧ pci = F ∧ p = F. ci = F ∧ pci = F ∧ p = F.
  - Additionally, ci is the only difference between the two tests in Pair 1 and the two tests in Pair 2.
  - That is, the values of the minor clauses cj must be identical for the two tests in Pair 1 and identical for the two tests in Pair 2. Again, one of the pairs is often infeasible.
- **16**
- **ICC系列标准包含PC：对于所有的子句均需要考察p=T和p=F场景对应的测试需求，综合所有的测试需求必定满足PC**

## Slide 17

- **两组概念**
- **判定覆盖/分支覆盖Decision/Branch Coverage (DC)**
  - 判定的true和false至少各执行一次.
  - Eg. ((x>5) && (y>0)): true and false
- **条件覆盖Condition Coverage (CC)**
  - 每个条件的true和false至少各被执行一次
  - (x>5) ：true and false
  - (y>0)：true and false
- **谓词覆盖Predicate Coverage (PC)**
  - 每个谓词P的true 和false 各被执行一次
- **子句覆盖Clause Coverage (CC)**
  - 每个子句C的true和false各被执行一次
- **17**
- **条件与判定**
- **Condition and Decision**
- **子句与谓词**
- **Clause and Predicate**

## Slide 18

- **修正条件判定覆盖MCDC**
- **条件判定覆盖Decision Condition Coverage(C/DC)**
  - 同时满足DC和CC，即C/DC(P)=CC(P) ∩ DC(P)
  - C/DC 包含 CC
  - C/DC 包含 DC
- **修正条件判定覆盖Modified Condition/Decision Coverage (MC/DC)**
  - 每个条件独立影响判定true和false各一次
  - 理论上测试用例数目一般为（N+1）
- **18**

## Slide 19

- **有效子句覆盖Active Clause Coverage**
- **General Active Clause Coverage (GACC)**
  - 满足子句覆盖，可能不满足谓词覆盖！
- **Restricted Active Clause Coverage (RACC)**
  - 满足谓词覆盖和子句覆盖，
  - 是ACC和MCDC中最常被采用的定义
  - 可能导致更多测试用例！
- **Correlated Active Clause Coverage (CACC)**
  - 满足谓词覆盖和子句覆盖
  - 测试用例数目介于GACC和RACC之间
- **19**

## Slide 20

- **The Number of Tests**
- **MCDC and the RACC criteria need at least n + 1 tests, but  always fewer than 2n tests.**
- **Kaminski also showed that n + 1 is enough when n < 4, because of the overlap among tests, but the number of tests  needed for some functions gets closer to 2n as n grows.**
- **20**

## Slide 21

- **Logic Coverage Summary**
- **Predicates are often very simple—in practice, most have less than 3 clauses**
  - In fact, most predicates only have one clause !
  - With only clause, PC is enough
  - With 2 or 3 clauses, CoC is practical
  - Advantages of ACC and ICC criteria significant for large predicates
    - CoC is impractical for predicates with many clauses
- **Control software often has many complicated predicates, with lots of clauses**
- **Question … why don’t complexity metrics count the number of clauses in predicates?**
  - Traditional complexity metrics count decisions, not the number of clauses inside them.
  - From a control-flow perspective, a complex expression is still just one branch.
  - But from a testing perspective, it may contain multiple interacting conditions.
  - That gap is exactly what logic coverage addresses.
- **21**
