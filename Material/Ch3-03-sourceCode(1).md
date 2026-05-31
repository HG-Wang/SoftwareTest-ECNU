<!-- Slide 1 -->

Chapter 3 Graph Coverage
## 3.3 Graph Coverage for Source Code

---

<!-- Slide 2 -->

本节课程目标
掌握典型代码结构对应的控制流图，画出给定代码对应的控制流图，对控制流图进行数据流标记
应用图覆盖标准对控制流图（包括带数据流标记的）进行分析，设计测试用例。
2

---

<!-- Slide 3 -->

3
Overview
A common application of graph criteria is to program source
Graph : Usually the control flow graph (CFG)
Node coverage : Execute every statement
Edge coverage : Execute every branch
Loops : Looping structures such as for loops, while loops, etc.
Data flow coverage : Augment the CFG
defs are statements that assign values to variables
uses are statements that use variables

---

<!-- Slide 4 -->

4
Control Flow Graphs
A CFG models all executions of a method by describing control structures
Nodes : Statements or sequences of statements (basic blocks)
Edges : Transfers of control
Basic Block : A sequence of statements such that if the first statement is executed, all statements will be (no branches)
Loops require “extra” nodes to be added
Nodes that do not represent statements or basic blocks
CFGs are sometimes annotated with extra information
branch predicates
defs
uses
Rules for translating statements into graphs …

---

<!-- Slide 5 -->

5
CFG : The if Statement
if (x < y)
{
y = 0;
x = x + 1;
}
else
{
x = y;
}
if (x < y)
{
y = 0;
x = x + 1;
}
Draw the graph. Label the edges with the Java statements.
Draw the graph and label the edges.

---

<!-- Slide 6 -->

6
CFG : The if-Return Statement
if (x < y)
{
return;
}
print (x);
return;
Draw the graph and label the edges.

---

<!-- Slide 7 -->

7
CFG : while and for Loops
x = 0;
while (x < y)
{
y = f (x, y);
x = x + 1;
}
for (x = 0; x < y; x++)
{
y = f (x, y);
}
#### x = x + 1
implicitly increments loop
Draw the graph and label the edges.
Draw the graph and label the edges.

---

<!-- Slide 8 -->

8
CFG : do Loop, break and continue
x = 0;
do
{
y = f (x, y);
x = x + 1;
} while (x < y);
println (y)


#### x = 0

3

2

#### x >= y
#### x < y
#### y = f (x, y)
#### x = x+1


1

#### x = 0
#### x = x + 1

#### break
#### y < 0







#### y =f(x,y)
#### y == 0
#### y = y*2
#### continue


x = 0;
while (x < y)
{
y = f (x, y);
if (y == 0)
{
break;
} else if (y < 0)
{
y = y*2;
continue;
}
x = x + 1;
}
print (y);
#### print (y)
Draw the graph and label the edges.
Draw the graph and label the edges.

---

<!-- Slide 9 -->

9
CFG : The case (switch) Structure
read ( c) ;
switch ( c )
{
case ‘N’:
z = 25;
case ‘Y’:
x = 50;
break;
default:
x = 0;
break;
}
print (x);
Draw the graph and label the edges.
Cases without breaks fall through to the next case


---

<!-- Slide 10 -->

10
CFG : Exceptions (try-catch)
1

#### s = br.readLine()
8




try
{
s = br.readLine();
if (s.length() > 96)
throw new Exception
(“too long”);
if (s.length() == 0)
throw new Exception
(“too short”);
} (catch IOException e) {
e.printStackTrace();
} (catch Exception e) {
e.getMessage();
}
return (s);
2
3
4
5
6
7






#### IOException
#### e.printStackTrace()
#### length > 96
#### length <= 96
#### return (s)
#### throw
#### length == 0
#### length != 0
#### throw
#### e.getMessage()
Draw the graph and label the edges.

---

<!-- Slide 11 -->

© Ammann & Offutt
Example Control Flow – Stats

#### public static void computeStats (int [ ] numbers)
#### {
#### int length = numbers.length;
#### double med, var, sd, mean, sum, varsum;

#### sum = 0;
#### for (int i = 0; i < length; i++)
#### {
#### sum += numbers [ i ];
#### }
#### med   = numbers [ length / 2];
#### mean = sum / (double) length;

#### varsum = 0;
#### for (int i = 0; i < length; i++)
#### {
#### varsum = varsum  + ((numbers [ I ] - mean) * (numbers [ I ] - mean));
#### }
#### var = varsum / ( length - 1.0 );
#### sd  = Math.sqrt ( var );

