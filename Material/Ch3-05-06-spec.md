<!-- Slide 1 -->

Chapter 2 Graph Coverage
## 3.5 Graph Coverage for Specifications

---

<!-- Slide 2 -->

本节课程目标
明确针对顺序约束、状态机、用例图（活动图）进行图覆盖的思路，写出对应的测试需求和测试路径；
明确状态机的构造方法。
2

---

<!-- Slide 3 -->

3
Design Specifications
A design specification describes aspects of what behavior software should exhibit

A design specification may or may not reflect the implementation
More accurately – the implementation may not exactly reflect the spec
Design specifications are often called models of the software

Two types of descriptions are used in this chapter
Sequencing constraints on class methods
State behavior descriptions of software

---

<!-- Slide 4 -->

4
Sequencing Constraints
Sequencing constraints are rules that impose constraints on the order in which methods may be called
They can be encoded as preconditions or other specifications
Section 2.4 said that classes often have methods that do not call each other
## Tests can be created for these classes as sequences of method calls
## Sequencing constraints give an easy and effective way to choose which sequences to use

---

<!-- Slide 5 -->

5
Sequencing Constraints Overview
Sequencing constraints might be
Expressed explicitly
Expressed implicitly
Not expressed at all
Testers should derive them if they do not exist
Look at existing design documents
Look at requirements documents
Ask the developers
Last choice : Look at the implementation
If they don’t exist, expect to find more faults !
Share with designers before designing tests
Sequencing constraints do not capture all behavior

---

<!-- Slide 6 -->

6
Queue Example
Sequencing constraints are implicitly embedded in the pre and postconditions
enQueue () must be called before deQueue ()
Does not include the requirement that we must have at least as many enQueue () calls as deQueue () calls
Can be handled by state behavior techniques
### public int deQueue(){   // Pre: At least one element must be on the queue.   … …
### public enQueue (int e){   // Post: e is on the end of the queue.

---

<!-- Slide 7 -->

7
File ADT Example
class FileADT has three methods:
open (String fName) // Opens file with name fName
close () // Closes the file and makes it unavailable
write (String textLine) // Writes a line of text to the file
### Valid sequencing constraints on FileADT:
### An open (f) must be executed before every write (t)
### An open (f) must be executed before every close ()
### A write (f) may not be executed after a close () unless there is an open (f) in between
### A write (t) should be executed before every close ()
Client that uses FileADT

---

<!-- Slide 8 -->

8
Static Checking
Is there a path to a write() that does not go through an open() ?
Is there a path to a close() that does not go through an open() ?
Is there a path from a close() to a write()?
Is there a path from an open() to a close() that does not go through a write() ? (“write-clear” path)
### Is there a path that violates any of the sequencing constraints ?
### [ 1, 3, 4, 6 ] – ADT use anomaly!

---

<!-- Slide 9 -->

9
Static Checking
## Consider the following graph :
### [ 7, 3, 4 ] – close () before write () !

---

<!-- Slide 10 -->

10
Generating Test Requirements
Use the sequencing constraints to generate test requirements
The goal is to violate every sequencing constraint








#### open (f)
#### write (t)
#### write (t)
#### close ()
### [ 1, 3, 4, 6 ] – ADT use anomaly!
### But it is possible that the logic of the program does not allow the pair of edges [1, 3, 4]
### That is – the loop body must be taken at least once
### Determining this is undecidable – so static methods are not enough

---

<!-- Slide 11 -->

11
Test Requirements for FileADT
### Cover every path from the start node to every node that contains a write() such that the path does not go through a node containing an open()
### Cover every path from the start node to every node that contains a close() such that the path does not go through a node containing an open()
### Cover every path from every node that contains a close() to every node that contains a write()
### Cover every path from every node that contains an open() to every node that contains a close() such that the path does not go through a node containing a write()
### Apply to all programs that use FileADT
### If program is correct, all test requirements will be infeasible
### Any tests created will almost definitely find faults

---

<!-- Slide 12 -->

