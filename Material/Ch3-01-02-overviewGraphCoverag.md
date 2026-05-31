<!-- Slide 1 -->

Chapter 3 Graph Coverage
3.1 Overview &
3.2 Graph Coverage Criteria

---

<!-- Slide 2 -->

本节课程目标
### 描述图的形式化定义；
### 明确与图相关的主要术语的含义；
### 明确结构化覆盖图的思路及主要覆盖标准之间的包含关系；
### 写出点覆盖、边覆盖、边对覆盖、主路径覆盖的测试需求及满足上述测试需求的测试路径（包括sidetrip和detour游历）
### 明确definition集合、use集合、DU-pair、DU-path的含义，写出definition集合、use集合中的元素，写出DU-pair、DU-path；
### 明确覆盖标准ADC、AUC、ADUPC的含义，写出上述覆盖标准的测试需求及满足对应测试需求的测试路径（包括sidetrip和detour游历）；
### 明确主要的图覆盖标准（包括结构化覆盖和数据流覆盖）之间的包含关系。

2

---

<!-- Slide 3 -->

Ch. 3 : Graph Coverage
3
## Four Structures for Modeling Software




---

<!-- Slide 4 -->

Covering Graphs
Graphs are the most commonly used structure for testing
Graphs can come from many sources
Control flow graphs
Design structure
FSMs and statecharts
Use cases
Tests usually are intended to “cover” the graph in some way
4

---

<!-- Slide 5 -->

5
Definition of a Graph
N0 = { 1 }
Nf = { 1 }
E = { }
### Is this a graph?
Yes

---

<!-- Slide 6 -->

Write down the initial and final nodes, and the edges
Write down the initial and final nodes, and the edges
6
Example Graphs
N0 = { }
Nf = { 4 }
E = { (1,2), (1,3), (2,4), (3,4) }
N0 = { 1, 2, 3 }
Nf = { 8, 9, 10 }
E = { (1,4), (1,5), (2,5), (3,6), (3, 7), (4, 8), (5,8), (5,9), (6,2), (6,10), (7,10) (9,6) }
Not a
valid
graph
Write down the initial and final nodes, and the edges
N0 = { 1 }
Nf = { 4 }
E = { (1,2), (1,3), (2,4), (3,4) }

---

<!-- Slide 7 -->

Write down three paths in this graph
7
Paths in Graphs
A Few Paths
[ 1, 4, 8 ]
[ 2, 5, 9, 6, 2 ]
[ 3, 7, 10 ]

---

<!-- Slide 8 -->

Paths in Graphs
Reach (n) : Subgraph that can be reached from n
A node n is syntactically reachable from node ni if there exist a path from ni to n.
A location in a graph (node or edge) can be reached from another location if there is a sequence of edges from the first location to the second
Syntactic reach : A subpath exists in the graph
Semantic reach : A test exists that can execute that subpath
This distinction becomes important in section 2.3
8

---

<!-- Slide 9 -->

Paths in Graphs
**Each coverage criterion are based on reachG(N0)**
**syntactically**

9
reach (0) = { 0, 3, 4, 7, 8, 5, 1, 9 }
reach ({0, 2}) = N
reach([2,6]) = {2, 6, 9}

---

<!-- Slide 10 -->

Write down all the test paths in this graph
10
Test Paths and SESEs
Test Path : A path that starts at an initial node and ends at a final node
Test paths represent execution of test cases
### Some test paths can be executed by many tests
### Some test paths cannot be executed by any tests
SESE graphs : All  test paths start at a single node and end at another node
### Single-entry, single-exit
### N0 and Nf have exactly one node
Double-diamond graph
Four test paths
[1, 2, 4, 5, 7]
[1, 2, 4, 6, 7]
[1, 3, 4, 5, 7]
[1, 3, 4, 6, 7]

---

<!-- Slide 11 -->

11
Visiting and Touring
Visit : A test path p visits node n if n is in p
A test path p visits edge e if e is in p
Tour : A test path p tours subpath q if q is a subpath of p
### Test path [ 1, 2, 4, 5, 7 ]
### Visits nodes ?
### Visits edges ?
### Tours subpaths ?


