<!-- Slide 1 -->

Chapter 1 Introduction
Why Do We Test Software?

---

<!-- Slide 2 -->

本节课程目标

【重点】从风险控制视角理解测试存在的工程意义。
【难点】明确fault、failure、error、bug的具体含义和区别；
【难点】根据RIPR模型分析代码中潜在的fault及其可能导致的error和failure；
正确理解软件测试的作用和价值。
2

---

<!-- Slide 3 -->

Software is a Skin that Surrounds Our Civilization
3
Quote due to Dr. Mark Harman

---

<!-- Slide 4 -->

Software Failures
2020: More than 100 flights to and from London’s Heathrow airport disruption due to issues with departure boards and check-in systems
2019: Facebook, Instagram, WhatsApp 14 hours downtime due to Facebook News Feed issue in routine maintenance
2019: Boeing 737 Max crashed due to aggressive software flight overrides
2018: Pedestrian in Arizona was killed by an Uber car due to its self-driving software failure
2018: Google shut down Google+ due to the undetected fault that was present for more than two years, causing nearly 500,000 users’ data to be compromised
2017: 606 recorded software failures, impacting 3.7 billion people, 314 companies, $1.7 trillion in financial losses

4

---

<!-- Slide 5 -->

Software Failures
2016: Nissan recalled 4 millions cars from the market due to software failure in the airbag sensory detectors
2003: Northeast blackout due to the alarm system in the energy management system failure, affecting 40 million people in 8 US states, 10 million people in Ontario, Canada
1999: NASA’s Mars lander crashed due to a unit integration fault
1997: Ariane 5 explosion: Exception-handling bug forced self-destruct on maiden flight (64-bit to 16-bit conversion), causing $370 millions
1986: 3 patients were killed by Therac-25 radiation machine due to poor testing of its safety-critical software
5

---

<!-- Slide 6 -->

Terms for Software Failures
Fault（故障）, failure（失败）, and defect（缺陷） tend to imply a condition that's really severe, maybe even dangerous.
It doesn't sound right to call an incorrectly colored icon a fault.
These words also tend to imply blame: "It's his fault that the software failed."
Anomaly, incident, and variance don't sound quite so negative and are often used to infer unintended operation rather than all-out failure.
"The president stated that it was a software anomaly that caused the missile to go off course."
**Problem, error（错误）, and bug are probably the most generic terms used.**


6

---

<!-- Slide 7 -->

Software Faults, Errors & Failures
Software Fault : A static defect in the software

Software Failure : External, incorrect behavior with respect to the requirements or other description of the expected behavior

Software Error : An incorrect internal state that is the manifestation of some fault
7
### Faults in software are equivalent to design mistakes in hardware.
### Software does not degrade.

---

<!-- Slide 8 -->

Fault and Failure Example
A patient gives a doctor a list of symptoms
Failures
The doctor tries to diagnose the root cause, the ailment
Fault
The doctor may look for anomalous internal conditions (high blood pressure, irregular heartbeat, bacteria in the blood stream)
Errors
8
### Most medical problems result from external attacks (bacteria, viruses) or physical degradation as we age.
### Software faults were there at the beginning and do not “appear” when a part wears out.

---

<!-- Slide 9 -->

A Concrete Example
### Identify the fault.
### If possible, identify a test case that does not execute the fault.
### If possible identify a test case that results in error, but not a failure.
#### Public  static  int  numZero (int [ ] arr)
#### {
#### // Effects: If arr is null throw NullPointerException
#### // else return the number of occurrences of 0 in arr

#### int count = 0;
#### for (int i = 1; i < arr.length; i++)
#### {
#### if (arr [ i ] == 0)
#### {
#### count++;
#### }
#### }
#### return count;
#### }

---

<!-- Slide 10 -->

A Concrete Example
10
public static int numZero (int [ ] arr)
{  // Effects: If arr is null throw NullPointerException
// else return the number of occurrences of 0 in arr
int count = 0;
for (int i = 1; i < arr.length; i++)
{
if (arr [ i ] == 0)
{
count++;
}
}
return count;
}