#### System.out.println ("length:                   " + length);
#### System.out.println ("mean:                    " + mean);
#### System.out.println ("median:                 " + med);
#### System.out.println ("variance:                " + var);
#### System.out.println ("standard deviation: " + sd);
#### }
11
Draw the graph and label the edges.

---

<!-- Slide 12 -->

© Ammann & Offutt
Control Flow Graph for Stats

#### public static void computeStats (int [ ] numbers)
#### {
#### int length = numbers.length;
#### double med, var, sd, mean, sum, varsum;

#### sum = 0;
#### for (int i = 0; i < length; i++)
#### {
#### sum += numbers [ i ];
#### }
#### med   = numbers [ length / 2];
#### mean = sum / (double) length;

#### varsum = 0;
#### for (int i = 0; i < length; i++)
#### {
#### varsum = varsum  + ((numbers [ I ] - mean) * (numbers [ I ] - mean));
#### }
#### var = varsum / ( length - 1.0 );
#### sd  = Math.sqrt ( var );

#### System.out.println ("length:                   " + length);
#### System.out.println ("mean:                    " + mean);
#### System.out.println ("median:                 " + med);
#### System.out.println ("variance:                " + var);
#### System.out.println ("standard deviation: " + sd);
#### }
i = 0
#### i++
i = 0
i++
12

---

<!-- Slide 13 -->

## Control Flow TRs and Test Paths—EC
13
### A. [ 1, 2 ]
### B. [ 2, 3 ]
### C. [ 3, 4 ]
### D. [ 3, 5 ]
### E. [ 4, 3 ]
### F. [ 5, 6 ]
### G. [ 6, 7 ]
### H. [ 6, 8 ]
### I. [ 7, 6 ]
### [ 1, 2, 3, 4, 3, 5, 6, 7, 6, 8 ]
Write down the TRs for EC.
Write down test paths that tour all edges.

---

<!-- Slide 14 -->

## Control Flow TRs and Test Paths—EPC
14
### A. [ 1, 2, 3 ]
### B. [ 2, 3, 4 ]
### C. [ 2, 3, 5 ]
### D. [ 3, 4, 3 ]
### E. [ 3, 5, 6 ]
### F. [ 4, 3, 5 ]
### G. [ 5, 6, 7 ]
### H. [ 5, 6, 8 ]
### I. [ 6, 7, 6 ]
### J. [ 7, 6, 8 ]
### K. [ 4, 3, 4 ]
### L. [ 7, 6, 7 ]
### i. [ 1, 2, 3, 4, 3, 5, 6, 7, 6, 8 ]
### ii. [ 1, 2, 3, 5, 6, 8 ]
### iii. [ 1, 2, 3, 4, 3, 4, 3, 5, 6, 7,
### 6, 7, 6, 8 ]

TP iii makes TP i redundant.  A minimal set of TPs is cheaper.
Write down TRs for EPC.
Write down test paths that tour all edge pairs.

---

<!-- Slide 15 -->

## Control Flow TRs and Test Paths—PPC
15
### A. [ 3, 4, 3 ]
### B. [ 4, 3, 4 ]
### C. [ 7, 6, 7 ]
### D. [ 7, 6, 8 ]
### E. [ 6, 7, 6 ]
### F. [ 1, 2, 3, 4 ]
### G. [ 4, 3, 5, 6, 7 ]
### H. [ 4, 3, 5, 6, 8 ]
### I. [ 1, 2, 3, 5, 6, 7 ]
### J. [ 1, 2, 3, 5, 6, 8 ]
### i.  [ 1, 2, 3, 4, 3, 5, 6, 7, 6, 8 ]
### ii. [ 1, 2, 3, 4, 3, 4, 3,
### 5, 6, 7, 6, 7, 6, 8 ]
### iii. [ 1, 2, 3, 4, 3, 5, 6, 8 ]
### iv. [ 1, 2, 3, 5, 6, 7, 6, 8 ]
### v.  [ 1, 2, 3, 5, 6, 8 ]

TP ii makes
TP i redundant.
Write down TRs for PPC.
Write down test paths that tour all prime paths.

---

<!-- Slide 16 -->

16
Data Flow Coverage for Source
def : a location where a value is stored into memory
x appears on the left side of an assignment (x = 44;)
x is an actual parameter in a call and the method changes its value
x is a formal parameter of a method (implicit def when method starts)
x is an input to a program
use : a location where variable’s value is accessed
x appears on the right side of an assignment
x appears in a conditional test
x is an actual parameter to a method
x is an output of the program
x is an output of a method in a return statement
If a def and a use appear on the same node, then it is only a DU-pair if the def occurs after the use and the node is in a loop

