<!-- Slide 1 -->

Chapter 2 Input Space Partition


---

<!-- Slide 2 -->

本节课程目标
### 明确输入空间划分技术的好处及划分时需要满足的特性；
### 【难点】明确输入域建模的步骤，能使用基于接口和基于功能两种方法进行输入域建模；理解输入域建模在识别潜在风险触发条件中的作用；
### 【重点】掌握常见的特征块组合标准及它们之间的包含关系，包括ACoC、ECC、PWC、TWC、BCC、MBCC等，能计算满足组合标准的测试的数目，能根据给定的组合标准构造对应的测试用例。理解不同组合标准在测试资源受限情况下的适用场景及成本差异。
### 【重点】解释等价类划分与边界值分析技术，明确边界值分析技术的使用场景
### 【重点】应用等价类划分技术和2-value和3-value方法进行边界值分析
### 基于具体的接口说明文档，应用输入空间划分技术，包括确定特征、定义测试需求、精化测试需求。
### 掌握典型组合测试工具的用法，使用组合测试工具PICT生成满足pairwise组合标准的测试用例。
2

---

<!-- Slide 3 -->

Ch. 2 : Input Space Coverage
3
## Four Structures for Modeling Software



---

<!-- Slide 4 -->

Input Domains
The input domain for a program contains all the possible inputs to that program
For even small programs, the input domain is so large that it might as well be infinite
Testing is fundamentally about choosing finite sets of values from the input domain
Input parameters define the scope of the input domain
Parameters to a method
Data read from a file
Global variables
User level inputs
Domains for input parameters are partitioned into regions
At least one value is chosen from each region
4

---

<!-- Slide 5 -->

5
Benefits of ISP
Can be equally applied at several levels of testing
Unit
Integration
System
Relatively easy to apply with no automation
Easy to adjust the procedure to get more or fewer tests
No implementation knowledge is needed
Just the input space

---

<!-- Slide 6 -->

6
Partitioning Domains
Domain D
Partition scheme q of D
## The partition q defines a set of blocks, Bq = b1 , b2 , …, bQ
The partition must satisfy two properties :
Blocks must be pairwise disjoint (no overlap)
Together the blocks cover the domain D (complete)
### bi  bj = ,  i  j, bi, bj  Bq
##    b = D
### b  Bq

---

<!-- Slide 7 -->

In-Class Exercise
7
## Design a partitioning for all integers
## That is, partition integers into blocks such that each block seems to be equivalent in terms of testing
## Make sure your partition is valid:
## Pairwise disjoint
## Complete

---

<!-- Slide 8 -->

8
Using Partitions – Assumptions
Choose a value from each block
Each value is assumed to be equally useful for testing
Application to testing
Find characteristics in the inputs : parameters, semantic descriptions, …
Partition each characteristic
Choose tests by combining values from characteristics
Example Characteristics
Input X is null
Order of the input file F (sorted, inverse sorted, arbitrary, …)
Min separation of two aircraft
Input device (DVD, CD, VCR, computer, …)

---

<!-- Slide 9 -->

9
Choosing Partitions
Choosing (or defining) partitions seems easy, but is easy to get wrong
Consider the characteristic “order of file F”
### b1 = sorted in ascending order
### b2 = sorted in descending order
### b3 = arbitrary order
### but … something’s fishy …
### What if the file is of length 1?
### The file will be in all three blocks …
### That is, disjointness is not satisfied
### Solution:
### Each characteristic should address just one property
### C1: File F sorted ascending
### - c1.b1 = true
- c1.b2 = false
### C2: File F sorted descending
### - c2.b1 = true
- c2.b2 = false
## Design blocks for that characteristic
## Can you find the problem?
## Can you think of a solution?

---

<!-- Slide 10 -->

10
Properties of Partitions
If the partitions are not complete or disjoint, that means the partitions have not been considered carefully enough
They should be reviewed carefully, like any design
Different alternatives should be considered

---

<!-- Slide 11 -->

11
Modeling the Input Domain
We model the input domain in five steps …
Step 1 : Identify testable functions
Step 2 : Find all the parameters
Step 3 : Model the input domain
Step 4 : Apply a test criterion to choose combinations of values
Step 5 : Refine combinations of blocks into test inputs
### implementation abstraction level
### design abstraction level
Step 1&2
Step 3&4
Step 5

---

<!-- Slide 12 -->

