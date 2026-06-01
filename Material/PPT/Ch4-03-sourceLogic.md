## Slide 1

- **Chapter 4 Logic Coverage**
- **Logic Coverage for Source Code**
- **(8.3 Logic Coverage for Source Code)**

## Slide 2

- **本节课程目标**
- **掌握将逻辑覆盖应用于源代码的方法步骤；**
- **能提取被测代码中的条件/谓词；**
- **分析每一个条件的可达约束；**
- **分析可达约束中出现的内部变量并求解；**
- **根据内部变量的求解结果求解可达约束条件；**
- **根据覆盖需求求解测试用例；**
- **能将代码中包含多个子句的谓词重写成只包含单个子句的形式；**
- **明确谓词转换可能带来的问题。**
- **2**

## Slide 3

- **Logic Expressions from Source**
- **Predicates are derived from decision statements**
- **In programs, most predicates have less than four clauses**
  - Wise programmers actively strive to keep predicates simple
- **When a predicate only has one clause, COC, ACC, ICC, and CC all collapse to predicate coverage (PC)**
- **Applying logic criteria to program source is hard because of reachability and controllability:**
  - Reachability : Before applying the criteria on a predicate at a particular statement, we have to get to that statement
  - Controllability : We have to find input values that indirectly assign values to the variables in the predicates
  - Variables in the predicates that are not inputs to the program are called internal variables
- **Illustrated through an example in the following slides …**
- **3**

## Slide 4

- **Logic Coverage of Programs**
- **Steps:**
  - 提取被测代码中的条件(谓词)语句
  - 分析每一个条件的可达约束
  - 分析可达约束中出现的内部变量并求解
  - 根据内部变量的求解结果求解可达约束条件
  - 根据覆盖需求求解测试用例
- **Triangle Example**
  - The program of triangle

## Slide 5


## Slide 6

- **Derive predicates from program**
- **30- 42**
- **44-45**
- **(s1<=0||s2<=0||s3<=0)**
- **48- 49**
- **!(s1<=0||s2<=0||s3<=0)**
- **50**
- **51**
- **s1=s2**
- **s1!=s2**
- **52**
- **53**
- **s1=s3**
- **s1!=s3**
- **54**
- **55**
- **s2=s3**
- **s2!=s3**
- **59**
- **60-61**
- **62-63**
- **64**
- **triOut==0**
- **70**
- **triOut!=0**
- **71**
- **triOut>3**
- **72**
- **triOut==1&&s1+s2>s3**
- **73**
- **triOut<=3**
- **74**
- **triOut!=1||s1+s2<=s3**
- **80**
- **75**
- **76**
- **77**
- **78-79**
- **triOut==2&&s1+s3>s2**
- **triOut==3&&s2+s3>s1**
- **triOut!=2||s1+s3<=s2**
- **triOut!=3||s2+s3<=s1**
- **s1+s2<=s3|| s1+s3<=s2|| S2+s3<=s1**
- **s1+s2>s3&& s1+s3>s2&& S2+s3>s1**

## Slide 7

- **Reachability**
- **30- 42**
- **44-45**
- **(s1<=0||s2<=0||s3<=0)**
- **48- 49**
- **!(s1<=0||s2<=0||s3<=0)**
- **50**
- **51**
- **s1=s2**
- **s1!=s2**
- **52**
- **53**
- **s1=s3**
- **s1!=s3**
- **54**
- **55**
- **s2=s3**
- **s2!=s3**
- **59**
- **60-61**
- **62-63**
- **64**
- **triOut==0**
- **triOut!=0**
- **s1+s2<=s3|| s1+s3<=s2|| S2+s3<=s1**
- **s1+s2>s3&& s1+s3>s2&& S2+s3>s1**
- **到达42的路径约束条件为true**
- **..**
- **到达49的路径约束条件从初始节点到达49经历路径条件的合取为（true）&&（!(s1<=0||s2<=0||s3<=0)）= （!(s1<=0||s2<=0||s3<=0)）**
- **到达51的路径约束条件从初始节点到达51经历路径条件的合取为（!(s1<=0||s2<=0||s3<=0)）&&(s1=s2||s1!=s2) = （!(s1<=0||s2<=0||s3<=0)）**

## Slide 8

- **Reachability**
- **70**
- **triOut!=0**
- **71**
- **triOut>3**
- **72**
- **triOut==1&&s1+s2>s3**
- **73**
- **triOut<=3**
- **74**
- **triOut!=1||s1+s2<=s3**
- **80**
- **75**
- **76**
- **77**
- **78-79**
- **triOut==2&&s1+s3>s2**
- **triOut==3&&s2+s3>s1**
- **triOut!=2||s1+s3<=s2**
- **triOut!=3||s2+s3<=s1**
- **55**
- **!(s1<=0||s2<=0||s3<=0)**
- **到达74的路径约束条件从初始节点到达51经历路径条件的合取为 !(s1<=0||s2<=0||s3<=0)）&&(triOut!=0)&&(triOut<=3) &&(triOut!=1||s1+s2<=s3)**