12
Testing State Behavior
A finite state machine (FSM) is a graph that describes how software variables are modified during execution
Nodes : States, representing sets of values for key variables
Edges : Transitions, possible changes in the state

---

<!-- Slide 13 -->

13
## Finite State Machine—Two Variables
Tropical Depression
#### circulation = yes
#### windspeed < 39mph
### Other variables may exist but not be part of state

---

<!-- Slide 14 -->

14
## Finite State Machines are Common
FSMs can accurately model many kinds of software
Embedded and control software (think electronic gadgets)
Abstract data types
Compilers and operating systems
Web applications
Creating FSMs can help find software problems
Numerous languages for expressing FSMs
UML statecharts
Automata
State tables (SCR)
Petri nets
Limitation : FSMs are not always practical for programs that have lots of states (for example, GUIs)

---

<!-- Slide 15 -->

15
Annotations on FSMs
FSMs can be annotated with different types of actions
Actions on transitions
Entry actions to nodes
Exit actions on nodes
Actions can express changes to variables or conditions on variables
These slides use the basics:
Preconditions (guards) : conditions  that must be true for transitions to be taken
Triggering events : changes to variables that cause transitions to be taken
This is close to the UML Statecharts, but not exactly the same

---

<!-- Slide 16 -->

16
Example Annotations
### open elevator door
### pre: elevSpeed = 0
### trigger: openButton = pressed

---

<!-- Slide 17 -->

17
Covering FSMs
Node coverage : execute every state (state coverage)
Edge coverage : execute every transition (transition coverage)
Edge-pair coverage : execute every pair of transitions (transition-pair)
Data flow:
Nodes often do not include defs or uses of variables
Defs of variables in triggers are used immediately (the next state)
Defs and uses are usually computed for guards, or states are extended
FSMs typically only model a subset of the variables
Generating FSMs is often harder than covering them …

---

<!-- Slide 18 -->

18
Deriving FSMs
With some projects, an FSM (such as a statechart) was created during design
Tester should check to see if the FSM is still current with respect to the implementation
If not, it is very helpful for the tester to derive the FSM
Strategies for deriving FSMs from a program:
Combining control flow graphs (wrong)
Using the software structure (wrong)
Modeling state variables
Example based on a digital watch …
Class Watch uses class Time

---

<!-- Slide 19 -->

19
Class Watch
class Watch
#### // Constant values for the button (inputs)
#### private static final int NEXT = 0;
#### private static final int UP   = 1;
#### private static final int DOWN = 2;
#### // Constant values for the state
#### private static final int TIME      = 5;
#### private static final int STOPWATCH = 6;
#### private static final int ALARM     = 7;
#### // Primary state variable
#### private int mode = TIME;
#### // Three separate times, one for each state
#### private Time watch, stopwatch, alarm;

#### public Watch () // Constructor
#### public void doTransition (int button) // Handles inputs
#### public String toString ()  // Converts values



#### class Time   ( inner class )
#### private int hour   = 0;
#### private int minute = 0;

#### public void changeTime (int button)
#### public String toString ()



---

<!-- Slide 20 -->

20
#### // Takes the appropriate transition when a button is pushed.
#### public void doTransition (int button)
#### {
#### switch ( mode )
#### {
#### case TIME:
#### if (button == NEXT)
#### mode = STOPWATCH;
#### else
#### watch.changeTime (button);
#### break;
#### case STOPWATCH:
#### if (button == NEXT)
#### mode = ALARM;
#### else
#### stopwatch.changeTime (button);
#### break;
#### case ALARM:
#### if (button == NEXT)
#### mode = TIME;
#### else
#### alarm.changeTime (button);
#### break;
#### default:
#### break;
#### }
#### }  // end doTransition()
#### // Increases or decreases the time.
#### // Rolls around when necessary.
#### public void changeTime (int button)
#### {
#### if (button == UP)
#### {
#### minute += 1;
#### if (minute >= 60)
#### {
#### minute = 0;
#### hour += 1;
#### if (hour > 12)
#### hour = 1;
#### }
#### }
#### else if (button == DOWN)
#### {
#### minute -= 1;
#### if (minute < 0)
#### {
#### minute = 59;
#### hour -= 1;
#### if (hour <= 0)
#### hour = 12;
#### }
#### }
#### }  // end changeTime()