### 1, 2, 4, 5, 7
### (1,2), (2,4), (4, 5), (5, 7)
### [1,2,4], [2,4,5], [4,5,7], [1,2,4,5], [2,4,5,7], [1,2,4,5,7]
### (Also, each edge is technically a subpath)

---

<!-- Slide 12 -->

12
Tests and Test Paths
path (t) : The test path executed by test t
path (T) : The set of test paths executed by the set of tests T
**For determinstic graph, each test executes one and only one test path**
Complete execution from a start node to an final node

---

<!-- Slide 13 -->

13
Tests and Test Paths
### test 1
### test 2
### test 3

---

<!-- Slide 14 -->

Exercises
List all test paths in the graph

0,3,7
0,4,7
0,4,8
0,4,8,5,9
1,4,8
1,4,7
1,4,8,5,9
2,5,9
2,6,9
#### 2,5,1,4,8(包含多个初始节点)
2,5,1,4,7
……

---

<!-- Slide 15 -->

Exercises
Find test case inputs such that the corresponding test path visits edge (n1,n3)
15
Test case t1 : (a=0, b=1)
Test path p1 : [n0, n1, n3, n2 ]

Test case t2 : (a=1, b=1)
Test path p2 : [n0, n3, n2 ]

Test case t3 : (a=2, b=1)
Test path p3 : [n0, n2 ]

---

<!-- Slide 16 -->

Testing and Covering Graphs
We use graphs in testing as follows :
Develop a model of the software as a graph
Require tests to visit or tour specific sets of nodes, edges or subpaths
Satisfaction : Given a set TR of test requirements for a criterion C, a set of tests T satisfies C on a graph if and only if for every test requirement in TR, there is a test path in path(T) that meets the test requirement tr
Structural Coverage Criteria : Defined on a graph just in terms of nodes and edges
Data Flow Coverage Criteria : Requires a graph to be annotated with references to variables


16

---

<!-- Slide 17 -->

17
Node and Edge Coverage
The first (and simplest) two criteria require that each node and edge in a graph be executed
### Node Coverage (NC) : Test set T satisfies node coverage on graph G iff for every syntactically reachable node n in N, there is some path p in path(T) such that p visits n.
### Node Coverage (NC) : TR contains each reachable node in G.
## This statement is a bit cumbersome, so we abbreviate it in terms of the set of test requirements

---

<!-- Slide 18 -->

18
Node and Edge Coverage
Edge coverage is slightly stronger than node coverage
### Edge Coverage (EC) : TR contains each reachable path of length up to 1, inclusive, in G.
## The phrase “length up to 1” allows for graphs with one node and no edges
## NC and EC are only different when there is an edge and another subpath between a pair of nodes (as in an “if-else” statement)
Node Coverage :  ?


Edge Coverage : ?


TR = { 1, 2, 3 }
Test Path = [ 1, 2, 3 ]
TR = { (1, 2), (1, 3), (2, 3) }
Test Paths = [ 1, 2, 3 ]
[ 1, 3 ]

---

<!-- Slide 19 -->

19
Paths of Length 1 and 0
A graph with only one node will not have any edges
## It may seem trivial, but formally, Edge Coverage needs to require Node Coverage on this graph
## Otherwise, Edge Coverage will not subsume Node Coverage
### So we define “length up to 1” instead of simply “length 1”
## We have the same issue with graphs that only have one edge – for Edge-Pair Coverage …

---

<!-- Slide 20 -->

20
Covering Multiple Edges
Edge-pair coverage requires pairs of edges, or subpaths of length 2
### Edge-Pair Coverage (EPC) : TR contains each reachable path of length up to 2, inclusive, in G.
## The phrase “length up to 2” is used to include graphs that have less than 2 edges
## The logical extension is to require all paths …
Edge-Pair Coverage :  ?



TR = { [1,4,5], [1,4,6], [2,4,5], [2,4,6], [3,4,5], [3,4,6] }

---

<!-- Slide 21 -->

21
Covering Multiple Edges
### Complete Path Coverage (CPC) : TR contains all paths in G.
### Specified Path Coverage (SPC) : TR contains a set S of test paths, where S is supplied as a parameter.
## Unfortunately, this is impossible if the graph has a loop, so a weak compromise makes the tester decide which paths:

---

<!-- Slide 22 -->

