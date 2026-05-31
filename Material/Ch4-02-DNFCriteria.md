## Slide 1

- **Chapter 4 Logic Coverage**
- **Syntactic Logic Coverage Criteria**
- **(8.2 Disjunctive Normal Form)**

## Slide 2

- **本节课程目标**
- **掌握DNF记法，了解字（literal）、项（term）、蕴含项（implicant）的概念；**
- **知晓真子项、主蕴含项、冗余蕴含项、最小DNF表示形式的含义；**
- **明确唯真点（UTP）、近假点（NFP）的含义，写出谓词表达式DNF形式中蕴含项的唯真点和近假点；**
- **明确从语法角度出发的主要逻辑覆盖标准的含义，包括IC、MUTP、CUTPNFP、MNFP等，能写出上述覆盖标准的测试需求；**
- **了解DNF典型的fault种类及它们之间的包含关系，明确MUTP和CUTPNFP对上述各类fault的检测能力；**
- **应用卡诺图分析逻辑覆盖相关概念。**
- **2**

## Slide 3

- **Disjunctive Normal Form**
- **Common Representation for Boolean Functions**
  - Slightly Different Notation for Operators
  - Slightly Different Terminology
- **Basics:**
  - A literal is a clause or the negation (overstrike) of a clause
    - Examples:  a, a
  - A term is a set of literals connected by logical “and”
    - “and” is denoted by adjacency instead of 
    - Examples: ab, ab, ab  for a  b, a  ¬ b, ¬ a  ¬ b
  - A (disjunctive normal form) predicate is a set of terms connected by “or”
    - “or” is denoted by + instead of 
    - Examples: abc + ab + ac
    - Terms are also called “implicants”
      - If a term is true, that implies the predicate is true
- **3**

## Slide 4

- **Implicant Coverage (8.2.1)**
- **Obvious coverage idea :  Make each implicant evaluate to “true”**
  - Problem :  Only tests  “true” cases for the predicate
  - Solution :  Include DNF representations for negation
- **Implicant Coverage (IC) : Given DNF representations of a predicate f and its negation f, for each implicant in f and f, TR contains the requirement that the implicant evaluate to true.**
- **Example:   f = ab + bc       f = b + ac**
  - Implicants:  { ab, bc, b, ac }
  - Possible test set:  {TTF, FFT}
- **Observation:  IC is relatively weak**
- **4**

## Slide 5

- **Improving on Implicant Coverage**
- **Additional Definitions :**
  - A proper subterm is a term with one or more clauses removed
    - Example:  abc has 6 proper subterms:  a, b, c, ab, ac, bc
  - A prime implicant is an implicant such that no proper subterm is also an implicant
    - Example:  f = ac + abc
    - Implicant ac is a prime implicant
    - Implicant abc is not a prime implicant (due to proper subterm ac)
  - A redundant implicant is an implicant that can be removed without changing the value of the predicate
    - Example:  f = ab + ac + bc
    - ab is redundant
    - Predicate can be written:  ac + bc
- **5**

## Slide 6

- **Unique True Points**
- **A minimal DNF representation is one with only prime, non-redundant implicants**
- **A unique true point with respect to a given implicant is an assignment of truth values so that**
  - The given implicant is true, and
  - All other implicants are false
- **A unique true point test focuses on just one implicant**
- **A minimal representation guarantees the existence of at least one unique true point for each implicant**
- **Multiple Unique True Point Coverage (MUTP) : Given minimal DNF representations of a predicate f, for each implicant i, choose unique true points (UTPs) such that clauses not in i take on values T and F.**
- **6**

## Slide 7

- **Unique True Point Example**
- **Consider again :   f = ab + bc**
  - Implicants :  { ab, bc }
  - Each implicants is prime
  - None implicant is redundant
- **Unique true points :**
  - ab: {TTT}
  - bc: {FTF}
  - MUTP requires both of these
- **But MUTP is still infeasible for both implicants**
  - Not enough UTPs for clauses to take on all truth values
  - Later, we will have an example where MUTP is feasible
- **7**

## Slide 8

- **Near False Points**
- **A  near false point with respect to a clause c in implicant i is an assignment of truth values such that f is false, but if c is negated (and all other clauses left as is), i (and hence f) evaluates to true**
- **Relation to determination: at a near false point, c determines f**
  - Hence we should expect relationship to ACC criteria
- **Note that definition only mentions f, and not f**
- **Clearly, CUTPNFP subsumes RACC**
- **Unique True Point and Near False Point Pair Coverage (CUTPNFP) : Given a minimal DNF representation of a predicate f, for each clause c in each implicant i, TR contains a unique true point for i and a near false point for c such that the points differ only in the truth value of c.**
- **8**