---

<!-- Slide 21 -->

21
## 1. Combining Control Flow Graphs
The first instinct for inexperienced developers is to draw CFGs and link them together
This is really not an FSM
Several problems
Methods must return to correct callsites—implicit nondeterminism
Implementation must be available before graph can be built
This graph does not scale up
Watch example …

---

<!-- Slide 22 -->

22

CFGs for Watch
1
2
3
4
11
12
13
14

doTransition ()

---

<!-- Slide 23 -->

23
2. Using the Software Structure
A more experienced programmer may map methods to states

These are really not states

Problems
Subjective—different testers get different graphs
Requires in-depth knowledge of implementation
Detailed design must be present

Watch example …

---

<!-- Slide 24 -->

24
Software Structure for Watch
#### button
### inMain
### inChangeTime
### inDoTransition
#### button==NEXT / change mode
#### button==UP or button==DOWN
#### button==DOWN / change hour, minute
#### button==UP   / change hour, minute

---

<!-- Slide 25 -->

25
3. Modeling State Variables
More mechanical
State variables are usually defined early
First identify all state variables, then choose which are relevant
In theory, every combination of values for the state variables defines a different state
In practice, we must identify ranges, or sets of values, that are all in one state
Some states may not be feasible

---

<!-- Slide 26 -->

26
State Variables in Watch
Constants
NEXT, UP, DOWN
TIME, STOPWATCH, ALARM

Non-constant variables in class Watch
int mode (values: TIME, STOPWATCH, ALARM)
Time watch, stopwatch, alarm

---

<!-- Slide 27 -->


27
State Variables in Time
Non-constant variables in class Time
int hour (values: 1..12)
int minute (values: 0 .. 59)
### 12 X 60 values is 720 states
### Clearly, that is too many
Combine values into ranges of similar values :
hour : 1.. 11, 12
minute : 0, 1.. 59
Four states : (1..11, 0); (12, 0); (1..11, 1.. 59); (12, 1 .. 59)
### Clumsy ... Not sequential …
### let’s combine hour and minute …
Time : 12:00, 12:01..12:59,  01:00 .. 11:59
These require lots of thought and semantic domain knowledge of the program

---

<!-- Slide 28 -->

Hierarchical FSMs
One FSM is contained within the other
28
### S1
### S3
### S2
a
b
c
### Class Watch uses class Time
### How can we model two classes—one that uses another?

---

<!-- Slide 29 -->

Watch / Time Hierarchical FSM
29
### next
### next
### next

---

<!-- Slide 30 -->

30
Summary–Tradeoffs in Applying Graph Coverage Criteria to FSMs
Two advantages
Tests can be designed before implementation
Analyzing FSMs is much easier than analyzing source

Three disadvantages
Some implementation decisions are not modeled in the FSM
There is some variation in the results because of the subjective nature of deriving FSMs
Tests have to be “mapped” to actual inputs to the program – the names that appear in the FSM may not be the same as the names in the program

---

<!-- Slide 31 -->

Chapter 2 Graph Coverage
## 3.6 Graph Coverage for Use Cases

---

<!-- Slide 32 -->

32
UML Use Cases
UML use cases are often used to express software requirements

They help express computer application workflow

We won’t teach use cases, but show examples

---

<!-- Slide 33 -->

33

Simple Use Case Example
Actors : Humans or software components that use the software being modeled
Use cases : Shown as circles or ovals
Node Coverage : Try each use case once …



#### ATM
#### User
### Use case graphs, by themselves, are not useful for testing

---

<!-- Slide 34 -->

34
Elaboration
Use cases are commonly elaborated (or documented)

Elaboration is first written textually

Details of operation

Alternatives model choices and conditions during execution

---

<!-- Slide 35 -->

