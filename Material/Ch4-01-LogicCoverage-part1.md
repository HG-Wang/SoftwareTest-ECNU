## Slide 1

- **Chapter 4 Logic Coverage**
- **8.1Logic Coverage**

## Slide 2

- **Ch. 4 : Logic Coverage**
- **2**
- **Four Structures for Modeling Software**

## Slide 3

- **Objectives**
- **1. Identify predicates and clauses in logical expressions**
- **2. Compare PC, CC, and CoC, and explain their limitations**
- **3. Explain how each clause independently affects the predicate in ACC (GACC, CACC, RACC)**
- **4. Analyze test requirements for logical expressions under different logic coverage criteria**
- **3**

## Slide 4

- **Motivation**
- **Consider:**
- **if ((a < b) || (f(z) && D && (m >= n*o))) { ... }**
- **Questions:**
- **• Would 2 test cases be enough to test the logic expression?**
- **• If we already achieve branch coverage, is that sufficient?**
- **4**

## Slide 5

- **From Graph Coverage to Logic Coverage**
- **Previously:**
  - Statement Coverage → execute each statement
  - Branch Coverage → take each decision outcome
- **However:**
  - These criteria focus on execution structure
  - Complex logical expressions are treated as a single Boolean result
  - Internal logic within expressions are NOT explicitly tested
- **Are we testing execution paths, or the logical semantics inside expressions?**
- **Solution: Logic Coverage**
  - A set of criteria for testing logical expressions
  - Focuses on how different parts of a logical expression affect the overall outcome
- **5**

## Slide 6

- **Semantic Logic Coverage Criteria  (8.1)**
- **Logic expressions define system behavior in many contexts:**
  - Decisions in programs
  - Guards in state-based systems (FSMs and statecharts)
  - Decisions in UML activity graphs
  - Constraints in requirements, both formal and informal
  - Conditions in SQL queries
- **Covering logic expressions is required by the US Federal Aviation Administration (FAA) for safety-critical software**
- **Key Insight:**
  - Testing selects a subset of all possible truth assignments.
  - Different truth assignments represent different system behaviors
- **We need systematic criteria to select effective tests**
- **6**

## Slide 7

- **Logic Predicates and Clauses**
- **A predicate（谓词） is a logical expression that evaluates to a Boolean value**
- **Predicates can contain**
  - Boolean variables
  - comparisons (>, <, ==, >=, <=, !=)
  - Boolean function calls
- **Internal structure is created by logical operators**
  - ¬ (not),  (and),  (or),  (implies),  (xor),   (equivalence)
- **A clause（子句） is a logical expression with no logical operators**
  - It represents a basic unit in a logical expression
- **In programming, we often call predicates “decisions”（判定） and clauses “conditions”（条件）.**
- **7**

## Slide 8

- **Example and Observations**
- **E.g.,	 (a < b) || (f (z) && D && (m >= n*o) ) has four clauses:**
  - (a < b) – relational expression
  - f (z) – boolean-valued function
  - D – boolean variable
  - (m >= n*o) – relational expression
- **Most predicates have few clauses (from a study of 63 open source programs, >400,000 predicates)**
  - 88.5% have 1 clause
  - 9.5% have 2 clauses
  - 1.35% have 3 clauses
  - Only 0.65% have 4 or more !
- **Exhaustive testing may be feasible for small predicates,  but becomes costly as clauses increase**
- **8**

## Slide 9

- **Predicate Coverage (PC)**
- **9**
- **Testcase for Predicate = true**
- **a = 5, b = 10, D = true, m = 1, n = 1, o = 1**
- **p = ((5 < 10)  true)  (1 >= 1*1)**
- **= (true  true)   true**
- **= true**
- **Testcase for Predicate = false**
- **a = 10, b = 5, D = false, m = 1, n = 1, o = 1**
- **p = ((10 < 5)  false)  (1 >= 1*1)**
- **= (false  false)  true**
- **= false**
- **Predicate Coverage (PC)**
- **The predicate p must evaluate to:**
- **True at least once**
- **False at least once**
- **E.g., p = ((a < b)  D)  (m >= n*o)**

## Slide 10