## Slide 9

- **CUTPNFP Example**
- **Consider f = ab + cd**
  - Implicant ab has 3 unique true points : {TTFF, TTFT, TTTF}
    - For clause a, we can pair unique true point TTFF with near false point FTFF
    - For clause b, we can pair unique true point TTFF with near false point TFFF
  - Implicant cd has 3 unique true points : {FFTT, FTTT, TFTT}
    - For clause c, we can pair unique true point FFTT with near false point FFFT
    - For clause d, we can pair unique true point FFTT with near false point FFTF
- **CUTPNFP set : {TTFF, FFTT, TFFF, FTFF, FFTF, FFFT}**
  - First two tests are unique true points; others are near false points
- **Rough number of tests required: #  implicants * # literals**
- **9**

## Slide 10

- **The MNFP and MUMCUT Criteria**
  - The next two criteria provide enough scaffolding to make guarantees about fault detection (see later slides)
- **Multiple Near False Point Coverage (MNFP) : Given a minimal DNF representation of a predicate f, for each literal c in each implicant i, TR choose near false points (NFPs) such that clauses not in i take on values T and F.**
- **10**
- **MUMCUT : Given a minimal DNF representation of a predicate f,  apply MUTP, CUTPNFP, and MNFP.**

## Slide 11

- **MNFP Example**
- **Consider again :   f = ab + bc**
  - Implicants :  { ab, bc }
- **True points :**
  - ab: TTT, TTF
    - NFP for a where c=T: {FTT}
    - Infeasible NFP for a where c = F
    - NFPs for b where c = T, F: {TFT, TFF}
  - bc:  FTF, TTF
    - NFPs for b where a = T, F:  {TFF, FFF}
    - NFP for c where a = F: {FTT}
    - Infeasible NFP for c where a = T
- **Resulting MNFP set = {FTT, TFT, TFF, FFF}**
- **11**

## Slide 12

- **DNF Fault Classes**
- **ENF: Expression Negation Fault   f = ab+c        f’ = ab+c**
- **TNF: Term Negation Fault          f = ab+c         f’ = ab+c**
- **TOF: Term Omission Fault          f = ab+c	        f’ = ab**
- **LNF: Literal Negation Fault          f = ab+c	        f’ = ab+c**
- **LRF: Literal Reference Fault         f = ab + bcd   f’ = ad + bcd**
- **LOF: Literal Omission Fault         f = ab + c      f’ = a + c**
- **LIF: Literal Insertion Fault            f = ab + c      f’ = ab + bc**
- **ORF+: Operator Reference Fault f = ab + c      f’ = abc**
- **ORF*: Operator Reference Fault f = ab + c      f’ = a + b + c**
- **Key idea is that fault classes are related with respect to testing :**
- **Test sets guaranteed to detect certain faults are also**
- **guaranteed to detect additional faults**
- **12**

## Slide 13

- **Fault Detection Relationships**
- **13**

## Slide 14

- **MUTP可以检测所有的LIF**
- **Take f=ab+cd as example, suppose f is written as abl+cd**
  - If l is a, then the value of ab won’t change. It does not matter.
  - If l is a’, then the fault can be detected by TTFT and TTTF with MUTP. i.e. the expected result is T, but the actual result is F.
  - If l is c, then the fault can be detected by TTFT with MUTP. i.e. the expected result is T, but the actual result is F.
  - If l is c’, then the fault can be detected by TTTF with MUTP. i.e. the expected result is T, but the actual result is F.
- **14**

## Slide 15

- **CUTPNFP可以检测所有的LOF**
- **Take f=ab+cd as example, suppose c is omitted and f is written as ab+d**
  - the fault can be detected by FFTT (UTP) and FFFT (NFP) with CUTPNFP. i.e. the expected result of UTP is T, the expected result of NFP is F, but the actual result of NFP is T.
- **15**

## Slide 16

- **Comparison between Syntactic  and Semantic Coverage Criterion**
- **Compared to a semantic coverage criterion such as RACC, MUMCUT is quite expensive in terms of the number of tests needed for a given predicate.**
- **Significant benefit to extra tests.**
  - From a theoretical perspective, RACC is only guaranteed to detect all instances of the TNF and ENF faults. RACC tests are not guaranteed to detect the faults for the other seven fault classes.
  - In practice, researchers have found that RACC tests only detect about one-third of the faults from the fault hierarchy, failing to detect two-thirds.
  - Thus, MUMCUT should be considered when testing applications where the consequences of failures are especially severe.
- **16**

## Slide 17