Structural Coverage Example
22










Node Coverage
TR =
Test Paths:
Edge Coverage
TR =

Test Paths:
Edge-Pair Coverage
TR =

Test Paths:

Complete Path Coverage
Test Paths:

Node Coverage
TR = { 1, 2, 3, 4, 5, 6, 7 }
Test Paths: [ 1, 2, 3, 4, 7 ] [ 1, 2, 3, 5, 6, 5, 7 ]
Edge Coverage
TR = { (1,2), (1, 3), (2, 3), (3, 4), (3, 5), (4, 7), (5, 6), (5, 7), (6, 5) }
Test Paths: [ 1, 2, 3, 4, 7 ] [1, 3, 5, 6, 5, 7 ]
Edge-Pair Coverage
TR = { [1,2,3], [1,3,4], [1,3,5], [2,3,4], [2,3,5], [3,4,7],
[3,5,6], [3,5,7], [5,6,5], [6,5,6], [6,5,7] }
Test Paths: [ 1, 2, 3, 4, 7 ] [ 1, 2, 3, 5, 7 ] [ 1, 3, 4, 7 ]
[ 1, 3, 5, 6, 5, 6, 5, 7 ]
Complete Path Coverage
Test Paths: [ 1, 2, 3, 4, 7 ] [ 1, 2, 3, 5, 7 ] [ 1, 2, 3, 5, 6, 5, 7 ] [ 1, 2, 3, 5, 6, 5, 6, 5, 7 ] [ 1, 2, 3, 5, 6, 5, 6, 5, 6, 5, 7 ] …
Write down the TRs and Test Paths for these criteria

---

<!-- Slide 23 -->

23
Handling Loops in Graphs
If a graph contains a loop, it has an infinite number of paths

Thus, CPC is not feasible

SPC is not satisfactory because the results are subjective and vary with the tester

Attempts to “deal with” loops:
### 1970s : Execute cycles once  ([5, 6, 5] in previous example, informal)
### 1980s : Execute each loop, exactly once (formalized)
### 1990s : Execute loops 0 times, once, more than once (informal description)
### 2000s : Prime paths (touring, sidetrips, and detours)

---

<!-- Slide 24 -->

Simple Paths and Prime Paths
Simple Path : A path from node ni to nj is simple if no node appears more than once, except possibly the first and last nodes are the same
No internal loops
A loop is a simple path
Prime Path : A simple path that does not appear as a proper subpath of any other simple path

24
Simple Paths :




Prime Paths :

[1,2,4,1], [1,3,4,1], [2,4,1,2], [2,4,1,3], [3,4,1,2], [3,4,1,3], [4,1,2,4], [4,1,3,4], [1,2,4], [1,3,4], [2,4,1], [3,4,1], [4,1,2], [4,1,3], [1,2], [1,3], [2,4], [3,4], [4,1], [1], [2], [3], [4]

[2,4,1,2], [2,4,1,3], [1,3,4,1], [1,2,4,1], [3,4,1,2], [4,1,3,4], [4,1,2,4], [3,4,1,3]
Write down the simple and prime paths for this graph

---

<!-- Slide 25 -->

25
Prime Path Coverage
A simple, elegant and finite criterion that requires loops to be executed as well as skipped
### Prime Path Coverage (PPC) : TR contains each prime path in G.
## Will tour all paths of length 0, 1, …
## That is, it subsumes node and edge coverage
## PPC almost, but not quite, subsumes EPC…
## Why?

---

<!-- Slide 26 -->

PPC Does Not Subsume EPC
26
## If a node n has an edge to itself (self edge), EPC requires [n, n, m] and [m, n, n]
## [n, n, m] is not prime
## Neither [n, n, m] nor [m, n, n] are simple paths (not prime)
EPC Requirements :  ?


TR = { [1,2,3], [1,2,2], [2,2,3], [2,2,2] }
PPC Requirements :  ?


TR = { [1,2,3], [2,2] }

---

<!-- Slide 27 -->

Simple & Prime Path Example
27
Len 0







Simple paths
[1]
[2]
[3]
[4]
[5]
[6]
[7] !

Write paths of length 0
‘!’ means path terminates
Len 1