12
Modeling the Input Domain
Step 1 : Identify testable functions
Individual methods have one testable function
Methods in a class often have the same characteristics
Programs have more complicated characteristics—modeling documents such as UML can be used to design characteristics
Systems of integrated hardware and software components can use devices, operating systems, hardware platforms, browsers, etc.
## Step 2 : Find all the parameters
### Often fairly straightforward, even mechanical
### Important to be complete
### Methods : Parameters and state (non-local) variables used
### Components : Parameters to methods and state variables
### System : All inputs, including files and databases

---

<!-- Slide 13 -->

13
Modeling the Input Domain (cont)
Step 3 : Model the input domain
The domain is scoped by the parameters
The structure is defined in terms of characteristics
Each characteristic is partitioned into sets of blocks
Each block represents  a set of values
This is the most creative design step in using ISP
## Step 4 : Apply a test criterion to choose combinations of values
### A test input has a value for each parameter
### One block for each characteristic
### Choosing all combinations is usually infeasible
### Coverage criteria allow subsets to be chosen
## Step 5 : Refine combinations of blocks into test inputs
### Choose appropriate values from each block

---

<!-- Slide 14 -->

14
## Steps 1 & 2—Identifying Functionalities, Parameters and  Characteristics
A creative engineering step
More characteristics means more tests
Interface-based : Translate parameters to characteristics
Candidates for characteristics :
Preconditions and postconditions
Relationships among variables
Relationship of variables with special values (zero, null, blank, …)
Should not use program source—characteristics should be based on the  input domain
Program source should be used with graph or logic criteria
Better to have more characteristics with few blocks
Fewer mistakes and fewer tests

---

<!-- Slide 15 -->

15
## Step 3 : Modeling the Input Domain
Partitioning characteristics into blocks and values is a very creative engineering step
More blocks means more tests
Partitioning often flows directly from the definition of characteristics and both steps are done together
Should evaluate them separately – sometimes fewer characteristics can be used with more blocks and vice versa
Strategies for identifying values :
Include valid, invalid and special values
Sub-partition some blocks
Explore boundaries of domains
Include values that represent “normal use”
Try to balance the number of blocks in each characteristic
Check for completeness and disjointness

---

<!-- Slide 16 -->

16
Two Approaches to Input Domain Modeling
Interface-based approach
Develops characteristics directly from individual input parameters
Simplest application
Can be partially automated in some situations

Functionality-based approach
Develops characteristics from a behavioral view of the program under test
Harder to develop—requires more design effort
May result in better tests, or fewer tests that are as effective
### Input Domain Model (IDM)

---

<!-- Slide 17 -->

17
1. Interface-Based Approach
### Mechanically consider each parameter in isolation
### This is an easy modeling technique and relies mostly on syntax
### Some domain and semantic information won’t be used
### Could lead to an incomplete IDM
### Ignores relationships among parameters
### Consider method triang() from class TriangleType

public enum Triangle { Scalene, Isosceles, Equilateral, Invalid }
public static Triangle triang (int Side, int Side2, int Side3)
// Side1, Side2, and Side3 represent the lengths of the sides of a triangle
// Returns the appropriate enum value
The IDM for each parameter is identical
Reasonable characteristic : Relation of side with zero

---

<!-- Slide 18 -->

Interface-Based –triang()
triang() has one testable function and three integer inputs
18
| Characteristic | b1 | b2 | b3 |
| --- | --- | --- | --- |
| q1 = “Relation of Side 1 to 0” | greater than 0 | equal to 0 | less than 0 |
| q2 = “Relation of Side 2 to 0” | greater than 0 | equal to 0 | less than 0 |
| q3 = “Relation of Side 3 to 0” | greater than 0 | equal to 0 | less than 0 |
### First Characterization of TriTyp’s Inputs
A maximum of 3*3*3 = 27 tests
Some triangles are valid, some are invalid
Refining the characterization can lead to more tests …

---

<!-- Slide 19 -->

19
Interface-Based IDM—triang()
### Second Characterization of triang()’s Inputs
| Characteristic | b1 | b2 | b3 | b4 |
| --- | --- | --- | --- | --- |
| q1 = “Refinement of q1” | greater than 1 | equal to 1 | equal to 0 | less than 0 |
| q2 = “Refinement of q2” | greater than 1 | equal to 1 | equal to 0 | less than 0 |
| q3 = “Refinement of q3” | greater than 1 | equal to 1 | equal to 0 | less than 0 |
A maximum of 4*4*4 = 64 tests
Complete because the inputs are integers (0 . . 1)
### Possible values for partition q1
| Characteristic | b1 | b2 | b3 | b4 |
| --- | --- | --- | --- | --- |
| Side1 | 5 | 1 | 0 | -5 |