- **Karnaugh Maps for Testing Logic Expressions**
- **Fair Warning**
  - We use, rather than teach, Karnaugh Maps
  - Newcomers to Karnaugh Maps probably need a tutorial
    - Suggestion:  Google “Karnaugh Map Tutorial”
- **Our goal:  Apply Karnaugh Maps to concepts used to test logic expressions**
  - Identify when a clause determines a predicate
  - Identify the negation of a predicate
  - Identify prime implicants and redundant implicants
  - Identify unique true points
  - Identify unique true point / near false point pairs
- **No new material here on testing**
  - Just fast shortcuts for concepts already presented
- **17**

## Slide 18

- **K-Map:  A Clause Determines a Predicate**
- **Consider the predicate :  f = b + ac + ac**
- **Suppose we want to identify when b determines f**
- **The dashed line highlights where b changes value**
  - If two cells joined by the dashed line have different values for f, then b determines f for those two cells
  - b determines f:  ac + ac  (but NOT at ac or ac )
- **Repeat for clauses a and c**
- **18**

## Slide 19

- **K-Map:  Negation of a predicate**
- **Consider the predicate:  f = ab + bc**
- **Draw the Karnaugh Map for the negation**
  - Identify groups
  - Write down negation:  f = b + a c
- **19**

## Slide 20

- **K-Map:  Prime and Redundant Implicants**
- **Consider the predicate:  f = abc + abd + abcd + abcd + acd**
- **Draw the Karnaugh Map**
- **Implicants that are not prime: abd,  abcd,  abcd,  acd**
- **Redundant implicant: abd**
- **Prime implicants**
  - Three:  ad, bcd, abc
  - The last is redundant
  - Minimal DNF representation
    - f = ad + bcd
- **20**

## Slide 21

- **K-Map:  Unique True Points**
- **Consider the predicate:  f = ab + cd**
- **Three unique true points for ab**
  - TTFF, TTFT, TTTF
  - TTTT is a true point, but not a unique true point
- **Three unique true points for cd**
  - FFTT, FTTT, TFTT
- **Unique true points for f**
  - f = ac + bc + ad + bd
  - FTFT,TFFT, FTTF, TFTF
- **21**
- **Unique true points are simply true points covered by a single rectangle.**

## Slide 22

- **For MUTP, we can identify unique true points where clauses not in the term take on both truth values.**
- **For each implicant find unique true points (UTPs) so that**
  - Literals not in implicant take on values T and F
- **Consider the DNF predicate:**
  - f = ab + cd
- **For implicant ab**
  - Choose TTFT, TTTF
- **For implicant cd**
  - Choose FTTT, TFTT
- **MUTP test set**
  - {TTFT, TTTF, FTTT, TFTT}
- **MUTP: Multiple Unique True Points**
- **22**

## Slide 23

- **23**
- **Near false points for any given true point are simply those false points that are immediately adjacent in the Karnaugh map.**
- **For CUTPNFP, pair up near false points with unique true points, being careful to obtain a pairing for each clause in f.**
- **CUTPNFP: Corresponding Unique True Point Near False Point Pairs**

## Slide 24

- **CUTPNFP: Corresponding Unique True Point Near False Point Pairs**
- **Consider the DNF predicate:  f = ab + cd**
- **For implicant ab**
  - For a, choose UTP, NFP pair
    - TTFF, FTFF
  - For b, choose UTP, NFP pair
    - TTFT, TFFT
- **For implicant cd**
  - For c, choose UTP, NFP pair
    - FFTT, FFFT
  - For d, choose UTP, NFP pair
    - FFTT, FFTF
- **Possible CUTPNFP test set**
  - {TTFF, TTFT, FFTT              //UTPs
  - FTFF, TFFT, FFFT, FFTF} //NFPs
- **24**

## Slide 25

- **Find NFP tests for each literal such that all literals not in the term attain F and T**
- **Consider the DNF predicate:**
  - f = ab + cd
- **For implicant ab**
  - Choose FTFT, FTTF for a
  - Choose TFFT, TFTF for b
- **For implicant cd**
  - Choose FTFT, TFFT for c
  - Choose FTTF, TFTF for d
- **MNFP test set**
  - {TFTF, TFFT, FTTF, TFTF}
- **Example is small, but generally MNFP is large**
- **MNFP : Multiple Near False Points**
- **25**

## Slide 26

- **26**
- **Minimal-MUMCUT CriterionKaminski/Ammann (ICST 2009)**
- **Minimal-MUMCUT uses low level criterion feasibility analysis**
  - Adds CUTPNFP and MNFP only when necessary
- **Minimal-MUMCUT guarantees detecting LIF, LRF, LOF**
  - And thus all 9 faults in the hierarchy
