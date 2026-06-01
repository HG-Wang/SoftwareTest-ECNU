## Slide 1

- **Chapter 4 Logic Coverage**
- **8.5 Logic Coverage of FSMs**

## Slide 2

- **本节课程目标**
- **掌握将逻辑覆盖应用到有限状态机（FSM）的思路和方法；**
- **结合测试需求分析其中可能存在的不可行测试需求、意外跳转等问题；**
- **明确测试自动化涉及的可达性和可控制性（映射）问题。**
- **2**

## Slide 3

- **Covering Finite State Machines**
- **FSMs are graphs**
  - Nodes represent state
  - Edges represent transitions among states
- **Transitions often have logical expressions as guards or triggers**
- **As we said :**
- **3**
- **Find a logical expression and cover it**

## Slide 4

- **4**
- **Example—Subway Train**
- **All Doors**
- **Open**
- **Left Doors**
- **Open**
- **Right Doors**
- **Open**
- **All Doors**
- **Closed**
- **trainSpeed = 0  platform=right  (location = inStation  (emergencyStop  overrideOpen  location = inTunnel))**
- **trainSpeed = 0  platform=left  (location = inStation  (emergencyStop  overrideOpen  location = inTunnel))**
- **secondPlatform = right**
- **secondPlatform= left**
- **¬ emergencyStop  ¬ overrideOpen  doorsClear  closeDoorPressed**
- **(applies to all three transitions)**

## Slide 5

- **5**
- **Determination of the Predicate**
- **trainSpeed = 0  platform=left  (location = inStation  (emergencyStop  overrideOpen  location = inTunnel))**
- **Find the truth assignments that let the all six clauses determine the value of the predicate.**
- **That is, solve for PtrainSpeed, then Pplatform=left, etc.**
- **a  b  (c  (d  e  f))**

## Slide 6

- **6**
- **Determination of the Predicate**
- **trainSpeed = 0  platform=left  (location = inStation  (emergencyStop  overrideOpen  location = inTunnel))**
- **PtrainSpeed = 0 : platform = left  (location = inStation  (emergencyStop **
- **overrideOpen  location = inTunnel))**
- **Pplatform = left : trainSpeed = 0  (location = inStation  (emergencyStop **
- **overrideOpen  location = inTunnel))**
- **Plocation = inStation : trainSpeed = 0  platform = left  (¬ emergencyStop **
- **¬ overrideOpen  ¬ location = inTunnel)**
- **PemergencyStop : trainSpeed = 0  platform = left  (¬ location = inStation **
- **overrideOpen  location = inTunnel)**
- **PoverrideOpen : trainSpeed = 0  platform = left  (¬ location = inStation **
- **emergencyStop  location = inTunnel)**
- **Plocation = inTunnel : trainSpeed = 0  platform = left  (¬ location = inStation **
- **emergencyStop  overrideOpen)**
- **Solution for PtrainSpeed …**
- **Solution for Pplatform …**
- **Solution for PinStation …**
- **Solution for PemergencyStop …**
- **Solution for PoverrideOpen …**
- **Solution for Plocation …**

## Slide 7

- **Test Truth Assignments (CACC)**
- **7**
- **trainSpeed = 0  platform=left  (location = inStation  (emergencyStop  overrideOpen  location = inTunnel))**
| Major Clause | Speed=0 | platform=left | inStation | emergStop | overrideOpen | inTunnel |
| --- | --- | --- | --- | --- | --- | --- |
| trainSpeed = 0 | T | t | t | t | t | t |
| trainSpeed != 0 | F | t | t | t | t | t |
| platform = left |  |  |  |  |  |  |
| platform != left |  |  |  |  |  |  |
| inStation |  |  |  |  |  |  |
| ¬ inStation |  |  |  |  |  |  |
| emergencyStop |  |  |  |  |  |  |
| ¬ emergStop |  |  |  |  |  |  |
| overrideOpen |  |  |  |  |  |  |
| ¬ overrideOpen |  |  |  |  |  |  |
| inTunnel |  |  |  |  |  |  |
| ¬ inTunnel |  |  |  |  |  |  |

- **Fill in the remaining truth assignments based on the expressions computed for the previous slide**
- **One of these must be true**

## Slide 8

- **Test Truth Assignments (CACC)**
- **8**
- **trainSpeed = 0  platform=left  (location = inStation  (emergencyStop  overrideOpen  location = inTunnel))**
| Major Clause | Speed=0 | platform=left | inStation | emergStop | overrideOpen | inTunnel |
| --- | --- | --- | --- | --- | --- | --- |
| trainSpeed = 0 | T | t | t | t | t | t |
| trainSpeed != 0 |  |  |  |  |  |  |
| platform = left |  |  |  |  |  |  |
| platform != left |  |  |  |  |  |  |
| inStation |  |  |  |  |  |  |
| ¬ inStation |  |  |  |  |  |  |
| emergencyStop |  |  |  |  |  |  |
| ¬ emergStop |  |  |  |  |  |  |
| overrideOpen |  |  |  |  |  |  |
| ¬ overrideOpen |  |  |  |  |  |  |
| inTunnel |  |  |  |  |  |  |
| ¬ inTunnel |  |  |  |  |  |  |