2
-1

#### Test boundary conditions



---

<!-- Slide 20 -->

20
2. Functionality-Based Approach
Identify characteristics that correspond to the intended functionality
Requires more design effort from tester
Can incorporate domain and semantic knowledge
Can use relationships among parameters
Modeling can be based on requirements, not implementation
The same parameter may appear in multiple characteristics, so it’s harder to translate values to test cases

---

<!-- Slide 21 -->

2. Functionality-Based Example
Again, consider method triang() from class TriangleType :
21
### The three parameters represent a triangle
### The IDM can combine all parameters
### Reasonable characteristic : Type of triangle

---

<!-- Slide 22 -->

22
Functionality-Based IDM—triang()
### First two characterizations are based on syntax–parameters and their type
### A semantic level characterization could use the fact that the three integers represent a triangle
### Geometric Characterization of triang()’s Inputs
| Characteristic | b1 | b2 | b3 | b4 |
| --- | --- | --- | --- | --- |
| q1 = “Geometric  Classification” | scalene | isosceles | equilateral | invalid |
| Characteristic | b1 | b2 | b3 | b4 |
| --- | --- | --- | --- | --- |
| q1 = “Geometric  Classification” | scalene | isosceles, not equilateral | equilateral | invalid |
### Equilateral is also isosceles !
### We need to refine the example to make characteristics valid
### Correct Geometric Characterization of triang()’s Inputs

## What’s wrong with this partitioning?

---

<!-- Slide 23 -->

23
Functionality-Based IDM—triang()
Values for this partitioning can be chosen as
## Possible values for geometric partition q1
| Characteristic | b1 | b2 | b3 | b4 |
| --- | --- | --- | --- | --- |
| Triangle | (4, 5, 6) | (3, 3, 4) | (3, 3, 3) | (3, 4, 8) |

---

<!-- Slide 24 -->

24
Functionality-Based IDM—triang()
A different approach would be to break the geometric characterization into four separate characteristics
### Four Characteristics for triang()
| Characteristic | b1 | b2 |
| --- | --- | --- |
| q1 = “Scalene” | True | False |
| q2 = “Isosceles” | True | False |
| q3 = “Equilateral” | True | False |
| q4 = “Valid” | True | False |
### Use constraints to ensure that
Equilateral = True implies Isosceles = True
Valid = False implies Scalene = Isosceles = Equilateral = False

---

<!-- Slide 25 -->

25
Using More than One IDM
Some programs may have dozens or even hundreds of parameters
Create several small IDMs
A divide-and-conquer approach
Different parts of the software can be tested with different amounts of rigor
For example, some IDMs may include a lot of invalid values
It is okay if the different IDMs overlap
The same variable may appear in more than one IDM

---

<!-- Slide 26 -->

26
## Step 4 – Choosing Combinations of Values  (6.2)
Once characteristics and partitions are defined, the next step is to choose test values
We use criteria – to choose effective subsets
The most obvious criterion is to choose all combinations
### All Combinations (ACoC) : All combinations of blocks from all characteristics must be used.
## Number of  tests is the product of the number of blocks in each characteristic :
## The second characterization of triang() results in 4*4*4 = 64 tests
## Too many ?

---

<!-- Slide 27 -->

ISP Criteria – All Combinations
27
| Characteristic | b1 | b2 | b3 | b4 |
| --- | --- | --- | --- | --- |
| q1 = “Refinement of q1” | greater than 1 | equal to 1 | equal to 0 | less than 0 |
| q2 = “Refinement of q2” | greater than 1 | equal to 1 | equal to 0 | less than 0 |
| q3 = “Refinement of q3” | greater than 1 | equal to 1 | equal to 0 | less than 0 |
Consider the “second characterization” of Triang as given before:
| Characteristic | b1 | b2 | b3 | b4 |
| --- | --- | --- | --- | --- |
| A | A1 | A2 | A3 | A4 |
| B | B1 | B2 | B3 | B4 |
| C | C1 | C2 | C3 | C4 |
For convenience, we relabel the blocks:

---

<!-- Slide 28 -->

