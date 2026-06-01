<!-- Slide 1 -->

Chapter 3 Graph Coverage
## 3.4 Graph Coverage for Design Elements

---

<!-- Slide 2 -->

本节课程目标
明确设计元素图覆盖的思路，包括调用图、包含类的实例化对象的调用图；
明确last-def集合、first-use集合、couplingdu-path的含义，能写出上述集合中的元素，couplingdu-path；
明确覆盖标准All-Coupling-Def覆盖、All-Coupling-Use覆盖、All-Coupling-du-paths覆盖的含义，写出上述覆盖标准的测试需求及满足对应测试需求的测试路径。
2

---

<!-- Slide 3 -->

3
OO Software and Designs
Emphasis on modularity and reuse puts complexity in the design connections

Testing design relationships is more important than before

Graphs are based on the connections among the software components
Connections are dependency relations, also called couplings

---

<!-- Slide 4 -->

4
Call Graph
The most common graph for structural design testing
Nodes : Units (in Java – methods)
Edges : Calls to units
### Node coverage : call every unit at least once (method coverage)
### Edge coverage : execute every call at least once (call coverage)

---

<!-- Slide 5 -->

5
Call Graphs on Classes
Node and edge coverage of class call graphs often do not work very well
Individual methods might not call each other at all!
Class stack
public void push (Object o)
public Object pop ( )
public boolean isEmpty (Object o)
## Other types of testing are needed – do not use graph criteria

---

<!-- Slide 6 -->

6
Inheritance & Polymorphism
Caution : Ideas are preliminary and not widely used
### Classes are not executable, so this graph is not directly testable

### We need objects
### What is coverage on this graph ?

---

<!-- Slide 7 -->

7
Coverage on Inheritance Graph
Create an object for each class ?
This seems weak because there is no execution
### Create an object for each class and apply call coverage?
### OO Call Coverage : TR contains each reachable node in the call graph of an object instantiated for each class in the class hierarchy.
### OO Object Call Coverage : TR contains each reachable node in the call graph of every object instantiated for each class in the class hierarchy.
## Data flow is probably more appropriate …

---

<!-- Slide 8 -->

8
Data Flow at the Design Level
Data flow couplings among units and classes are more complicated than control flow couplings
When values are passed, they “change names”
Many different ways to share data
Finding defs and uses can be difficult – finding which uses a def can reach is very difficult
When software gets complicated … testers should get interested
That’s where the faults are!

---

<!-- Slide 9 -->

Preliminary Definitions
Caller : A unit that invokes another unit
Callee : The unit that is called
Callsite : Statement or node where the call appears
Actual parameter : Variable in the caller
Formal parameter : Variable in the callee
9

---

<!-- Slide 10 -->

10
Example Call Site
### A  B (x) end A
### B (Y) end B
Caller
Actual Parameter
Formal Parameter
Callee
Applying data flow criteria to def-use pairs between units is too expensive
Too many possibilities
But this is integration testing, and we really only care about the interface …

---

<!-- Slide 11 -->

11
Inter-procedural DU Pairs
If we focus on the interface, then we just need to consider the last definitions of variables before calls and returns and first uses inside units and after calls
Last-def : The set of nodes that define a variable x and has a def-clear path from the node through a callsite to a use in the other unit
Can be from caller to callee (parameter or shared variable) or from callee to caller as a return value
First-use : The set of nodes that have uses of a variable y and for which there is a def-clear and use-clear path from the callsite to the nodes

---

<!-- Slide 12 -->

12
## Inter-procedural DU Pairs Example

F
X = 14y = G (x) print (y)

G (a)
print (a)b = 42 return (b)
### Caller
### Callee

---

<!-- Slide 13 -->

13
## Inter-procedural DU Pairs Example

### Last Defs2, 3
### First Uses11, 12
### DU Pairs
### (A,  x, 2)—(B, y, 11)
### (A,  x, 2)—(B, y, 12)
### (A,  x, 3)—(B, y, 11)
### (A,  x, 3)—(B, y, 12)

---

<!-- Slide 14 -->

Data Flow at the Design Level
**A coupling du-path is a path from a last-def to a first-use**
**All-Coupling-Def coverage:  every last def to at least one first use**
**All-Coupling-use Coverage: every last def to every first use**
**All-Coupling-du-Paths Coverage: every simple path from every last def to every first use**

---

<!-- Slide 15 -->

15
#### 1 // Program to compute the quadratic root for two numbers2 import java.lang.Math;3 4 class Quadratic5 {6  private static float Root1, Root2;78  public static void main (String[] argv)9  {10     int X, Y, Z;11     boolean ok;12     int controlFlag = Integer.parseInt (argv[0]);13     if (controlFlag == 1)14     {15          X = Integer.parseInt (argv[1]);16          Y = Integer.parseInt (argv[2]);17          Z = Integer.parseInt (argv[3]);18      }19     else20     {
#### 21           X = 10;22           Y = 9;23           Z = 12;24      }
#### 25              ok = Root (X, Y, Z);26              if (ok)27                System.out.println28                      (“Quadratic: ” + Root1 + Root2);29              else30                  System.out.println (“No Solution.”);31    }3233 // Three positive integers, finds quadratic root34    private static boolean Root (int A, int B, int C)35    {36        double D;37        boolean Result;38        D = (double) (B*B) -  (double) (4.0*A*C );39        if (D < 0.0)40        {41            Result = false;
#### 42            return (Result);43        }44        Root1 = (double) ((-B + Math.sqrt(D))/(2.0*A));45        Root2 = (double) ((-B – Math.sqrt(D))/(2.0*A));46        Result = true;47        return (Result);48    } // End method Root49 } // End class Quadratic
# Example – Quadratic

