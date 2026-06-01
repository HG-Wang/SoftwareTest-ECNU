## Slide 1

- **Chapter 4 Logic Coverage**
- **Logic Coverage for Specifications**
- **(8.4 Logic Coverage for Specifications)**

## Slide 2

- **本节课程目标**
- **能将非形式化（自然语言）表示的规约转写成对应的逻辑表达式；**
- **对于合取范式（CNF）/析取范式（DNF）形式的逻辑表达式，能直接写出满足有效子句覆盖ACC的测试需求。**
- **2**

## Slide 3

- **3**
- **Specifications in Software**
- **Specifications can be formal or informal**
  - Formal specs are usually expressed mathematically
  - Informal specs are usually expressed in natural language
- **Lots of formal languages and informal styles are available**
- **Most specification languages include explicit logical expressions, so it is very easy to apply logic coverage criteria**
- **Implicit logical expressions in natural-language specifications should be re-written as explicit logical expressions as part of test design**
  - You will often find mistakes
- **One of the most common is preconditions …**

## Slide 4

- **Preconditions**
- **Programmers often include preconditions for their methods**
- **The preconditions are often expressed in comments in method headers**
- **Preconditions can be in javadoc, “requires”,  “pre”, …**
- **4**
- **Example – Saving addresses**
- **// name must not be empty**
- **// state must be valid**
- **// zip must be 5 numeric digits**
- **// street must not be empty**
- **// city must not be empty**
- **Rewriting to logical expression**
- **name != “”  state in stateList  zip >= 00000  zip <= 99999  street != “”  city != “”**
- **Conjunctive Normal Form**

## Slide 5

- **Shortcut for Predicates in Conjunctive Normal Form**
- **A predicate is in conjunctive normal form (CNF) if it consists of clauses or disjuncts connected by the and operator**
  - A  B  C  …
  - (A  B)  (C  D)
- **A major clause is made active by making all other clauses true**
- **5**
|  | A | B | C | … |
| --- | --- | --- | --- | --- |
| 1 | T | T | T |  |
| 2 | F | T | T | … |
| 3 | T | F | T |  |
| 4 | T | T | F |  |
|  |  | . |  | . |
|  |  | . |  | . |
|  |  | . |  | . |

- **ACC tests are “all true” and then a “diagonal” of false values:**

## Slide 6

- **Shortcut for Predicates in Disjunctive Normal Form**
- **A predicate is in disjunctive normal form (DNF) if it consists of clauses or conjuncts connected by the or operator**
  - A  B  C  …
  - (A  B)  (C  D)
- **A major clause is made active by making all other clauses false**
- **6**
|  | A | B | C | … |
| --- | --- | --- | --- | --- |
| 1 | F | F | F |  |
| 2 | T | F | F | … |
| 3 | F | T | F |  |
| 4 | F | F | T |  |
|  |  | . |  | . |
|  |  | . |  | . |
|  |  | . |  | . |

- **ACC tests are “all false” and then a “diagonal” of true values:**

## Slide 7

- **Summary : Logic Coverage for Specs**
- **Logical specifications can come from lots of places :**
  - Preconditions
  - Java asserts
  - Contracts (in design-by-contract development)
  - OCL conditions
  - Formal languages
- **Logic specifications can describe behavior at many levels :**
  - Methods and classes (unit and module testing)
  - Connections among classes and components
  - System-level behavior
- **Many predicates in specifications are in disjunctive normal or conjunctive normal form—simplifying the computations**
- **7**