ISP Criteria – ACoC Tests
28
A1 B1 C1
A1 B1 C2
A1 B1 C3
A1 B1 C4

A1 B2 C1
A1 B2 C2
A1 B2 C3
A1 B2 C4

A1 B3 C1
A1 B3 C2
A1 B3 C3
A1 B3 C4

A1 B4 C1
A1 B4 C2
A1 B4 C3
A1 B4 C4
A2 B1 C1
A2 B1 C2
A2 B1 C3
A2 B1 C4

A2 B2 C1
A2 B2 C2
A2 B2 C3
A2 B2 C4

A2 B3 C1
A2 B3 C2
A2 B3 C3
A2 B3 C4

A2 B4 C1
A2 B4 C2
A2 B4 C3
A2 B4 C4
A3 B1 C1
A3 B1 C2
A3 B1 C3
A3 B1 C4

A3 B2 C1
A3 B2 C2
A3 B2 C3
A3 B2 C4

A3 B3 C1
A3 B3 C2
A3 B3 C3
A3 B3 C4

A3 B4 C1
A3 B4 C2
A3 B4 C3
A3 B4 C4
A4 B1 C1
A4 B1 C2
A4 B1 C3
A4 B1 C4

A4 B2 C1
A4 B2 C2
A4 B2 C3
A4 B2 C4

A4 B3 C1
A4 B3 C2
A4 B3 C3
A4 B3 C4

A4 B4 C1
A4 B4 C2
A4 B4 C3
A4 B4 C4
## ACoC yields 4*4*4 = 64 tests for Triang!
## This is almost certainly more than we need
## Only 8 are valid (all sides greater than zero)

---

<!-- Slide 29 -->

Example
Introduction to Software Testing, Edition 2  (Ch 6)
© Ammann & Offutt
29
## Input: students
## Characteristics: Level, Mode, Major, Classification
## Blocks:
## Level: ( grad, undergrad )
## Mode: ( full-time, part-time )
## Major: ( cs, swe, other )
## Classification: ( in-state, out-of-state )
## Abstract IDM:
## A = [ a1, a2 ]	C = [ c1, c2, c3 ]
## B = [ b1, b2 ]	D = [ d1, d2 ]

---

<!-- Slide 30 -->

In-class exercise
Introduction to Software Testing, Edition 2  (Ch 6)
© Ammann & Offutt
30
## Consider this abstract IDM
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]
## How many tests are needed to satisfy ACoC?
## All combinations criterion (ACoC)

---

<!-- Slide 31 -->

In-class exercise (answer)
Introduction to Software Testing, Edition 2  (Ch 6)
© Ammann & Offutt
31
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]
## All combinations criterion (ACoC)
Number of tests: 2*2*3*2 = 24
| a1 b1 c1 d1 | a1 b2 c1 d1 | a2 b1 c1 d1 | a2 b2 c1 d1 |
| --- | --- | --- | --- |
| a1 b1 c1 d2 | a1 b2 c1 d2 | a2 b1 c1 d2 | a2 b2 c1 d2 |
| a1 b1 c2 d1 | a1 b2 c2 d1 | a2 b1 c2 d1 | a2 b2 c2 d1 |
| a1 b1 c2 d2 | a1 b2 c2 d2 | a2 b1 c2 d2 | a2 b2 c2 d2 |
| a1 b1 c3 d1 | a1 b2 c3 d1 | a2 b1 c3 d1 | a2 b2 c3 d1 |
| a1 b1 c3 d2 | a1 b2 c3 d2 | a2 b1 c3 d2 | a2 b2 c3 d2 |

---

<!-- Slide 32 -->

32
ISP Criteria – Each Choice
64 tests for triang() is almost certainly way too many
One criterion comes from the idea that we should try at least one value from each block
### Each Choice Coverage (ECC) : One value from each block for each characteristic must be used in at least one test case.
## Number of  tests is the number of blocks in the largest characteristic :
## For triang() : A1, B1, C1
## A2, B2, C2
## A3, B3, C3
## A4, B4, C4
## Substituting values:  2, 2, 2
## 1, 1, 1
## 0, 0, 0
## -1, -1, -1

---

<!-- Slide 33 -->

In-class exercise
Introduction to Software Testing, Edition 2  (Ch 6)
© Ammann & Offutt
33
## Apply ECC to our previous example
## How many tests are needed for ECC?
## Design the (abstract) tests
## Each choice criterion (ECC)
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]