---

<!-- Slide 17 -->

17
Example Data Flow – Stats

#### public static void computeStats (int [ ] numbers)
#### {
#### int length = numbers.length;
#### double med, var, sd, mean, sum, varsum;

#### sum = 0.0;
#### for (int i = 0; i < length; i++)
#### {
#### sum += numbers [ i ];
#### }
#### med   = numbers [ length / 2 ];
#### mean = sum / (double) length;

#### varsum = 0.0;
#### for (int i = 0; i < length; i++)
#### {
#### varsum = varsum  + ((numbers [ i ] - mean) * (numbers [ i ] - mean));
#### }
#### var = varsum / ( length - 1 );
#### sd  = Math.sqrt ( var );

#### System.out.println ("length:                   " + length);
#### System.out.println ("mean:                    " + mean);
#### System.out.println ("median:                 " + med);
#### System.out.println ("variance:                " + var);
#### System.out.println ("standard deviation: " + sd);
#### }
#### 10
#### 11
#### 12
#### 13
#### 14
#### 15
#### 16
#### 17
#### 18
#### 19
#### 20
#### 21
#### 22
#### 23
#### 24
#### 25
#### 26
#### 27
#### 28
#### 29
#### 30
#### 31
#### 3233343536

---

<!-- Slide 18 -->

18
Control Flow Graph for Stats
#### ( numbers )
#### sum = 0
#### length = numbers.length
#### i = 0
#### sum += numbers [ i ]
#### i++
#### med = numbers [ length / 2 ]
#### mean = sum / (double) length
#### varsum = 0
#### i = 0
#### varsum = …
#### i++
#### var = varsum / ( length - 1.0 )
#### sd  = Math.sqrt ( var )
#### print (length, mean, med, var, sd)
Annotate with the statements …

---

<!-- Slide 19 -->

19
CFG for Stats – With Defs & Uses
#### def (1) = { numbers, sum, length }
#### def (2) = { i }
#### def (5) = { med, mean, varsum, i }
#### use (5) = { numbers, length, sum }
#### def (8) = { var, sd }
#### use (8) = { varsum, length, mean,
#### med, var, sd }
#### def (4) = { sum, i }
#### use (4) = { sum, numbers, i }
#### def (7) = { varsum, i }
#### use (7) = { varsum, numbers, i, mean }
#### use (1) = { numbers}
Turn the annotations into def and use sets …

---

<!-- Slide 20 -->

20
Defs and Uses Tables for Stats
| Node | Def | Use |
| --- | --- | --- |
| 1 | { numbers, sum, length } | { numbers } |
| 2 | { i } |  |
| 3 |  |  |
| 4 | { sum, i } | { numbers, i, sum } |
| 5 | { med, mean, varsum, i } | { numbers, length, sum } |
| 6 |  |  |
| 7 | { varsum, i } | { varsum, numbers, i, mean } |
| 8 | { var, sd } | { varsum, length, var, mean, med, var, sd } |
| Edge | Use |
| --- | --- |
| (1, 2) |  |
| (2, 3) |  |
| (3, 4) | { i, length } |
| (4, 3) |  |
| (3, 5) | { i, length } |
| (5, 6) |  |
| (6, 7) | { i, length } |
| (7, 6) |  |
| (6, 8) | { i, length } |

---

<!-- Slide 21 -->

DU Pairs for Stats
21
| variable | DU Pairs |
| --- | --- |
| numbers | (1, 1), (1, 4) (1, 5) (1, 7) |
| length | (1, 5) (1, 8) (1, (3,4)) (1, (3,5)) (1, (6,7)) (1, (6,8)) |
| med | (5, 8) |
| var | (8, 8) |
| sd | (8, 8) |
| mean | (5, 7) (5, 8) |
| sum | (1, 4) (1, 5) (4, 4) (4, 5) |
| varsum | (5, 7) (5, 8) (7, 7) (7, 8) |
| i | (2, 4) (2, (3,4)) (2, (3,5)) (2, 7) (2, (6,7)) (2, (6,8))
(4, 4) (4, (3,4)) (4, (3,5)) (4, 7) (4, (6,7)) (4, (6,8))
(5, 7) (5, (6,7)) (5, (6,8))
(7, 7) (7, (6,7)) (7, (6,8)) |
No path through graph from nodes 5 and 7 to 4 or 3


---

<!-- Slide 22 -->