| Major Clause | Speed=0 | platform=left | inStation | emergStop | overrideOpen | inTunnel |
| --- | --- | --- | --- | --- | --- | --- |
| trainSpeed = 0 | T | t | t | t | t | t |
| trainSpeed != 0 | F | t | t | t | t | t |
| platform = left | t | T | t | t | t | t |
| platform != left | t | F | t | t | t | t |
| inStation | t | t | T | f | f | f |
| ¬ inStation | t | t | F | f | f | f |
| emergencyStop | t | t | f | T | t | t |
| ¬ emergStop | t | t | f | F | t | t |
| overrideOpen | t | t | f | t | T | t |
| ¬ overrideOpen | t | t | f | t | F | t |
| inTunnel | t | t | f | t | t | T |
| ¬ inTunnel | t | t | f | t | t | F |

- **One of these must be true**
- **One of these must be false**

## Slide 9

- **Problem With a Predicate?**
- **9**
|  | trainSpeed=0 | platform=left | inStation | emergencyStop | overrideOpen | inTunnel |
| --- | --- | --- | --- | --- | --- | --- |
| inStation | t | t | T | f | f | f |
| ¬ inStation | t | t | F | f | f | f |

- **The model only has two locations**
- **inStation and inTunnel**
- **So these cannot both be false!**
- **If the train is not in the station (location != inStation), then it must be in a tunnel (location = inTunnel)**
- **Possible solutions :**
- **Check with the developer for mistakes (do this first)**
- **Rewrite the predicate to eliminate dependencies (if possible)**
- **Change truth assignment :  t  t  F  f  f  t**
- **Do you see a problem here?**
- **Think about these two values …**

## Slide 10

- **Expected Results**
- **10**
- **Expected outputs are read from the FSM :**
- **When the major clause is true, the transition is taken**
- **When false, the transition is not taken**
|  | Expected Results |
| --- | --- |
| trainSpeed = 0 |  |
| trainSpeed != 0 |  |
| platform = left |  |
| platform != left |  |
| inStation |  |
| ¬ inStation |  |
| emergencyStop |  |
| ¬ emergencyStop |  |
| overrideOpen |  |
| ¬ overrideOpen |  |
| inTunnel |  |
| ¬ inTunnel |  |

- **Fill in the expected results**

## Slide 11

|  | Expected Results |
| --- | --- |
| trainSpeed = 0 |  |
| trainSpeed != 0 |  |
| platform = left |  |
| platform != left |  |
| inStation |  |
| ¬ inStation |  |
| emergencyStop |  |
| ¬ emergencyStop |  |
| overrideOpen |  |
| ¬ overrideOpen |  |
| inTunnel |  |
| ¬ inTunnel |  |

|  | Expected Results |
| --- | --- |
| trainSpeed = 0 | Left Doors Open |
| trainSpeed != 0 | All Doors Closed |
| platform = left | Left Doors Open |
| platform != left | All Doors Closed |
| inStation | Left Doors Open |
| ¬ inStation | All Doors Closed |
| emergencyStop | Left Doors Open |
| ¬ emergencyStop | All Doors Closed |
| overrideOpen | Left Doors Open |
| ¬ overrideOpen | All Doors Closed |
| inTunnel | Left Doors Open |
| ¬ inTunnel | All Doors Closed |

- **Expected Results**
- **11**
- **Expected outputs are read from the FSM :**
- **When the major clause is true, the transition is taken**
- **When false, the transition is not taken**
- **Do you notice anything “funny”?**
- **What about here?**
- **If platform !=left, then platform must equal right**
- **So the expected output of this test is to go to state “Right Doors Open”**
- **Accidental transitions must be recognized when designing expected results during test automation**

## Slide 12

- **Early Identification is a Win!**
- **12**
- **The process of modeling software artifacts for test design can help us find defects in the artifacts**
- **This is a very powerful side-effect of the model-driven test design process**

## Slide 13

- **Complicating Issues**
- **Some buttons must be pressed simultaneously to have effect – so timing must be tested**
- **Reachability : The tests must reach the state where the transition starts (the prefix)**
- **Exit : Some tests must continue executing to an end state**
- **Expected output : The expected output is the state that the transition reaches for true values, or same state for false values**
- **Accidental transitions : Sometimes a false value for one transition happens to be a true value for another**
  - The alternate expected output must be recognized
- **13**

## Slide 14

- **Test Automation Issues**
- **Mapping problem : The names used in the FSMs may not match the names in the program**
- **Examples**
  - platform = left requires the train to go to a specific station
  - trainspeed = 0 probably requires the brake to be applied multiple times
- **The solution to this is implementation-specific**
  - Sometimes a direct name-to-name mapping can be found
  - Sometimes more complicated actions must be taken to assign the appropriate values
  - Simulation : Directly inserting value assignments into the middle of the program
- **This is an issue of controllability**
- **14**

## Slide 15

- **Summary FSM Logic Testing**
- **FSMs are widely used at all levels of abstraction**
- **Many ways to express FSMs**
  - Statecharts, tables, Z, decision tables, Petri nets, …
- **Predicates are usually explicitly included on the transitions**
  - Guards
  - Actions
  - Often represent safety constraints
- **FSMs are often used in embedded software**
- **15**