Fault: Should start searching at 0, not 1
Test 1
[ 2, 7, 0 ]
Expected: 1
Actual: 1
Test 2
[ 0, 2, 7 ]
Expected: 1
Actual: 0
Error: i is 1, not 0, on the first iteration
Failure: none
Error:  i is 1, not 0
Error propagates to the variable count
Failure: count is 0 at the return statement

---

<!-- Slide 11 -->

#### Public  static  int  numZero (int [ ] arr)
#### {
#### // Effects: If arr is null throw NullPointerException
#### // else return the number of occurrences of 0 in arr

#### int count = 0;
#### for (int i = 1; i < arr.length; i++)
#### {
#### if (arr [ i ] == 0)
#### {
#### count++;
#### }
#### }
#### return count;
#### }
A Concrete Example
arr = [2, 7, 0]
count = 0


arr = [2, 7, 0]
count = 0
i = 1
PC = if

i=1

arr = [2, 7, 0]
count = 0
i = 0


---

<!-- Slide 12 -->

12
Fault & Failure Model (RIPR)
Four conditions necessary for a failure to be observed

Reachability : The location or locations in the program that contain the fault must be reached
Infection : The state of the program must be incorrect
Propagation : The infected state must cause some output or final state of the program to be incorrect
Reveal : The tester must observe part of the incorrect portion of the program state

---

<!-- Slide 13 -->

RIPR Model
Reachability
Infection
Propagation
Revealability
### Test
### Fault
### Incorrect Program State

### Test Oracles
### Final Program State
### Observed Final Program State
### Reaches
### Infects
### Propagates
### Reveals
### Incorrect Final State
13
### Observed Final Program State

---

<!-- Slide 14 -->

14
Testing & Debugging
Testing : Evaluating software by observing its execution

Test Failure : Execution of a test that results in a software failure

Debugging : The process of finding a fault given a failure
## Not all inputs will “trigger” a fault into causing a failure

---

<!-- Slide 15 -->

The Term Bug
### Bug is used informally
### Sometimes speakers mean fault, sometimes error, sometimes failure … often the speaker doesn’t know what it means !
### This class will try to use words that have precise, defined, and unambiguous meanings

15
#### “It has been just so in all of my inventions. The first step is an intuition, and comes with a burst, then difficulties arise—this thing gives out and [it is] then that 'Bugs'—as such little faults and difficulties are called—show themselves and months of intense watching, study and labor are requisite. . .” – Thomas Edison
#### “an analyzing process must equally have been performed in order to furnish the Analytical Engine with the necessary operative data; and that herein may also lie a possible source of error. Granted that the actual mechanism is unerring in its processes, the cards may give it wrong orders. ” – Ada, Countess Lovelace (notes on Babbage’s Analytical Engine)

---

<!-- Slide 16 -->

Product Specification
## A product specification, sometimes referred to as simply a spec or product spec, is an agreement among the software development team.
## It defines the product they are creating, detailing what it will be, how it will act, what it will do, and what it won't do.
16

---

<!-- Slide 17 -->

Formal Definition of Bug
## A software bug occurs when one or more of the following five rules is true:
## The software doesn't do something that the product specification says it should do.
## The software does something that the product specification says it shouldn't do.
## The software does something that the product specification doesn't mention.
## The software doesn't do something that the product specification doesn't mention but should.
## The software is difficult to understand, hard to use, slow, or in the software tester's eyes will be viewed by the end user as just plain not right.

17

---

<!-- Slide 18 -->

An Example
### The specification for a calculator probably states that it will perform correct addition, subtraction, multiplication, and division. The product spec might state that the calculator should never crash, lock up, or freeze.
If you, as the tester, receive the calculator, press the + key, and nothing happens, that's a bug because of Rule ??
If you get the wrong answer, that's a bug because of Rule ??
If you pound on the keys and get the calculator to stop responding to your input, that's a bug because of Rule ??
Suppose that you receive the calculator for testing and find that besides addition, subtraction, multiplication, and division, it also performs square roots. Is it a feature or a bug because of Rule ??
You start testing the calculator and discover when the battery gets weak that you no longer receive correct answers to your calculations. It is a bug because of Rule ??
You found that the buttons were too small. Maybe the placement of the = key made it hard to use. Maybe the display was difficult to read under bright lights. All of these are bugs because of Rule ??