[1, 2]
[1, 3]
[2, 3]
[3, 4]
[3, 5]
[4, 7] !
[5, 7] !
[5, 6]
[6, 5]

Write paths of length 1
Len 2











[1, 2, 3]
[1, 3, 4]
[1, 3, 5]
[2, 3, 4]
[2, 3, 5]
[3, 4, 7] !
[3, 5, 7] !
[3, 5, 6] !
[5, 6, 5] *
[6, 5, 7] !
[6, 5, 6] *

Write paths of length 2
‘*’ means path cycles
Len 3








[1, 2, 3, 4]
[1, 2, 3, 5]
[1, 3, 4, 7] !
[1, 3, 5, 7] !
[1, 3, 5, 6] !
[2, 3, 4, 7] !
[2, 3, 5, 6] !
[2, 3, 5, 7] !

Write paths of length 3
Len 4



[1, 2, 3, 4, 7] !
[1, 2, 3, 5, 7] !
[1, 2, 3, 5, 6] !

Write paths of length 4
Prime Paths ?

---

<!-- Slide 28 -->

Introduction to Software Testing, Edition 2  (Ch 07)
© Ammann & Offutt
28
Prime Path Example
The previous example has 38 simple paths
Only nine prime paths
Prime Paths









Execute loop once
Execute loop more than once
Execute loop 0 times
[1, 2, 3, 4, 7]
[1, 2, 3, 5, 7]
[1, 2, 3, 5, 6]
[1, 3, 4, 7]
[1, 3, 5, 7]
[1, 3, 5, 6]
[6, 5, 7]
[6, 5, 6]
[5, 6, 5]

Write down all 9 prime paths

---

<!-- Slide 29 -->

29
Touring, Sidetrips, and Detours
Prime paths do not have internal loops … test paths might
## Tour : A test path p tours subpath q if q is a subpath of p
## Tour With Sidetrips : A test path p tours subpath q with sidetrips iff every edge in q is also in p in the same order
### The tour can include a sidetrip, as long as it comes back to the same node
## Tour With Detours : A test path p tours subpath q with detours iff every node in q is also in p in the same order
### The tour can include a detour from node ni, as long as it comes back to the prime path at a successor of ni

---

<!-- Slide 30 -->

30
Sidetrips and Detours Example
Touring the prime path [1, 2, 3, 5, 6] without sidetrips or detours

---

<!-- Slide 31 -->

31
Infeasible Test Requirements
An infeasible test requirement cannot be satisfied
### Unreachable statement (dead code)
### Subpath that can only be executed with a contradiction (X > 0 and X < 0)
### Practical recommendation—Best Effort Touring
#### Satisfy as many test requirements as possible without sidetrips
#### Allow sidetrips to try to satisfy remaining test requirements
## Most test criteria have some infeasible test requirements
## It is usually undecidable whether all test requirements are feasible
## When sidetrips are not allowed, many structural criteria have more infeasible test requirements
## However, always allowing sidetrips weakens the test criteria

---

<!-- Slide 32 -->

Best Effort Touring
Let TRtour  be the subset of test requirements that can be toured and TRsidetrip be the subset of test requirements that can be toured with sidetrips.
Note that TRtour ⊆TRsidetrip.
A set T of test paths achieves best effort touring if for every path p in TRtour  some path in T tours p directly and for every path p in Trsidetrip , some paths in T tours p either directly or with a sidetrip.

---

<!-- Slide 33 -->

33
Round Trips
Round-Trip Path : A prime path that starts and ends at the same node
### Simple Round Trip Coverage (SRTC) : TR contains at least one round-trip path for each reachable node in G that begins and ends a round-trip path.
### Complete Round Trip Coverage (CRTC) : TR contains all round-trip paths for each reachable node in G.
## These criteria omit nodes and edges that are not in round trips
## Thus, they do not subsume edge-pair, edge, or node coverage

---

<!-- Slide 34 -->

Questions (1)
**如何在测试过程中使用图？**
将软件开发过程中的产物建模成图，然后按照指定的覆盖准则覆盖图，如访问指定的节点集合、边或游历指定的子路径。
分别对应两个方面的问题：软件开发产物与图之间如何建立联系？如何设计合适的覆盖准则？
**一般从哪些角度设计图覆盖标准？**
结构化覆盖（覆盖点、边、子路径）
数据流覆盖（在图中体现程序中的变量，考虑如何覆盖变量）
**常见的结构化图覆盖标准有哪些？**
点覆盖、边覆盖、边对覆盖、完全路径覆盖、指定路径覆盖、主路径覆盖、简单环路覆盖、完全环路覆盖