## Slide 9

- **Control Internal Variable**
- **triOut**
  - Replace triOut with inputs variables,that is, s1,s2,s3
  - triOut ∈ [0,6]
  - triOut == 0: s1!=s2 && s2!=s3 && s1!=s3
  - triOut == 1: s1==s2 && s2!=s3 && s1!=s3
  - triOut == 2: s1!=s2 && s2!=s3 && s1==s3
  - triOut == 3: s1!=s2 && s2==s3 && s1!=s3  或者s1==s2 && s2!=s3 && s1==s3
  - triOut == 4: s1==s2 && s2==s3 && s1!=s3
  - triOut == 5: s1!=s2 && s2==s3 && s1==s3
  - triOut == 6: s1==s2 && s2==s3 && s1==s3

## Slide 10

- **Reduced Reachability**
- **Replace triOut with the resolved predict**
- **Example: statement74**
  - !(s1<=0||s2<=0||s3<=0))
  - && (triOut!=0) [!(s1!=s2 && s2!=s3 && s1!=s3 )]
  - && (triOut<=3)[(s1!=s2 && s2!=s3 && s1!=s3)||(s1==s2 && s2!=s3 && s1!=s3 )||(s1!=s2 && s2!=s3 && s1==s3 ) ]
  - && (triOut!=1||s1+s2<=s3)[!(s1==s2 && s2!=s3 && s1!=s3) ]

## Slide 11

- **Thermostat (pg 1 of 2)**
- **11**
- **1  // Jeff Offutt & Paul Ammann—September 2014**
- **2  // Programmable Thermostat**
- **6  import java.io.*;**
- **10  public class Thermostat**
- **11  {**
- **12     private int curTemp;                // Current temperature reading**
- **13     private int thresholdDiff;          // Temp difference until heater on**
- **14     private int timeSinceLastRun; // Time since heater stopped**
- **15     private int minLag;                   // How long I need to wait**
- **16     private boolean Override;        // Has user overridden the program**
- **17     private int overTemp;               // OverridingTemp**
- **18     private int runTime;                  // output of turnHeaterOn–how long to run**
- **19     private boolean heaterOn;       // output of turnHeaterOn – whether to run**
- **20     private Period period;               // morning, day, evening, or night**
- **21     private DayType day;               // week day or weekend day**
- **23     // Decide whether to turn the heater on, and for how long.**
- **24     public boolean turnHeaterOn (ProgrammedSettings pSet)**
- **25     {**

## Slide 12

- **Thermostat (pg 2 of 2)**
- **12**
- **26     int dTemp = pSet.getSetting (period, day);**
- **28     if (((curTemp < dTemp - thresholdDiff) ||**
- **29          (Override && curTemp < overTemp - thresholdDiff)) &&**
- **30          (timeSinceLastRun > minLag))**
- **31     {  // Turn on the heater**
- **32        // How long? Assume 1 minute per degree (Fahrenheit)**
- **33        int timeNeeded = curTemp - dTemp;**
- **34        if (Override)**
- **35           timeNeeded = curTemp - overTemp;**
- **36        setRunTime (timeNeeded);**
- **37        setHeaterOn (true);**
- **38        return (true);**
- **39     }**
- **40     else**
- **41     {**
- **42        setHeaterOn (false);**
- **43        return (false);**
- **44     }**
- **45  } // End turnHeaterOn**
- **The full class is in the book and on the book website.**

## Slide 13

- **13**
- **Two Thermostat Predicates**
- **28-30 : (((curTemp < dTemp - thresholdDiff) ||**
- **(Override && curTemp < overTemp - thresholdDiff)) &&**
- **timeSinceLastRun > minLag))**
- **34 : (Override)**
- **Simplify**
- **a : curTemp < dTemp - thresholdDiff**
- **b : Override**
- **c : curTemp < overTemp - thresholdDiff**
- **d : timeSinceLastRun > minLag)**
- **28-30 :  (a || (b && c)) && d**
- **34 :       b**

## Slide 14

- **14**
- **Reachability for Thermostat Predicates**
- **28-30 : True**
- **34 : (a || (b && c)) && d**
- **curTemp < dTemp - thresholdDiff**
- **Need to solve for the internal variable dTemp**
- **pSet.getSetting (period, day);**
  - setSetting (Period.MORNING, DayType.WEEKDAY, 69);
  - setPeriod (Period.MORNING);
  - setDay (DayType.WEEKDAY);