22
DU Paths for Stats
| variable | DU Pairs | DU Paths |
| --- | --- | --- |
| numbers | (1, 4)
(1, 5)
(1, 7) | [ 1, 2, 3, 4 ]
[ 1, 2, 3, 5 ]
[ 1, 2, 3, 5, 6, 7 ] |
| length | (1, 5)
(1, 8)
(1, (3,4))
(1, (3,5))
(1, (6,7))
(1, (6,8)) | [ 1, 2, 3, 5 ]
[ 1, 2, 3, 5, 6, 8 ]
[ 1, 2, 3, 4 ]
[ 1, 2, 3, 5 ]
[ 1, 2, 3, 5, 6, 7 ]
[ 1, 2, 3, 5, 6, 8 ] |
| med | (5, 8) | [ 5, 6, 8 ] |
| var | (8, 8) | No path needed |
| sd | (8, 8) | No path needed |
| sum | (1, 4)
(1, 5)
(4, 4)
(4, 5) | [ 1, 2, 3, 4 ]
[ 1, 2, 3, 5 ]
[ 4, 3, 4 ]
[ 4, 3, 5 ] |
| variable | DU Pairs | DU Paths |
| --- | --- | --- |
| mean | (5, 7)
(5, 8) | [ 5, 6, 7 ]
[ 5, 6, 8 ] |
| varsum | (5, 7)
(5, 8)
(7, 7)
(7, 8) | [ 5, 6, 7 ]
[ 5, 6, 8 ]
[ 7, 6, 7 ]
[ 7, 6, 8 ] |
| i | (2, 4)
(2, (3,4))
(2, (3,5))
(4, 4)
(4, (3,4))
(4, (3,5))
(5, 7)
(5, (6,7))
(5, (6,8))
(7, 7)
(7, (6,7))
(7, (6,8)) | [ 2, 3, 4 ]
[ 2, 3, 4 ]
[ 2, 3, 5 ]
[ 4, 3, 4 ]
[ 4, 3, 4 ]
[ 4, 3, 5 ]
[ 5, 6, 7 ]
[ 5, 6, 7 ]
[ 5, 6, 8 ]
[ 7, 6, 7 ]
[ 7, 6, 7 ]
[ 7, 6, 8 ] |

---

<!-- Slide 23 -->

23
DU Paths for Stats—No Duplicates
There are 38 DU paths for Stats, but only 12 unique

---

<!-- Slide 24 -->

24
Test Cases and Test Paths
A fault was
found

---

<!-- Slide 25 -->

Summary
Applying the graph test criteria to control flow graphs is relatively straightforward
Most of the developmental research work was done with CFGs

A few subtle decisions must be made to translate control structures into the graph

Some tools will assign each statement to a unique node
These slides and the book uses basic blocks
Coverage is the same, although the bookkeeping will differ
25

---

<!-- Slide 26 -->

**趋势1：CFG → SSA → Dataflow Graph（显式化）**
传统：CFG + def-use
现在：
SSA （Static Single Assignment，静态单赋值形式）直接编码 def-use
Dataflow IR（如 MLIR）直接消除控制依赖
**本质：把数据流从“分析结果”变成“程序表示本身”**

26
#### 在普通程序中，一个变量可以被多次赋值，例如：
#### x = 1;
#### x = x + 2;
#### 在 SSA 中，会被改写为：
#### x1 = 1;
#### x2 = x1 + 2;
#### 每个变量版本（x1, x2）只定义一次
#### 使用关系天然形成 def-use 链

---

<!-- Slide 27 -->

**趋势2：数据流分析 + 约束求解（Datalog / SMT）**
代表：
Rust Polonius （Datalog）
P4Testgen（SMT-like concolic）
方法：
def-use → 转换为逻辑规则
优势：
可扩展
易表达复杂语义
27

---

<!-- Slide 28 -->

**趋势3：数据流分析 + 安全语义（Taint / IFC）**
从：
“变量是否被定义使用”
到：
“信息是否非法传播”
在 P4（P4BID 2025）、Solidity（Slither）、eBPF中非常明显
28

---

<!-- Slide 29 -->

**趋势4：路径敏感（Path-sensitive）数据流分析**
传统：
flow-sensitive
新：
path-sensitive（结合 symbolic execution）
代表：
P4Testgen
KLEE-like systems
29

---

<!-- Slide 30 -->

**趋势5：数据流分析 + 在线学习 / 动态分析（前沿）**
新方向：
trace-based dataflow inference
runtime taint tracking
在网络领域：
用于 telemetry + anomaly detection


30

---