34

---

<!-- Slide 35 -->

Questions (2)
**一个有效的图应该具备哪些要素？**
非空的节点集合、非空的起始节点集合、非空的终结节点集合、边集（可以为空）
**Syntactic reach和Semantic reach的区别是什么？**
语法仅是从图的结构上存在对应的子路径，
语义是指存在测试用例能够执行对应的子路径
**Visit和tour有何区别？**
## 作用对象不同：visit作用于点或边；tour作用于子路径
## 但如果把边视作子路径，则使用tour亦可

35

---

<!-- Slide 36 -->

Questions (3)
**路径与测试路径的区别是什么？**
测试路径必须从起始节点开始并以终结节点结束。
路径没有上述要求。
**测试用例与测试路径之间的关系是什么？**
确定的测试：一个测试用例执行唯一一个测试路径。测试用例与测试路径之间是多对一的关系
不确定的测试：测试用例与测试路径之间是多对多的关系
然而，存在不可能被测试用例执行的测试路径。
**什么是简单路径？什么是主路径？**
简单路径：首尾节点不同的路径除非是环，即没有内部环路的路径。
主路径：不作为其他简单路径的真子路径出现的简单路径，即不能再延申的简单路径

36

---

<!-- Slide 37 -->

Questions (4)
**点覆盖与边覆盖之间的关系是什么？在什么情况下存在不同的测试需求？**
边覆盖包含点覆盖。
在一对节点间存在一条边和另一个子路径的场景下，点覆盖与边覆盖具有不同的测试需求
**主路径覆盖为了解决什么问题提出的？**
覆盖图中的环
**主路径覆盖在什么情况下不能包含边对覆盖？**
某个节点存在指向自己的边

37

---

<!-- Slide 38 -->

Questions (5)
**Sidetrip (侧访/经旁) 和detour (绕道) 的区别是什么？**
Sidetrip：游历岔道后回到岔道的起点
Detour：游历岔道后到岔道的终点
**除了直接游历之外，为什么还要定义sidetrip（侧访/经旁）和detour（绕道）方式的游历？**
弱化测试覆盖标准的要求，在直接游历不可行的情况下，可以以退而求其次的方式尽力而为的游历

38

---

<!-- Slide 39 -->

Data Flow Criteria
Definition (def) : A location where a value for a variable is stored into memory
Use : A location where a variable’s value is accessed
### Goal : Ensure that values are computed and used correctly
39
## def (n) or def (e) : The set of variables that are defined by node n or edge e
## use (n) or use (e) : The set of variables that are used by node n or edge e

---

<!-- Slide 40 -->

Data Flow Criteria

40
Defs: def (1) = {       }
def (5) = {       }
def (6) = {       }
Uses: use (5) = {       }
use (6) = {       }
### The values given in defs should reach at least one, some, or all possible uses
X
Z
Z
X
X
Fill in these sets

---

<!-- Slide 41 -->

DU Pairs and DU Paths
41
## DU pair : A pair of locations (li, lj) such that a variable v is defined at li and used at lj
## Def-clear : A path from li to lj is def-clear with respect to variable v if v is not given another value on any of the nodes or edges in the path
## Reach : If there is a def-clear path from li to lj with respect to v, the def of v at li reaches the use at lj
## du-path : A simple subpath that is def-clear with respect to v from a def of v to a use of v
## du (ni, nj, v) – the set of du-paths from ni to nj
## du (ni, v) – the set of du-paths that start at ni

---

<!-- Slide 42 -->