## Slide 15

- **15**
- **Predicate Coverage (true)**
- **(a || (b && c)) && d**
- **a: curTemp < dTemp – thresholdDiff : true**
- **b: Override : true**
- **c: curTemp < overTemp – thresholdDiff : true**
- **d: timeSinceLastRun > (minLag) : true**
- **a : true     b : true**
- **c : true     d : true**
- **thermo = new Thermostat();  // Needed object**
- **settings = new ProgrammedSettings();  // Needed object**
- **settings.setSetting (Period.MORNING, DayType.WEEKDAY, 69);  // dTemp**
- **thermo.setPeriod (Period.MORNING);  // dTemp**
- **thermo.setDay (DayType.WEEKDAY);  // dTemp**
- **thermo.setCurrentTemp (63);  // clause a**
- **thermo.setThresholdDiff (5);   // clause a**
- **thermo.setOverride (true);  // clause b**
- **thermo.setOverTemp (70);  // clause c**
- **thermo.setMinLag (10);  // clause d**
- **thermo.setTimeSinceLastRun (12);  // clause d**
- **assertTrue (thermo.turnHeaterOn (settings));   // Run test**

## Slide 16

- **Correlated Active Clause Coverage**
- **16**
- **Pa = ((a || (b && c)) && d)  ((a || (b && c)) && d)**
- **(T && d)  ((b && c) && d)**
- **((T || (b && c)) && d)  ((F || (b && c)) && d)**
- **!(b && c) && d**
- **( !b || !c ) && d**
- **Check with the logic coverage web app**
- **http://cs.gmu.edu:8080/offutt/coverage/LogicCoverage**
- **d  ((b && c) && d)**
- **(1 of 6)**
- **T  ((b && c) && T)**

## Slide 17

- **Correlated Active Clause Coverage**
- **17**
- **(a || (b && c)) && d**
- **a    b        c           d**
- **Pa :     T    t         f            t**
- **F    t         f            t**
- **Pb :     f     T        t            t**
- **f     F        t            t**
- **Pc :     f     t         T           t**
- **f     t         F           t**
- **Pd :     t     t         t           T**
- **t     t         t           F**
- **duplicates**
- **Six tests needed for CACC on Thermostat**
- **(2 of 6)**

## Slide 18

- **Correlated Active Clause Coverage**
- **18**
- **curTemp    dTemp     thresholdDiff**
- **a=t : curTemp < dTemp - thresholdDiff        63             69                 5**
- **a=f : !(curTemp < dTemp - thresholdDiff)     66             69                 5**
- **dTemp:**
- **settings.setSettings (Period.MORNING, DayType.WEEKDAY, 69)**
- **thermo.setPeriod (Period.MORNING);**
- **thermo.setDay (Daytype.WEEKDAY);**
- **Override**
- **b=t : Override      T**
- **b=f : !Override     F**
- **curTemp overTemp  thresholdDiff**
- **c=t : curTemp < overTemp - thresholdDiff            63            72               5**
- **c=f : !(curTemp < overTemp - thresholdDiff)         66            67               5**
- **timeSinceLastRun   minLag**
- **d=t : timeSinceLastRun > minLag                   12                 10**
- **d=f : !(timeSinceLastRun > minLag)                 8                  10**
- **These values then need to be placed into calls to turnHeaterOn() to satisfy the 6 tests for CACC**
- **(3 of 6)**

## Slide 19

- **Correlated Active Clause Coverage**
- **dTemp = 69 (period = MORNING, daytype = WEEKDAY)**
- **1. T t f t**
- **thermo.setCurrentTemp (63);**
- **thermo.setThresholdDiff (5);**
- **thermo.setOverride (true);**
- **thermo.setOverTemp (67); // c is false**
- **thermo.setMinLag (10);**
- **thermo.setTimeSinceLastRun (12);**
- **2. F t f t**
- **thermo.setCurrentTemp (66); // a is false**
- **thermo.setThresholdDiff (5);**
- **thermo.setOverride (true);**
- **thermo.setOverTemp (67); // c is false**
- **thermo.setMinLag (10);**
- **thermo.setTimeSinceLastRun (12);**
- **19**
- **(4 of 6)**

## Slide 20

- **Correlated Active Clause Coverage**
- **dTemp = 69 (period = MORNING, daytype = WEEKDAY)**
- **3. f T t t**
- **thermo.setCurrentTemp (66); // a is false**
- **thermo.setThresholdDiff (5);**
- **thermo.setOverride (true);**
- **thermo.setOverTemp (72); // to make c true**
- **thermo.setMinLag (10);**
- **thermo.setTimeSinceLastRun (12);**
- **4. F f T t**
- **thermo.setCurrentTemp (66); // a is false**
- **thermo.setThresholdDiff (5);**
- **thermo.setOverride (false); // b is false**
- **thermo.setOverTemp (72);**
- **thermo.setMinLag (10);**
- **thermo.setTimeSinceLastRun (12);**
- **20**
- **(5 of 6)**