Elaboration of ATM Use Case
### Use Case Name : Withdraw Funds
### Summary : Customer uses a valid card to withdraw funds from a valid bank account.
### Actor : ATM Customer
### Precondition : ATM is displaying the idle welcome message
### Description :
#### Customer inserts an ATM Card into the ATM Card Reader.
#### If the system can recognize the card, it reads the card number.
#### System prompts the customer for a PIN.
#### Customer enters PIN.
#### System checks the card’s expiration date and whether the card has been stolen or lost.
#### If the card is valid, the system checks if the entered PIN matches the card PIN.
#### If the PINs match, the system finds out what accounts the card can access.
#### System displays customer accounts and prompts the customer to choose a type of transaction.  There are three types of transactions, Withdraw Funds, Get Balance and Transfer Funds.  (The previous eight steps are part of all three use cases; the following steps are unique to the Withdraw Funds use case.)
35

---

<!-- Slide 36 -->

## Elaboration of ATM Use Case—(2/3)
### Description (continued) :
#### Customer selects Withdraw Funds, selects the account number, and enters the amount.
#### System checks that the account is valid, makes sure that customer has enough funds in the account, makes sure that the daily limit has not been exceeded, and checks that the ATM has enough funds.
#### If all four checks are successful, the system dispenses the cash.
#### System prints a receipt with a transaction number, the transaction type, the amount withdrawn, and the new account balance.
#### System ejects card.
#### System displays the idle welcome message.
36

---

<!-- Slide 37 -->

## Elaboration of ATM Use Case—(3/3)
#### Alternatives :
#### If the system cannot recognize the card, it is ejected and the welcome message is displayed.
#### If the current date is past the card's expiration date, the card is confiscated and the welcome message is displayed.
#### If the card has been reported lost or stolen, it is confiscated and the welcome message is displayed.
#### If the customer entered PIN does not match the PIN for the card, the system prompts for a new PIN.
#### If the customer enters an incorrect PIN three times, the card is confiscated and the welcome message is displayed.
#### If the account number entered by the user is invalid, the system displays an error message, ejects the card and the welcome message is displayed.
#### If the request for withdraw exceeds the maximum allowable daily withdrawal amount, the system displays an apology message, ejects the card and the welcome message is displayed.
#### If the request for withdraw exceeds the amount of funds in the ATM, the system displays an apology message, ejects the card and the welcome message is displayed.
#### If the customer enters Cancel, the system cancels the transaction, ejects the card and the welcome message is displayed.
#### Postcondition :
#### Funds have been withdrawn from the customer’s account.
37

---

<!-- Slide 38 -->

38
Wait A Minute …
What does this have to do with testing ?

Specifically, what does this have to do with graphs ???

Remember our admonition : Find a  graph, then cover it!

Beizer suggested “Transaction Flow Graphs” in his book

UML has something very similar :
## Activity Diagrams

---

<!-- Slide 39 -->

39
Use Cases to Activity Diagrams
Activity diagrams indicate flow among activities
Activities should model user level steps
Two kinds of nodes:
Action states
Sequential branches
Use case descriptions become action state nodes in the activity diagram
Alternatives are sequential branch nodes
Flow among steps are edges
Activity diagrams usually have some helpful characteristics:
Few loops
Simple predicates
No obvious DU pairs

---

<!-- Slide 40 -->

40
ATM Withdraw Activity Graph

---

<!-- Slide 41 -->

41
Covering Activity Graphs
Node Coverage
Inputs to the software are derived from labels on nodes and predicates
Used to form test case values
Edge Coverage
Data flow techniques do not apply
Scenario Testing
Scenario : A complete path through a use case activity graph
Should make semantic sense to the users
Number of paths often finite
If not, scenarios defined based on domain knowledge
Use “specified path coverage,” where the set S of paths is the set of scenarios
Note that specified path coverage does not necessarily subsume edge coverage, but scenarios should be defined so that it does

---

<!-- Slide 42 -->

Summary of Use Case Testing
Use cases are defined at the requirements level
Can be very high level
UML Activity Diagrams encode use cases in graphs
Graphs usually have a fairly simple structure
Requirements-based testing can use graph coverage
Straightforward to do by hand
Specified path coverage makes sense for these graphs
42

---