Example
3
4
5
6
7
11
1
2
10
8
9
Def(1)={subject, pattern}
Def(2)={NotFound, iSub,rtnIndex, isPat, subjectLen,patternLen}
use(2)={NotFound, subject, pattern}
use(3,4)=use(3,11)={isPat, iSub,patternLen,subjectLen}
use(4,10)=use(4,5)={iSub,subject,pattern}
def(5)={rtnIndex,isPat,iPat}, use(5)={iSub,}
use(6,10)=use(6,7)={ipat,patternLen}
use(7,8)=use(7.9)={subject,iSub,iPat,Pattern}
Def(9)=use(9)={iPat}
Def(8)={rtnIndex, isPat}
use(8)={NotFound}
Def(10)=use(10)={iSub}
use(11)={rtnIndex}
#### du{10, 10, iSub} = {[10,3,4,5,6,10], [10,3,4,5,6,7,8,10], [10,3,4,10]}






#### du(10, (3, 4), iSub)={[10,3,4]}
#### du(10, (3, 11), iSub)={[10,3,11]}
#### du(10, (4, 10), iSub)={[10,3,4,10]}
#### du(10, (4, 5), iSub)={[10,3,4,5]}
#### du(10, (7, 8), iSub)={[10,3,4,5,6,7,8]}
#### du(10, (7, 9), iSub)={[10,3,4,5,6,7,9]}
#### du(10, 5, iSub)={[10,3,4,5]}

---

<!-- Slide 43 -->

Example (cont.)
| Variable | Def | Use | DU-pair | Du-path |  |
| --- | --- | --- | --- | --- | --- |
| isub | 10 | (3, 4) | (10, (3, 4)) | [10,3,4] | du(10, (3, 4), iSub) |
|  |  | (3, 11) | (10, (3, 11)) | [10,3,11] | du(10, (3, 11), iSub) |
|  |  | (4, 10) | (10, (4, 10)) | [10,3,4,10] | du(10, (4, 10), iSub) |
|  |  | (4, 5) | (10, (4, 5)) | [10,3,4,5] | du(10, (4, 5), iSub) |
|  |  | 5 | (10, 5) | [10,3,4,5] | du(10, 5, iSub) |
|  |  | (7, 8) | (10, (7, 8)) | [10,3,4,5,6,7,8] | du(10, (7, 8), iSub) |
|  |  | (7, 9) | (10, (7, 9)) | [10,3,4,5,6,7,9] | du(10, (7, 9), iSub) |
|  |  | 10 | (10, 10) | {[10,3,4,5,6,10], [10,3,4,5,6,7,8,10], [10,3,4,10]} | du(10, 10, iSub) |
43
#### du(10,iSub)={[10,3,4],[10.3.11],[10,3,4,5],[10,3,4,5,6,7,8],[10,3,4,5,6,7,9],[10,3,4,5,6,10],[10,3,4,5,6,7,8,10],[10,3,4,10]}

---

<!-- Slide 44 -->

44
Touring DU-Paths
A test path p du-tours subpath d with respect to v if p tours d and the subpath taken is def-clear with respect to v

Sidetrips can be used, just as with previous touring

Three criteria
Use every def
Get to every use
Follow all du-paths

---

<!-- Slide 45 -->

45
Data Flow Test Criteria
### All-defs coverage (ADC) : For each set of du-paths S = du (n, v), TR contains at least one path d in S.
### All-uses coverage (AUC) : For each set of du-paths to uses S = du (ni, nj, v), TR contains at least one path d in S.
### All-du-paths coverage (ADUPC) : For each set S = du (ni, nj, v), TR contains every path d in S.
## Then we make sure that every def reaches all possible uses
## Finally, we cover all the paths between defs and uses
## First, we make sure every def reaches a use

---

<!-- Slide 46 -->

46
Data Flow Testing Example
### [ 1, 2, 4, 5 ]

### [ 1, 2, 4, 5 ]
### [ 1, 2, 4, 6 ]

### [ 1, 2, 4, 5 ]
### [ 1, 3, 4, 5 ]
### [ 1, 2, 4, 6 ]
### [ 1, 3, 4, 6 ]
Write down paths to satisfy ADC
Write down paths to satisfy AUC
Write down paths to satisfy ADUPC

---

<!-- Slide 47 -->

47
Graph Coverage Criteria        Subsumption

---

<!-- Slide 48 -->

Summary
Graphs are a very powerful abstraction for designing tests
The various criteria allow lots of cost / benefit tradeoffs
These two sections are entirely at the “design abstraction level” from chapter 3
Graphs appear in many situations in software
As discussed in the rest of chapter 3
48

---