---

<!-- Slide 16 -->

16
#### 1 // Program to compute the quadratic root for two numbers2 import java.lang.Math;3 4 class Quadratic5 {6  private static float Root1, Root2;78  public static void main (String[] argv)9  {10      int X, Y, Z;11     boolean ok;12     int controlFlag = Integer.parseInt (argv [0]);13     if (controlFlag == 1)14     {15          X = Integer.parseInt (argv [1]);16          Y = Integer.parseInt (argv [2]);17          Z = Integer.parseInt (argv [3]);18      }19     else20     {
#### 21           X = 10;22           Y = 9;23           Z = 12;24      }

---

<!-- Slide 17 -->

17
#### 25              ok = Root (X, Y, Z);26              if (ok)27                System.out.println28                      (“Quadratic: ” + Root1 + Root2);29              else30                  System.out.println (“No Solution.”);31    }3233    // Three positive integers, finds the quadratic root34    private static boolean Root (int A, int B, int C)35    {36        double D;37        boolean Result;38        D = (double) (B*B) - (double) (4.0*A*C);39        if (D < 0.0)40        {41            Result = false;
#### 42            return (Result);43        }44        Root1 = (double) ((-B + Math.sqrt (D)) / (2.0*A));45        Root2 = (double) ((-B – Math.sqrt (D)) / (2.0*A));46        Result = true;47        return (Result);48    } / /End method Root49 } // End class Quadratic

---

<!-- Slide 18 -->

18
Quadratic – Coupling DU-pairs
Pairs of locations: method name, variable name, statement
(main (), X, 15) – (Root (), A, 38)
(main (), Y, 16) – (Root (), B, 38)
(main (), Z, 17) – (Root (), C, 38)
(main (), X, 21) – (Root (), A, 38)
(main (), Y, 22) – (Root (), B, 38)
(main (), Z, 23) – (Root (), C, 38)
(Root (), Root1, 44) – (main (), Root1, 28)
(Root (), Root2, 45) – (main (), Root2, 28)
(Root (), Result, 41) – ( main (),   ok,   26 )
(Root (), Result, 46) – ( main (),   ok,   26 )

---

<!-- Slide 19 -->

19
Coupling Data Flow Notes
Only variables that are used or defined in the callee are considered.

## Implicit initializations of class and global variables

## Transitive DU-pairs are too expensive to handle
### A calls B, B calls C, and there is a variable defined in A and used in C

## Arrays : a reference to one element is considered to be a reference to all elements

---

<!-- Slide 20 -->

Summary—What Works?
Call graphs are common and very useful ways to design integration tests
Inter-procedural data flow is relatively easy to compute and results in effective integration tests
The ideas for OO software and web applications are preliminary and have not been used much in practice
20

---

<!-- Slide 21 -->

From Structure to Semantics: Evolution of Design Testing
Static Structure→ Call Graph, Node/Edge Coverage
Runtime Behavior→ Dynamic Call Graph, Execution Trace
Interface Interaction→ Service/API Coupling
Semantic Data Flow→ Taint Analysis, Contract Validation

Design testing evolves from “structure coverage” to “interaction and semantics validation”.
21

---

<!-- Slide 22 -->

From Static Call Graph to Runtime Call Graph
传统Static Call Graph无法准确处理：
Polymorphism
Reflection
Dynamic dispatch
现代方法
Dynamic Call Graph（Execution Trace）
Hybrid Approach（Static + Dynamic）
工程实践
Distributed Tracing（Jaeger / Zipkin）
自动生成跨服务调用链
Runtime coupling reveals what actually happens, not just what may happen.
22

---

<!-- Slide 23 -->

From Coupling DU to Data Flow Propagation
Last-def / First-use；Coupling DU-path；All-Coupling-Def / Use / Paths
计算复杂（尤其跨过程）
Transitive DU难以处理
现代升级
API-level Data Flow
Taint Analysis（污点传播）
Coupling DU ≈ Inter-procedural / Inter-service Taint Flow
核心区别
DU：枚举路径（path-based）
Taint：跟踪传播（propagation-based）
23

---

<!-- Slide 24 -->

Service-level / API coupling
| 传统概念 | 现代对应 |
| --- | --- |
| Caller / Callee | Service A / Service B |
| Actual Parameter | JSON / Protobuf payload |
| Formal Parameter | API Schema / Contract |
| Return value | HTTP response / Event |
| Call Graph | Service Dependency Graph |
24
### Service Dependency Graph (SDG)：
### 节点为服务，边为API调用（REST/gRPC）、异步消息（Kafka/RabbitMQ）。
### 在微服务架构中，接口耦合测试已成为系统正确性的核心。
### 一个接口破坏可能引发级联故障（cascade failure）

---

<!-- Slide 25 -->

From Coverage to Effectiveness
传统Node / Edge / DU Coverage关注路径是否被执行
现代
Fuzzing（尤其数据流引导）
Mutation Testing
Coverage measures “where we go”, but modern testing focuses on “what we break”.
实践趋势
Data-flow-guided fuzzing
Interface / API testing
Contract validation
25

---

<!-- Slide 26 -->

Summary
Graph coverage is effective for monolithic systems, but limited for modern architectures
Modern testing focuses on:
Runtime behavior
Cross-interface data flow
Service-level interactions
Coupling-based testing evolves toward:
Dynamic
Semantic
Scalable
26

---