18

---

<!-- Slide 19 -->

Where are errors？

19

---

<!-- Slide 20 -->

The Average Cost to Fix Fault

20

---

<!-- Slide 21 -->

Software Testability (3.1)
Plainly speaking – how hard it is to find faults in the software
Testability is dominated by two practical problems
How to provide the test values to the software
How to observe the results of test execution
21
## The degree to which a system or component facilitates the establishment of test criteria and the performance of tests to determine whether those criteria have been met

---

<!-- Slide 22 -->

Observability and Controllability
Observability



Software that affects hardware devices, databases, or remote files have low observability
Controllability


Easy to control software with inputs from keyboards
Inputs from hardware sensors or distributed software is harder
Data abstraction reduces controllability and observability
22
## How easy it is to observe the behavior of a program in terms of its outputs, effects on the environment and other hardware and software components
## How easy it is to provide a program with the needed inputs, in terms of values, operations, and behaviors

---

<!-- Slide 23 -->

Components of a Test Case (3.2)
A test case is a multipart artifact with a definite structure

Test case values



Expected results


A test oracle uses expected results to decide whether a test passed or failed
23
## The result that will be produced by the test if the software behaves as expected
## The input values needed to complete an execution of the software under test

---

<!-- Slide 24 -->

Affecting Controllability and Observability
Prefix values


Postfix values


Verification Values : Values needed to see the results of the test case values
Exit Values : Values or commands needed to terminate the program or otherwise return it to a stable state
24
## Any inputs that need to be sent to the software after the test case values are sent
## Inputs necessary to put the software into the appropriate state to receive the test case values

---

<!-- Slide 25 -->

Putting Tests Together
Test case



Test set


Executable test script
25
## The test case values, prefix values, postfix values, and expected results necessary for a complete execution and evaluation of the software under test
## A set of test cases
## A test case that is prepared in a form to be executed automatically on the test software and produce a report

---

<!-- Slide 26 -->

Testing in the 21st Century
More safety critical, real-time software
Embedded software is ubiquitous … check your pockets
Enterprise applications means bigger programs, more users
Security is now all about software faults
Secure software is reliable software
The web offers a new deployment platform
Very competitive and very available to more users
Web apps are distributed
Web apps must be highly reliable
Artificial Intelligence Software
26
## Industry desperately needs our inventions !

---

<!-- Slide 27 -->

What Does This Mean?
27
## Software testing is getting more important
## What are we trying to do when we test ?
## What are our goals ?

---

<!-- Slide 28 -->

## Validation & Verification (IEEE)
Validation : The process of evaluating software at the end of software development  to ensure compliance with intended usage

Verification : The process of determining whether the products of a given phase of the software development process fulfill the requirements established during the previous phase


IV&V stands for “independent verification and validation”
28

---

<!-- Slide 29 -->

## A case study for distinguishing Validation & Verification
### In April 1990, the Hubble space telescope was launched into orbit around the Earth. As a reflective telescope, Hubble uses a large mirror as its primary means to magnify the objects it's aiming at.
### The only means to test it was to carefully measure all its attributes and compare the measurements with what was specified. This testing was performed and Hubble was declared fit for launch. Unfortunately, soon after it was put into operation, the images it returned were found to be out of focus.
### An investigation discovered that the mirror was improperly manufactured. The mirror was ground according to the specification, but the specification was wrong. The mirror was extremely precise, but it wasn't accurate. Testing had confirmed that the mirror met the spec verification but it didn't confirm that it met the original requirement validation.
### In 1993, a space shuttle mission repaired the Hubble telescope by installing a "corrective lens" to refocus the image generated by the improperly manufactured mirror.
### Although this is a not a software example, verification and validation apply equally well to software testing. Never assume that the specification is correct. If you verify the spec and validate the final product, you help avoid problems such as the one that hit the Hubble telescope.

29

---

<!-- Slide 30 -->

30
Testing Goals Based on Test Process Maturity
Level 0 : There’s no difference between testing and debugging
## Level 1 : The purpose of testing is to show correctness
## Level 2 : The purpose of testing is to show that the software doesn’t work
## Level 3 : The purpose of testing is not to prove anything specific, but to reduce the risk of using the software
## Level 4 : Testing is a mental discipline that helps all IT professionals develop higher quality software