---

<!-- Slide 34 -->

In-class exercise (answer)
Introduction to Software Testing, Edition 2  (Ch 6)
© Ammann & Offutt
34
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]
## Each choice criterion (ECC)
Number of tests: max(2,2,3,2) = 3
| a1 b1 c1 d1 |
| --- |
| a2 b2 c2 d2 |
| a1 b1 c3 d1 |

---

<!-- Slide 35 -->

35
ISP Criteria – Pair-Wise
Each choice yields few tests—cheap but maybe ineffective
Another approach combines values with other values
### Pair-Wise Coverage (PWC) :  A value from each block for each characteristic must be combined with a value from every block for each other characteristic.
## Number of  tests is at least the product of two largest characteristics
### For triang() : A1, B1, C1      A1, B2, C2    A1, B3, C3     A1, B4, C4
### A2, B1, C2      A2, B2, C3    A2, B3, C4     A2, B4, C1
### A3, B1, C3      A3, B2, C4    A3, B3, C1     A3, B4, C2
### A4, B1, C4       A4, B2, C1    A4, B3, C2     A4, B4, C3

---

<!-- Slide 36 -->

In-class exercise
Introduction to Software Testing, Edition 2  (Ch 6)
© Ammann & Offutt
36
## Apply PWC to our previous example
## How many tests are needed for PWC?
## Design the (abstract) tests
## Pair-Wise criterion (PWC)
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]

---

<!-- Slide 37 -->

In-class exercise (answer)

37
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]
## Pair-Wise criterion (PWC)
Number of tests: 3*2 = 6
| a1 b1 c1 d1 |
| --- |
| a2 b2 c1 d2 |
| a1 b2 c2 d1 |
| a2 b1 c2 d2 |
| --- |
| a1 b1 c3 d2 |
| a2 b2 c3 d1 |
(a1, b1)
(a1, b2)
(a2, b1)
(a2, b2)
(a1, d1)
(a1, d2)
(a2, d1)
(a2, d2)
(a1, c1)
(a1, c2)
(a1, c3)
(a2, c1)
(a2, c2)
(a2, c3)
(b1, c1)
(b1, c2)
(b1, c3)
(b2, c1)
(b2, c2)
(b2, c3)
(d1, c1)
(d1, c2)
(d1, c3)
(d2, c1)
(d2, c2)
(d2, c3)
(d1, b1)
(d1, b2)
(d2, b1)
(d2, b2)

---

<!-- Slide 38 -->

38
ISP Criteria –T-Wise
A natural extension is to require combinations of t values instead of 2
### t-Wise Coverage (TWC) : A value from each block for each group of t characteristics must be combined.
## Number of  tests is at least the product of  t  largest characteristics
## If all characteristics are the same size, the formula is
## If t is the number of characteristics Q, then all combinations
## That is … Q-wise = AC
## t-wise is expensive and benefits are not clear

---

<!-- Slide 39 -->

39
ISP Criteria – Base Choice
Testers sometimes recognize that certain values are important
This uses domain knowledge of the program
### Base Choice Coverage (BCC) :  A base choice block is chosen for each characteristic, and a base test is formed by using the base choice for each characteristic.  Subsequent tests are chosen by holding all but one base choice constant and using each non-base choice in each other characteristic.
## Number of  tests is one base test + one test for each other block
### For triang() : Base  A1, B1, C1   A1, B1, C2    A1, B2, C1     A2, B1, C1
### A1, B1, C3    A1, B3, C1     A3, B1, C1
### A1, B1, C4    A1, B4, C1     A4, B1, C1

---

<!-- Slide 40 -->

Base Choice Notes
The base test must be feasible
That is, all base choices must be compatible
Base choices can be
Most likely from an end-use point of view
Simplest
Smallest
First in some ordering
Happy path tests often make good base choices
The base choice is a crucial design decision
Test designers should document why the choices were made
40

---

<!-- Slide 41 -->

In-class exercise
Introduction to Software Testing, Edition 2  (Ch 6)
© Ammann & Offutt
41
## Apply BCC to our previous example
## How many tests are needed for BCC?
## Pick base values and write one base test
## Design the remaining (abstract) tests
## Base choice criterion (BCC)
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]

---

<!-- Slide 42 -->