## Slide 21

- **Correlated Active Clause Coverage**
- **dTemp = 69 (period = MORNING, daytype = WEEKDAY)**
- **5. t t t T**
- **thermo.setCurrentTemp (63);**
- **thermo.setThresholdDiff (5);**
- **thermo.setOverride (true);**
- **thermo.setOverTemp (72);**
- **thermo.setMinLag (10);**
- **thermo.setTimeSinceLastRun (12);**
- **6. t t t F**
- **thermo.setCurrentTemp (63);**
- **thermo.setThresholdDiff (5);**
- **thermo.setOverride (true);**
- **thermo.setOverTemp (72);**
- **thermo.setMinLag (10);**
- **thermo.setTimeSinceLastRun (8); // d is false**
- **21**
- **(6 of 6)**

## Slide 22

- **Program Transformation Issues**
- **22**
- **if ((a && b) || c)**
- **{**
- **S1;**
- **}**
- **else**
- **{**
- **S2;**
- **}**
- **if (a) {**
- **if (b)**
- **S1;**
- **else {**
- **if (c)**
- **S1;**
- **else**
- **S2;**
- **}**
- **}**
- **else {**
- **if (c)**
- **S1;**
- **else**
- **S2;**
- **}**
- **Transform (1) ?**

## Slide 23

- **Problems With Transformation 1**
- **We trade one problem for two problems :**
  - Maintenance becomes harder
  - Reachability becomes harder
- **23**
| a | b | c | (ab)c | CACC | PCT |
| --- | --- | --- | --- | --- | --- |
| T | T | T | T |  | X |
| T | T | F | T | X |  |
| T | F | T | T | X | X |
| T | F | F | F | X | X |
| F | T | T | T |  | X |
| F | T | F | F | X |  |
| F | F | T | T |  |  |
| F | F | F | F |  | X |

- **Consider coverage :**
  - CACC on the original requires four rows marked in the table
  - PC on the transformed version requires five different rows
- **PC on the transformed version has two problems :**
  - It does not satisfy CACC on the original
  - It is more expensive (more tests)

## Slide 24

- **Program Transformation Issue 2**
- **24**
- **if ((a && b) || c)**
- **{**
- **S1;**
- **}**
- **else**
- **{**
- **S2;**
- **}**
- **d = a && b;**
- **e = d || c;**
- **if (e)**
- **{**
- **S1;**
- **}**
- **else**
- **{**
- **S2;**
- **}**
- **Transform (2) ?**

## Slide 25

- **Problems With Transformation 2**
- **We move complexity into computations**
  - Logic criteria are not effective at testing computations
- **25**
| a | b | c | (ab)c | CACC | PCT |
| --- | --- | --- | --- | --- | --- |
| T | T | T | T |  | X |
| T | T | F | T | X |  |
| T | F | T | T | X |  |
| T | F | F | F | X |  |
| F | T | T | T |  |  |
| F | T | F | F | X |  |
| F | F | T | T |  |  |
| F | F | F | F |  | X |

- **Consider coverage :**
  - CACC on the original requires four rows marked in the table
  - PC on the transformed version requires only two
- **PC on the transformed version becomes equivalent to clause coverage on the original**
  - Not an effective testing technique

## Slide 26

- **Transforming Does Not Work**
- **26**
- **Logic coverage criteria exist to help us make better software**
- **Circumventing the criteria is unsafe**

## Slide 27

- **Side Effects in Predicates**
- **Side effects occur when a value is changed while evaluating a predicate**
  - A clause appears twice in the same predicate
  - A clause in between changes the value of the clause that appears twice
- **Example :**
  - Evaluation : Runtime system checks A, then B, if B is false, check A again
  - But now A has a different value!
  - How do we write a test that has two different values for the same predicate?
- **No clear answers to this controllability problem**
- **27**
- **A && (B || A)**
- **B is : changeVar (A)**
- **We suggest a social solution : Go ask the programmer**

## Slide 28

- **Summary : Logic Coverage for Source Code**
- **Predicates appear in decision statements (if, while, for, etc.)**
- **Most predicates have less than four clauses**
  - But some programs have a few predicates with many clauses
- **The hard part of applying logic criteria to source is usually resolving the internal variables**
  - Sometimes setting variables requires calling other methods
- **Non-local variables (class, global, etc.) are also input variables if they are used**
- **If an input variable is changed within a method, it is treated as an internal variable thereafter**
- **Avoid transformations that hide predicate structure**
- **28**