- **Limitations with PC**
- **PC does not ensure all clauses take both true and false**
- **PC does not fully exercise all the clauses, especially in the presence of short circuit evaluation**
- **10**
- **P = A  B**
- **A = true, B = true → p = true**
- **A = false, B = true → p = false**
- **Here B is always true → B never takes value false**
  - B is NOT evaluated (short-circuit)

## Slide 11

- **Clause Coverage (CC)**
- **11**
- **E.g., ((a < b)  D)  (m >= n*o)**
- **Two tests**
- **Clause Coverage (CC)**
- **Each clause must evaluate to:**
- **True at least once**
- **False at least once**

## Slide 12

- **Limitations with CC**
- **CC does not always ensure the predicate to be both true and false**
- **Both PC and CC are insufficient:**
  - PC focuses on the predicate outcome
  - CC focuses on individual clauses
- **How can we systematically test combinations of clause values?**
- **12**
- **p = A   B**
- **(A = true, B = false) → p = true**
- **(A = false, B = true) → p = true**
  - Here each clause takes both true and false, but the predicate never changes

## Slide 13

- **Combinatorial Coverage（CoC）**
- **13**
|  | a < b | D | m >= n*o | ((a < b)  D)  (m >= n*o) |
| --- | --- | --- | --- | --- |
| 1 | T | T | T | T |
| 2 | T | T | F | F |
| 3 | T | F | T | T |
| 4 | T | F | F | F |
| 5 | F | T | T | T |
| 6 | F | T | F | F |
| 7 | F | F | T | F |
| 8 | F | F | F | F |

- **Combinatorial Coverage (CoC)**
- **All possible combinations of clause values.**
- **Sometimes called Multiple Condition Coverage.**

## Slide 14

- **From Combinatorial Coverage to Efficient Testing**
- **Observation (from CoC):**
  - Testing all combinations is simple, neat, clean, and comprehensive
  - But quite expensive: 2N tests (N = number of clauses)
  - Impractical for predicates with more than a few clauses
- **Instead of testing all combinations,  test how each clause affects the predicate**
- **What exactly does “independently” mean?**
- **The textbook presents this idea as “making clauses active”**
- **14**
- **Test each clause independently from the other clauses**

## Slide 15

- **Active Clauses (8.1.2)**
- **Clause coverage has a weakness: Clause values do NOT always affect the predicate**
- **To really test the results of a clause, the clause should be the determining factor in the value of the predicate**
- **15**
- **This is considered to make the clause active**
- **Determination: A clause ci in predicate p, called the major clause, determines p if and only if the values of the remaining minor clauses cj are such that changing ci changes the value of p**

## Slide 16

- **16**
- **Determining Predicates**
- **Goal : Find tests for each clause when the clause determines the value of the predicate**
- **This is formalized in a family of criteria that have subtle, but very important, differences**
- **P = A  B**
- **if B = true, A does NOT determine p.**
  - A changes, p does NOT change
- **if B = false, A determines p.**
  - A = true  p = true
  - A = false  p = false

## Slide 17

- **17**
- **Active Clause Coverage**
- **This is a form of MCDC (Modified Condition/Decision Coverage), which is required by the FAA for safety critical software**
- **Ambiguity : Should the minor clauses remain the same value when ci = true and ci = false?**
- **Active Clause Coverage (ACC) :**
- **For each clause ci: ci = true once, ci = false once**
- **In each test, ci (major clause) must determine p**

## Slide 18

- **18**
- **Resolving the Ambiguity in ACC**
- **This question caused confusion among testers for years**
- **Considering this carefully leads to three separate criteria :**
  - GACC: Minor clauses do not need to be the same
  - RACC: Minor clauses do need to be the same
  - CACC: Minor clauses force the predicate to become both true and false
- **p = a  (b  c)**
- **Major clause : a**
- **a = true, b = false, c = true  p = true**
- **a = false, b = false, c = false  p = false**
- **Do these two tests satisfy ACC for clause a?**
- **Should the minor clauses (b, c) be the same when a = true and a = false?**

## Slide 19