In-class exercise (answer)
Introduction to Software Testing, Edition 2  (Ch 6)
© Ammann & Offutt
42
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]
## Base choice criterion (BCC)
Number of tests: 1(base)+(2-1)+(2-1)+(3-1)+(2-1)
= 1+1+1+2+1=6
| Base | a1 b1 c1 d1 |
| --- | --- |
| A | a2 b1 c1 d1 |
| B | a1 b2 c1 d1 |
| C | a1 b1 c2 d1 |
| C | a1 b1 c3 d1 |
| D | a1 b1 c1 d2 |

---

<!-- Slide 43 -->

43
ISP Criteria – Multiple Base Choice
We sometimes have more than one logical base choice
### Multiple Base Choice Coverage (MBCC) :  At least one, and possibly more, base choice blocks are chosen for each characteristic, and base tests are formed by using each base choice for each characteristic at least once. Subsequent tests are chosen by holding all but one base choice constant for each base test and using each non-base choice in each other characteristic.
### If M base tests and mi base choices for each characteristic:
### For triang() : Bases
### A1, B1, C1   A1, B1, C3   A1, B3, C1    A3, B1, C1
### A1, B1, C4   A1, B4, C1    A4, B1, C1
### A2, B2, C2   A2, B2, C3   A2,  B3, C2   C3, B2, C2
### A2, B2, C4   A2, B4, C2    C3, B2, C2

---

<!-- Slide 44 -->

In-class exercise
Introduction to Software Testing, Edition 2  (Ch 6)
© Ammann & Offutt
44
## Apply MBCC to our previous example
## How many tests are needed for MBCC?
## Design the remaining (abstract) tests with the given base values:
## Two base tests: a1, b1, c1, d1    a2, b2, c2, d2
## Multiple base choice criterion (MBCC)
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]

---

<!-- Slide 45 -->

In-class exercise (answer)

45
### For our example: Two base tests: a1, b1, c1, d1    a2, b2, c2, d2
### Tests from a1, b1, c1, d1:  a1, b1, c3, d1
### Tests from a2, b2, c2, d2:  a2, b2, c3, d2
## 4 Characteristics:  A, B, C, D
## Abstract blocks: A = [a1, a2]; B = [b1, b2];
## C = [c1, c2, c3]; D = [d1, d2]
Number of tests: 2(base)+2*(2-2)+2*(2-2)+2*(3-2)+2*(2-2)
= 2+2 = 4
## Multiple base choice criterion (MBCC)

---

<!-- Slide 46 -->

46
## ISP Coverage Criteria Subsumption

---

<!-- Slide 47 -->

47
Constraints Among Characteristics
Some combinations of blocks are infeasible
“less than zero”  and “scalene” … not possible at the same time
These are represented as constraints among blocks
Two general types of constraints
A block from one characteristic cannot be combined with a specific block from another
A block from one characteristic can ONLY BE combined with a specific block from another characteristic
Handling constraints depends on the criterion used
ACC, PWC, TWC : Drop the infeasible pairs
BCC, MBCC : Change a value to another non-base choice to find a feasible combination
## (6.3)

---

<!-- Slide 48 -->

48
Example Handling Constraints
public boolean findElement (List list, Object element)
// Effects: if list or element is null throw NullPointerException
//           else return true if element is in the list, false otherwise
| Characteristic | Block 1 | Block 2 | Block 3 | Block 4 |
| --- | --- | --- | --- | --- |
| A : length and contents | One element | More than one, unsorted | More than one, sorted | More than one, all identical |
| B : match | element not found | element found once | element found more than once |  |
| Invalid combinations : (A1, B3), (A4, B2) |  |  |  |  |

---

<!-- Slide 49 -->

49
Input Space Partitioning Summary
Fairly easy to apply, even with no automation
Convenient ways to add more or less testing
Applicable to all levels of testing – unit, class, integration, system, etc.
Based only on the input space of the program, not the implementation
## Simple, straightforward, effective, and widely used

---

<!-- Slide 50 -->

Boundary value analysis (BVA)
A domain-oriented technique.
The idea of this method is that the defects are often found on the boundary values of the domains.
Built upon the equivalence partitioning (EP) method.
The first step in applying the BVA is to perform the equivalence partitioning of a given domain.
The boundary values of a given equivalence class are the minimal and maximal elements from this class.
The difference between EP and BVA lies in the way in which we choose class representants to tests.
EP: take one arbitrary element from each class.
BVA: take only the so-called boundary values of the identified classes.


---

<!-- Slide 51 -->