---

<!-- Slide 31 -->

31
Level 0 Thinking
## Testing is the same as debugging

## Does not distinguish between incorrect behavior and mistakes in the program

## Does not help develop software that is reliable or safe
## This is what we teach undergraduate CS majors

---

<!-- Slide 32 -->

32
Level 1 Thinking
## Purpose is to show correctness
## Correctness is impossible to achieve
## What do we know if no failures?
Good software or bad tests?
## Test engineers have no:
Strict goal
Real stopping rule
Formal test technique
Test managers are powerless
## This is what hardware engineers often expect

---

<!-- Slide 33 -->

33
Level 2 Thinking
## Purpose is to show failures

## Looking for failures is a negative activity

## Puts testers and developers into an adversarial relationship

## What if there are no failures?
## This describes most software companies.
## How can we move to a team approach ??

---

<!-- Slide 34 -->

34
Level 3 Thinking
## Testing can only show the presence of failures

## Whenever we use software, we incur some risk

## Risk may be small and consequences unimportant

## Risk may be great and consequences catastrophic

## Testers and developers cooperate to reduce risk
## This describes a few “enlightened” software companies

---

<!-- Slide 35 -->

35
Level 4 Thinking
# A mental discipline that increases quality

Testing is only one way to increase quality

Test engineers can become technical leaders of the project

Primary responsibility to measure and improve software quality

Their expertise should help the developers
## This is the way “traditional” engineering works

---

<!-- Slide 36 -->

Where Are You?
36
## Are you at level 0, 1, or 2 ?
## Is your organization at work at level 0, 1, or 2 ?
## Or 3?
## We hope to teach you to become “change agents” in your workplace …
## Advocates for level 4 thinking

---

<!-- Slide 37 -->

Tactical Goals : Why Each Test ?
37
## Written test objectives and requirements must be documented
## What are your planned coverage levels?
## How much testing is enough?
## Common objective – spend the budget … test until the ship-date …
## Sometimes called the “date criterion”
## If you don’t know why you’re conducting each test, it won’t be very helpful

---

<!-- Slide 38 -->

38
Why Each Test ?
## 1980: “The software shall be easily maintainable”

## Threshold reliability requirements?

## What fact does each test try to verify?

## Requirements definition teams need testers!
## If you don’t start planning for each test when the functional requirements are formed, you’ll never know why you’re conducting the test

---

<!-- Slide 39 -->

39
Cost of Not Testing
## Testing is the most time consuming and expensive part of software development
## Not testing is even more expensive
## If we have too little testing effort early, the cost of testing increases
## Planning for testing after development is prohibitively expensive
## Poor Program Managers might say: “Testing is too expensive.”

---

<!-- Slide 40 -->


Cost of Late Testing
40
60













Requirements
Prog / Unit Test
Design
Integration Test
#### Fault origin (%)

#### Fault detection (%)

#### Unit cost (X)



#### Software Engineering Institute; Carnegie Mellon University; Handbook CMU/SEI-96-HB-002
Assume $1000 unit cost, per fault, 100 faults


System Test
Post-Deployment

---

<!-- Slide 41 -->

Summary:Why Do We Test Software ?
41
## A tester’s goal is to eliminate faults as early as possible
## Improve quality
## Reduce cost
## Preserve customer satisfaction

---

<!-- Slide 42 -->

Exercise
42
#### The following faulty program includes test inputs that result in failure.  Answer the following questions about the program.
#### (a) Explain what is wrong with the given code. Describe the fault precisely by proposing a modiﬁcation to the code.
#### (b) If possible, give a test case that does not execute the fault. If not, brieﬂy explain why not.
#### (c) If possible, give a test case that executes the fault, but does not result in an error state. If not, brieﬂy explain why not.
#### (d) If possible, give a test case that results in an error state, but not a failure. Hint: Don’t forget about the program counter. If not, brieﬂy explain why not.
#### (e) For the given test case, describe the ﬁrst error state. Be sure to describe the complete state.
#### (f) Implement your repair and verify that the given test now produces the expected output. Submit a screen printout or other evidence that your new program works.

---