- **19**
- **General Active Clause Coverage**
- **GACC does NOT guarantee predicate coverage**
- **We really want to cause predicates to be both true and false !**
- **General Active Clause Coverage (GACC)**
- **For each clause ci: ci = true once, ci = false once**
- **In each test, ci (major clause) must determine p, minor clauses do not need to be the same**
- **p = a  ⊕  b**
- **Major clause: a**
- **a = true, b = false  p = true**
- **a = false, b = true  p = true**
- **a determines p under the chosen minor clause values**
- **GACC satisfied**
- **But p is always True**

## Slide 20

- **20**
- **Restricted Active Clause Coverage**
- **RACC strictly controls minor clauses**
- **Clear cause-effect relationship. Ensures the predicate outcome changes**
- **May lead to infeasible test requirements; Hard to satisfy for some predicates**
- **Closely related to MCDC. Widely used in safety-critical software (e.g., aviation)**
- **Restricted Active Clause Coverage (RACC)**
- **For each clause ci: ci = true once, ci = false once**
- **In each test, ci (major clause) must determine p, minor clauses must remain the same**
- **p = a  ⊕  b**
- **Major clause: a**
- **a = true, b = false  p = true**
- **a = false, b = false  p = false**
- **Only a changes**
- **Effect is observable**

## Slide 21

- **21**
- **Correlated Active Clause Coverage**
- **CACC guarantees predicate coverage**
- **Ensuring observable effect on the Predicate**
- **Compared to RACC, CACC does not require minor clauses to remain the same**
- **Correlated Active Clause Coverage (CACC)**
- **For each clause ci: ci = true once, ci = false once**
- **In each test, ci (major clause) must determine p, the predicate must change: p (ci = true) ≠ p(ci = false)**
- **p = a  ⊕  b**
- **Major clause: a**
- **a = true, b = false  p = true**
- **a = false, b = false  p = false**
- **The effect of a must be observable in p**
- **Minor clauses may differ**

## Slide 22

- **CACC and RACC**
- **22**
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

- **CACC:• a must determine p• p must change• (b, c) can vary**
- **RACC:• a must determine p• p must change• (b, c) must remain the same**

## Slide 23

- **Comparison of ACC Variants**
- **23**
| Criterion | Minor Clauses Fixed? | Guarantees p Changes? | Strength |
| --- | --- | --- | --- |
| GACC | No | No | Weakest |
| CACC | Partially | Yes | Medium |
| RACC | Yes | Yes | Strongest |


## Slide 24

- **24**
- **Logic Criteria Subsumption**

## Slide 25

- **Logic Coverage in Safety-Critical Systems**
- **Critical systems rely  on logical expressions**
  - E.g., safety condition in control software (sensor status, system mode, emergency flag)
  - Each condition must independently affect the decision outcome
- **Industry requirement: MCDC is mandatory for safety-critical software:**
  - E.g., aviation (DO-178C, FAA), space systems, industrial control systems
- **Engineering trade-off:**
  - CoC: 2ⁿ tests (not scalable)
  - MCDC/RACC (≈ ACC): linear growth (practical)
    - MCDC/RACC often needs ~ n + 1 tests (in many cases) to 2n tests
    - ACC typically stays within ~ n to 2n tests
- **Logic Coverage is not optional, it is required for certification**
- **25**

## Slide 26

- **Summary**
- **What we learned – semantic logic coverage**
  - PC/CC/CoC: cover truth values and combinations
  - ACC (GACC/RACC/CACC): capture how each clause affects the predicate
- **Covering values is not enough, we must test whether each condition actually influences the outcome**
- **Practical Guidance:**
  - 1 clause → PC is sufficient
  - 2–3 clauses → CoC is feasible
  - Multiple clauses → ACC / MCDC
- **Logic coverage is not about more tests, but about testing meaningful behavior**
  - Testing is not just about values, but about whether each condition matters
- **26**

## Slide 27

- **Next: From Logic Coverage to Test Construction**
- **When does a clause NOT matter? (Inactive Clause Coverage: GICC, RICC)**
- **How to express coverage requirements using truth-table pairs (PC / CC / CoC / GACC / RACC / CACC / GICC / RICC)**
- **How to compute when a clause determines a predicate (From criteria to systematic test construction)**
- **27**