Requirements of BVA
The elements are ordered and we can compare them using the relational operators (<, >, <=, >=, =).
E.g., a set of natural numbers is ordered, because for every two natural numbers, we can say which one is greater and which one is smaller.
Can we apply the BVA to the domain {Linux, Windows, iOS} representing operating systems?
No. Because we cannot compare them. It makes no sense to say that, for example, Windows is greater than or equal to Linux.
Every class needs to be “compact.”
Formally, this means that if any two values a, b belong to a certain class, then necessarily all elements x, such that a < x < b, must also belong to this class.
Informally, we can say that the classes cannot have “holes.”



---

<!-- Slide 52 -->

## Two variants of the BVA method (1)
In a 2-value version, for each identified equivalence class, the test values are:
The boundary values of this class (i.e., the minimal and maximal elements)
The element just below the minimal one
The element just above the maximal one
The two last elements are also the boundary values for the adjoining equivalence classes.
If we want to achieve 100% BVA coverage in the 2-value version, we just have to identify all boundary values for all identified classes and take them as the test inputs.

---

<!-- Slide 53 -->

## Two variants of the BVA method (2)
In a 3-value version, for each identified equivalence class, the test values are:
The boundary values of this class (i.e., the minimal and maximal elements)
The elements just below and just above the minimal one
The elements just below and just above the maximal one
In this case, some test values will not be the boundary values, but the values from the inside of the partitions.

---

<!-- Slide 54 -->

An Example
Suppose we have a domain {1, 2, ..., 15, 16}, which is split into three valid equivalence classes:
{1, ..., 6}, {7, ..., 13}, and {14, ..., 16}
The boundary values:
For the class {1, 2, 3, 4, 5, 6}, the boundary values are 1 and 6.
For the class {7, 8, 9, 10, 11, 12, 13}, the boundary values are 7 and 13.
For the class {14, 15, 16}, the boundary values are 14 and 16.

54

---

<!-- Slide 55 -->

2-value versions of the BVA
The domain is ordered and the classes are with no holes.
In the 2-value, we take the boundary values and their neighbors from other classes.
For the boundary value 1: 0 (if possible), 1
For the boundary value 6: 6, 7
For the boundary value 7: 6, 7
For the boundary value 13: 13, 14
For the boundary value 14: 13, 14
For the boundary value 16: 16, 17 (if possible)
The final set of the test values is equal to the set of all the boundary values: 0 (if possible), 1, 6, 7, 13, 14, 16, 17 (if possible).

#### Equivalence partitioning,
#### Boundary values (and at the same time the test elements for the 2-value version of the BVA),
#### Test elements for the 3-value version of BVA

---

<!-- Slide 56 -->

3-value versions of the BVA
In the 3-value version for each boundary value x, we take three test inputs: x, the value just below x and the value just above x,
For the boundary value 1: 0 (if possible), 1, 2
For the boundary value 6: 5, 6, 7
For the boundary value 7: 6, 7, 8
For the boundary value 13: 12, 13, 14
For the boundary value 14: 13, 14, 15
For the boundary value 16: 15, 16, 17 (if possible)
Hence, the values to test are: 0 (if possible), 1, 2, 5, 6, 7, 8, 12, 13, 14, 15, 16, 17 (if possible).


#### Equivalence partitioning,
#### Boundary values (and at the same time the test elements for the 2-value version of the BVA),
#### Test elements for the 3-value version of BVA

---

<!-- Slide 57 -->

## Strength of the 3-value version (1)
Suppose that the code (assume x and y are integers):
if (x >= 15) then y := 0
was incorrectly implemented as
if (x == 15) then y := 0
In the2-value version, we test the boundary (x >= 15), so the boundary values are 14 and 15.
In case of 14, we see that the outcomes of both correct and incorrect implementations of the predicate are FALSE, because it is not true that 14 >= 15, and it is also not true that 14 = 15.
In case of 15 also, both implementations give the same logical value (TRUE): it is true that 15 >= 15 and it is also true that 15 = 15.
Hence, neither the test 14, nor 15, detected the fault—in both cases, the expected and actual results are the same!

---

<!-- Slide 58 -->

## Strength of the 3-value version (2)
Suppose that the code (assume x and y are integers):
if (x >= 15) then y := 0
was incorrectly implemented as
if (x == 15) then y := 0
If we use the 3-value version, we need to test not only 14 and 15, but also 16.
In case of 16, the condition (x >= 15) is true (because 16 > 15), but the outcome of the faulty implementation is false, since it is not true that 16 = 15.
Hence, we detected the fault: the expected result (true) is different from the actual one (false).

58

---

<!-- Slide 59 -->

## How to deal with continuous domains?
Suppose we have a set of real numbers from 0 to 1 inclusively.
The boundary values of this class are obviously 0 and 1, but what are the neighbors from the adjoining classes?
E.g., what is the value just above 1? Is it 2? Or 1.01? Or may be 1.0001?
In fact, for every such value, we can find some smaller one, but still greater than 1.
It is because the set of real numbers is dense.


---

<!-- Slide 60 -->

Practical Solutions
The smallest increment is defined either by the nature of the problem, or by the way the numbers are represented in the computer memory.
E.g., if we test an e-shop application and the considered variable stores some price in dollars, it is obvious that the smallest increment is $0.01 (one cent). In this case, the boundary values for the set [0, 1] will be 0.01 and 1.01 dollars.
If the variable represents some physical value (like the rocket velocity), the precision is defined by the way the value is represented in the memory. The tester may also define other greater, reasonable increment.

60

---

<!-- Slide 61 -->

Exercise 1
For which of the following variables, the application of the BVA method is possible?
(a) The set of integer numbers
(b) The set of real numbers
(c) The set {5, 6, 7}
(d) The set of all strings of length 1, 2 or 3
(e) The set {Linux, Windows, MacOS}

For A, B, and C, we can apply BVA method, because these domains are ordered.
For D and E, we cannot apply BVA method, because the elements are incomparable. However, we could introduce the ordering on these sets and then apply the BVA method.
For example, in case of strings, we could introduce the classical, lexicographic ordering. Then, each string could be compared with another, for example: aaa < aab, az < ba etc.

---

<!-- Slide 62 -->

Exercise 2
A system accepts the year of birth (an integer number). The valid years are between 1900 and 2020. Which of the following is the minimal set of test values that achieves both boundary value and equivalence partition coverage?
A. 2003
B. 1900, 2020
C. 1900, 2003, 2020
D. 1899, 1900, 2020, 2021
E. 1899, 1900, 2003, 2020, 2021

Equivalence classes: {..., 1898, 1899}, {1900, 1901, ..., 2019, 2020},{2021, 2022, . . .}.
Boundary values: 1899, 1900, 2020, 2021.
Notice that a boundary value belonging to a class C is also the value from this class, so it covers the partition C.
Hence, four tests are enough and the correct answer is D.

---

<!-- Slide 63 -->

Exercise 3
当电梯中人员的总重量超过 280 kg 时，重量传感器可检测电梯过载情况。你希望验证传感器是否正确实现了该要求。每个测试模拟一定负载（以千克为量）。如果采用边界值划分（BVA）方法，试分别给出采用 2-value BVA 和 3-value BVA 两种不同方式达到 100%BVA 覆盖的最小测试用例集合。

边界条件为 w > 280，
等价类：{. . ., 279, 280}和{281, 282, . . .}
采用 2-value 方式：达到 100%BVA 覆盖的最小测试用例集合：{280，281}
采用 3-value 方式：达到 100%BVA 覆盖的最小测试用例集合：{279，280，281，282}

---

<!-- Slide 64 -->

Exercise 4
A shopping discount system takes as an input the total price T (a positive integer with precision of 1 cent), rounds it to the nearest integer value (in dollars), and basing on this value calculates a discount using the rules presented in the following table.




You want to test if the system correctly calculates the discount for a given total price T. Which of the following is a set of boundary values for one of the equivalence classes of a variable T? Assume that you follow 2-point boundary value analysis.
$0.01, $99.49
$0, $100
$100, $299
$299.49, $299.50
Correct answer: A

---

<!-- Slide 65 -->

Exercise 5
### You test one of the on-line banking system functions that verifies the correctness of the PIN for a credit card. A valid PIN:
### Must contain at least 4 and at most 6 digits
### Must contain at least 2 different digits
### You want to apply a 2-point boundary value analysis for checking that the system follows the two above rules. A test case consists of a PIN number. Which set of test cases covers all the boundary values that you need to test?
### 123, 1234, 123456, 1234567
### 949, 0011, 33333, 123123, 6667778
### 123, 1111, 123456, 1234567
### 777, 8888, 999999, 4444444

Correct answer: B

---
